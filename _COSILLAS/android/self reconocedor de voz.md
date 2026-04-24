No puedes “agarrar el micrófono del teclado” (Gboard u otro). El teclado usa sus **propios** servicios internos y Android **no expone** una API para “leer” lo que el teclado reconoce por voz.  
Lo correcto (y estándar) es usar:

- **`SpeechRecognizer`** (voz-a-texto del sistema/Google), con **resultados parciales** en “tiempo real”.
- Si luego necesitas *word timestamps*, offline, o control fino: **Vosk / Whisper (JNI)**, pero para tu “primer paso” `SpeechRecognizer` es lo más rápido.

Abajo te dejo una estructura MVVM + 2 pantallas (Start + Listening con animación) y que imprima texto parcial en realtime.

---

## 1) MVVM aplicado a tus 2 vistas

### Pantalla 1: “Inicio”
- View: `HomeScreen`
- VM: `HomeViewModel` (opcional, aquí puede ser simple)
- Acción: navegar a “Listening” y comenzar a escuchar

### Pantalla 2: “Escuchando”
- View: `ListeningScreen` (animación + lista/texto en vivo)
- VM: `ListeningViewModel`
- “Model”/infra: `SpeechRecognizerManager` (clase que envuelve callbacks y emite `StateFlow`)

**Regla:** La UI no llama `SpeechRecognizer` directo; le manda eventos al ViewModel.

---

## 2) Limitación importante: “palabra por palabra sincrónico”
`SpeechRecognizer` te entrega:
- **frases parciales** (strings que van cambiando) mientras hablas.
- no siempre garantiza *cada palabra* individual como evento separado.
- tampoco es “sincrónico” (bloqueante); funciona por callbacks.

Aun así, puedes imprimir “realtime” (parciales) y si quieres “palabra por palabra”, puedes **tokenizar** el parcial y detectar “nuevas palabras” (aproximado).

---

## 3) Permisos y Manifest

### AndroidManifest.xml
```xml
<manifest ...>
    <uses-permission android:name="android.permission.RECORD_AUDIO" />
    <!-- Opcional si vas a escuchar con la app en primer plano prolongado:
         <uses-permission android:name="android.permission.FOREGROUND_SERVICE_MICROPHONE" />
    -->
    ...
</manifest>
```

Además en runtime debes pedir `RECORD_AUDIO`.

---

## 4) Implementación (Compose + MVVM + SpeechRecognizer)

### Estructura sugerida
```
com.rextrem.anotador
├── MainActivity.kt
├── navigation
│   └── NavGraph.kt
├── speech
│   └── SpeechRecognizerManager.kt
└── presentation
    ├── home
    │   └── HomeScreen.kt
    └── listening
        ├── ListeningScreen.kt
        └── ListeningViewModel.kt
```

---

### 4.1 Manager: wrapper de SpeechRecognizer (parciales realtime)
`speech/SpeechRecognizerManager.kt`
```kotlin
package com.rextrem.anotador.speech

import android.content.Context
import android.content.Intent
import android.os.Bundle
import android.speech.RecognitionListener
import android.speech.RecognizerIntent
import android.speech.SpeechRecognizer
import kotlinx.coroutines.flow.MutableStateFlow
import kotlinx.coroutines.flow.StateFlow

class SpeechRecognizerManager(private val context: Context) {

    sealed class State {
        data object Idle : State()
        data object Listening : State()
        data class Partial(val text: String) : State()
        data class Final(val text: String) : State()
        data class Error(val code: Int) : State()
    }

    private val _state = MutableStateFlow<State>(State.Idle)
    val state: StateFlow<State> = _state

    private var recognizer: SpeechRecognizer? = null

    fun start(languageTag: String = "es-ES") {
        if (!SpeechRecognizer.isRecognitionAvailable(context)) {
            _state.value = State.Error(code = -1000)
            return
        }

        if (recognizer == null) {
            recognizer = SpeechRecognizer.createSpeechRecognizer(context).apply {
                setRecognitionListener(object : RecognitionListener {
                    override fun onReadyForSpeech(params: Bundle?) {
                        _state.value = State.Listening
                    }

                    override fun onBeginningOfSpeech() {}
                    override fun onRmsChanged(rmsdB: Float) {}
                    override fun onBufferReceived(buffer: ByteArray?) {}
                    override fun onEndOfSpeech() {}

                    override fun onError(error: Int) {
                        _state.value = State.Error(error)
                    }

                    override fun onResults(results: Bundle?) {
                        val text = results
                            ?.getStringArrayList(SpeechRecognizer.RESULTS_RECOGNITION)
                            ?.firstOrNull()
                            .orEmpty()
                        _state.value = State.Final(text)
                    }

                    override fun onPartialResults(partialResults: Bundle?) {
                        val text = partialResults
                            ?.getStringArrayList(SpeechRecognizer.RESULTS_RECOGNITION)
                            ?.firstOrNull()
                            .orEmpty()
                        if (text.isNotBlank()) _state.value = State.Partial(text)
                    }

                    override fun onEvent(eventType: Int, params: Bundle?) {}
                })
            }
        }

        val intent = Intent(RecognizerIntent.ACTION_RECOGNIZE_SPEECH).apply {
            putExtra(
                RecognizerIntent.EXTRA_LANGUAGE_MODEL,
                RecognizerIntent.LANGUAGE_MODEL_FREE_FORM
            )
            putExtra(RecognizerIntent.EXTRA_LANGUAGE, languageTag)
            putExtra(RecognizerIntent.EXTRA_PARTIAL_RESULTS, true)
            putExtra(RecognizerIntent.EXTRA_CALLING_PACKAGE, context.packageName)
        }

        recognizer?.startListening(intent)
    }

    fun stop() {
        recognizer?.stopListening()
        _state.value = State.Idle
    }

    fun destroy() {
        recognizer?.destroy()
        recognizer = null
        _state.value = State.Idle
    }
}
```

---

### 4.2 ViewModel: estado para la pantalla Listening
`presentation/listening/ListeningViewModel.kt`
```kotlin
package com.rextrem.anotador.presentation.listening

import androidx.lifecycle.ViewModel
import androidx.lifecycle.viewModelScope
import com.rextrem.anotador.speech.SpeechRecognizerManager
import kotlinx.coroutines.flow.MutableStateFlow
import kotlinx.coroutines.flow.StateFlow
import kotlinx.coroutines.launch

data class ListeningUiState(
    val isListening: Boolean = false,
    val partialText: String = "",
    val words: List<String> = emptyList(),
    val errorCode: Int? = null
)

class ListeningViewModel(
    private val speech: SpeechRecognizerManager
) : ViewModel() {

    private val _uiState = MutableStateFlow(ListeningUiState())
    val uiState: StateFlow<ListeningUiState> = _uiState

    private var lastPartial = ""

    init {
        viewModelScope.launch {
            speech.state.collect { st ->
                when (st) {
                    is SpeechRecognizerManager.State.Idle -> {
                        _uiState.value = _uiState.value.copy(isListening = false)
                        lastPartial = ""
                    }
                    is SpeechRecognizerManager.State.Listening -> {
                        _uiState.value = _uiState.value.copy(isListening = true, errorCode = null)
                    }
                    is SpeechRecognizerManager.State.Partial -> {
                        val newWords = extractNewWords(lastPartial, st.text)
                        lastPartial = st.text

                        _uiState.value = _uiState.value.copy(
                            partialText = st.text,
                            words = _uiState.value.words + newWords,
                            errorCode = null
                        )
                    }
                    is SpeechRecognizerManager.State.Final -> {
                        // Puedes decidir reiniciar aquí para “continuo”
                        _uiState.value = _uiState.value.copy(partialText = st.text)
                    }
                    is SpeechRecognizerManager.State.Error -> {
                        _uiState.value = _uiState.value.copy(errorCode = st.code, isListening = false)
                        lastPartial = ""
                    }
                }
            }
        }
    }

    fun start() = speech.start(languageTag = "es-ES")
    fun stop() = speech.stop()

    override fun onCleared() {
        speech.destroy()
        super.onCleared()
    }

    // Aproximación: tokeniza y detecta palabras nuevas entre parciales
    private fun extractNewWords(oldText: String, newText: String): List<String> {
        val oldTokens = oldText.trim().split("\\s+".toRegex()).filter { it.isNotBlank() }
        val newTokens = newText.trim().split("\\s+".toRegex()).filter { it.isNotBlank() }

        if (newTokens.size <= oldTokens.size) return emptyList()

        return newTokens.drop(oldTokens.size)
    }
}
```

---

### 4.3 UI: HomeScreen con botón “Comenzar”
`presentation/home/HomeScreen.kt`
```kotlin
package com.rextrem.anotador.presentation.home

import androidx.compose.foundation.layout.*
import androidx.compose.material3.*
import androidx.compose.runtime.Composable
import androidx.compose.ui.Modifier
import androidx.compose.ui.unit.dp

@Composable
fun HomeScreen(
    onStart: () -> Unit
) {
    Scaffold(
        topBar = { TopAppBar(title = { Text("Inicio") }) }
    ) { padding ->
        Column(
            modifier = Modifier
                .padding(padding)
                .padding(16.dp)
                .fillMaxSize(),
            verticalArrangement = Arrangement.Center
        ) {
            Button(
                onClick = onStart,
                modifier = Modifier.fillMaxWidth()
            ) {
                Text("Comenzar a escuchar")
            }
        }
    }
}
```

---

### 4.4 UI: ListeningScreen (animación simple + palabras en vivo)
`presentation/listening/ListeningScreen.kt`
```kotlin
package com.rextrem.anotador.presentation.listening

import androidx.compose.animation.core.*
import androidx.compose.foundation.layout.*
import androidx.compose.foundation.lazy.LazyColumn
import androidx.compose.foundation.lazy.items
import androidx.compose.material3.*
import androidx.compose.runtime.*
import androidx.compose.ui.Modifier
import androidx.compose.ui.draw.scale
import androidx.compose.ui.unit.dp

@Composable
fun ListeningScreen(
    viewModel: ListeningViewModel,
    onBack: () -> Unit
) {
    val state by viewModel.uiState.collectAsState()

    // Animación tipo “pulso” simulando micrófono/telefono escuchando
    val infiniteTransition = rememberInfiniteTransition(label = "pulse")
    val scale by infiniteTransition.animateFloat(
        initialValue = 1.0f,
        targetValue = 1.15f,
        animationSpec = infiniteRepeatable(
            animation = tween(600, easing = FastOutSlowInEasing),
            repeatMode = RepeatMode.Reverse
        ),
        label = "scale"
    )

    Scaffold(
        topBar = {
            TopAppBar(
                title = { Text("Escuchando") },
                navigationIcon = { TextButton(onClick = onBack) { Text("Atrás") } },
                actions = {
                    if (state.isListening) {
                        TextButton(onClick = viewModel::stop) { Text("Detener") }
                    } else {
                        TextButton(onClick = viewModel::start) { Text("Iniciar") }
                    }
                }
            )
        }
    ) { padding ->
        Column(
            modifier = Modifier
                .padding(padding)
                .padding(16.dp)
                .fillMaxSize(),
            verticalArrangement = Arrangement.spacedBy(12.dp)
        ) {
            Card(Modifier.fillMaxWidth()) {
                Column(Modifier.padding(16.dp)) {
                    Text(
                        text = if (state.isListening) "Escuchando..." else "Detenido",
                        style = MaterialTheme.typography.titleMedium
                    )
                    Spacer(Modifier.height(8.dp))

                    // “Icono” simple animado
                    Surface(
                        modifier = Modifier
                            .scale(if (state.isListening) scale else 1f),
                        tonalElevation = 6.dp,
                        shape = MaterialTheme.shapes.large
                    ) {
                        Text(
                            text = "🎙", // si no quieres emoji, cámbialo por "MIC"
                            modifier = Modifier.padding(horizontal = 24.dp, vertical = 12.dp)
                        )
                    }

                    state.errorCode?.let { code ->
                        Spacer(Modifier.height(8.dp))
                        Text("Error: $code", color = MaterialTheme.colorScheme.error)
                    }

                    Spacer(Modifier.height(8.dp))
                    Text("Parcial: ${state.partialText}")
                }
            }

            Text("Palabras detectadas (aprox):")
            LazyColumn(
                modifier = Modifier.fillMaxSize(),
                verticalArrangement = Arrangement.spacedBy(6.dp)
            ) {
                items(state.words) { w ->
                    Text("- $w")
                }
            }
        }
    }
}
```

> Nota: puse “🎙” solo como placeholder. Si prefieres 100% serio, cámbialo por texto o un Icon de Material.

---

### 4.5 Navegación + creación de ViewModel
`navigation/NavGraph.kt`
```kotlin
package com.rextrem.anotador.navigation

import android.content.Context
import androidx.compose.runtime.Composable
import androidx.compose.ui.platform.LocalContext
import androidx.lifecycle.ViewModel
import androidx.lifecycle.ViewModelProvider
import androidx.lifecycle.viewmodel.compose.viewModel
import androidx.navigation.NavHostController
import androidx.navigation.compose.NavHost
import androidx.navigation.compose.composable
import com.rextrem.anotador.presentation.home.HomeScreen
import com.rextrem.anotador.presentation.listening.ListeningScreen
import com.rextrem.anotador.presentation.listening.ListeningViewModel
import com.rextrem.anotador.speech.SpeechRecognizerManager

object Routes {
    const val HOME = "home"
    const val LISTENING = "listening"
}

@Composable
fun NavGraph(navController: NavHostController) {
    NavHost(navController = navController, startDestination = Routes.HOME) {
        composable(Routes.HOME) {
            HomeScreen(
                onStart = { navController.navigate(Routes.LISTENING) }
            )
        }
        composable(Routes.LISTENING) {
            val context = LocalContext.current
            val vm: ListeningViewModel = viewModel(factory = ListeningVmFactory(context))
            ListeningScreen(
                viewModel = vm,
                onBack = { navController.popBackStack() }
            )
        }
    }
}

private class ListeningVmFactory(private val context: Context) : ViewModelProvider.Factory {
    override fun <T : ViewModel> create(modelClass: Class<T>): T {
        val speech = SpeechRecognizerManager(context.applicationContext)
        @Suppress("UNCHECKED_CAST")
        return ListeningViewModel(speech) as T
    }
}
```

---

### 4.6 MainActivity: pide permiso y muestra el NavGraph
`MainActivity.kt`
```kotlin
package com.rextrem.anotador

import android.Manifest
import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.activity.result.contract.ActivityResultContracts
import androidx.compose.material3.AlertDialog
import androidx.compose.material3.Text
import androidx.compose.material3.TextButton
import androidx.compose.runtime.*
import androidx.navigation.compose.rememberNavController
import com.rextrem.anotador.navigation.NavGraph
import com.rextrem.anotador.ui.theme.AnotadorTheme

class MainActivity : ComponentActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        val requestPermission = registerForActivityResult(
            ActivityResultContracts.RequestPermission()
        ) { /* resultado */ }

        setContent {
            AnotadorTheme {
                var showPermissionDialog by remember { mutableStateOf(true) }

                if (showPermissionDialog) {
                    AlertDialog(
                        onDismissRequest = { showPermissionDialog = false },
                        title = { Text("Permiso de micrófono") },
                        text = { Text("Necesitas permitir el micrófono para usar voz a texto.") },
                        confirmButton = {
                            TextButton(onClick = {
                                requestPermission.launch(Manifest.permission.RECORD_AUDIO)
                                showPermissionDialog = false
                            }) { Text("Permitir") }
                        },
                        dismissButton = {
                            TextButton(onClick = { showPermissionDialog = false }) { Text("Ahora no") }
                        }
                    )
                }

                val navController = rememberNavController()
                NavGraph(navController)
            }
        }
    }
}
```

---

## 5) Para “realtime continuo” (siguiente mejora)
`SpeechRecognizer` muchas veces se detiene con `onEndOfSpeech()` y entrega `onResults()`. Para hacerlo “continuo” se suele:
- al recibir `Final` o `Error`, **reiniciar** `startListening()` automáticamente
- manejar errores típicos (7 = no match, 6 = speech timeout, etc.)

Si me confirmas si lo quieres **continuo sin parar** (tipo dictado infinito), te paso el patrón robusto de “auto-restart” y manejo de AudioFocus.

---

## Preguntas para afinar (importan mucho)
1) ¿Debe funcionar **sin Internet** o te sirve depender de Google?  
2)