## 1) MVVM explicado “para gente de Spring MVC”

### MVVM (Android)
- **View (Vista)**: la UI (en Compose: `@Composable`).  
  Solo renderiza estado y manda eventos (clicks, textos).
- **ViewModel**: mantiene el **estado** de la pantalla y expone **acciones** (intents).  
  Es lo más parecido a un `@Controller` + “glue code” de UI.
- **Model**: los datos (entities) + repositorios + casos de uso.

### Comparación mental con Spring
| Spring MVC | Android MVVM (Compose) | Nota |
|---|---|---|
| `@Controller` | `ViewModel` (y/o capa de eventos de UI) | El ViewModel recibe eventos de UI |
| `@Service` | `UseCase` / “Interactor” (opcional) | Reglas de negocio |
| `@Repository` | `Repository` (data layer) | Fuente de datos (Room/Retrofit/etc.) |
| `Model`/DTO | `data class` | Modelos de dominio/datos |
| `View` (Thymeleaf) | `@Composable` | UI reactiva (se recompone con estado) |

**Idea clave**: en Compose la UI “observa” estado. Cuando el estado cambia, la UI se re-dibuja sola.

---

## 2) Estructura de carpetas recomendada (tipo “Spring ordenado”)

Dentro de: `app/src/main/java/com/rextrem/anotador/`

Una estructura práctica:

```
com.rextrem.anotador
├── App.kt (opcional)
├── MainActivity.kt
├── data
│   ├── model
│   │   └── Note.kt
│   └── repository
│       ├── NoteRepository.kt
│       └── InMemoryNoteRepository.kt   (luego lo cambias por Room)
├── presentation
│   ├── navigation
│   │   └── NavGraph.kt
│   ├── notes_list
│   │   ├── NotesListScreen.kt
│   │   └── NotesListViewModel.kt
│   └── note_create
│       ├── NoteCreateScreen.kt
│       └── NoteCreateViewModel.kt
└── ui
    └── theme
        ├── Color.kt
        ├── Theme.kt
        └── Type.kt
```

Esto escala bien cuando metas Room, servicios, etc.

---

## 3) Dependencias mínimas (para 2 pantallas + ViewModel)

En `build.gradle (Module: app)` agrega (si no están):

```gradle
dependencies {
    implementation "androidx.lifecycle:lifecycle-viewmodel-compose:2.8.7"
    implementation "androidx.navigation:navigation-compose:2.8.7"
}
```

*(Versiones pueden variar según tu BOM; ajústalo a tu proyecto.)*

---

## 4) Ejemplo completo: 2 “vistas” (pantallas) funcionales

### 4.1 Modelo
`data/model/Note.kt`
```kotlin
package com.rextrem.anotador.data.model

data class Note(
    val id: Long,
    val text: String
)
```

### 4.2 Repositorio (temporal en memoria)
`data/repository/NoteRepository.kt`
```kotlin
package com.rextrem.anotador.data.repository

import com.rextrem.anotador.data.model.Note
import kotlinx.coroutines.flow.Flow

interface NoteRepository {
    fun observeNotes(): Flow<List<Note>>
    suspend fun addNote(text: String)
}
```

`data/repository/InMemoryNoteRepository.kt`
```kotlin
package com.rextrem.anotador.data.repository

import com.rextrem.anotador.data.model.Note
import kotlinx.coroutines.flow.Flow
import kotlinx.coroutines.flow.MutableStateFlow
import kotlinx.coroutines.flow.asStateFlow

class InMemoryNoteRepository : NoteRepository {

    private val notes = MutableStateFlow<List<Note>>(emptyList())
    private var nextId = 1L

    override fun observeNotes(): Flow<List<Note>> = notes.asStateFlow()

    override suspend fun addNote(text: String) {
        val trimmed = text.trim()
        if (trimmed.isEmpty()) return

        val newNote = Note(id = nextId++, text = trimmed)
        notes.value = listOf(newNote) + notes.value
    }
}
```

> Luego cambias `InMemoryNoteRepository` por Room sin tocar casi nada de UI.

---

## 4.3 ViewModels (equivalente a “Controller” por pantalla)

`presentation/notes_list/NotesListViewModel.kt`
```kotlin
package com.rextrem.anotador.presentation.notes_list

import androidx.lifecycle.ViewModel
import androidx.lifecycle.viewModelScope
import com.rextrem.anotador.data.model.Note
import com.rextrem.anotador.data.repository.NoteRepository
import kotlinx.coroutines.flow.SharingStarted
import kotlinx.coroutines.flow.StateFlow
import kotlinx.coroutines.flow.stateIn

class NotesListViewModel(
    repository: NoteRepository
) : ViewModel() {

    val notes: StateFlow<List<Note>> =
        repository.observeNotes()
            .stateIn(viewModelScope, SharingStarted.WhileSubscribed(5_000), emptyList())
}
```

`presentation/note_create/NoteCreateViewModel.kt`
```kotlin
package com.rextrem.anotador.presentation.note_create

import androidx.lifecycle.ViewModel
import androidx.lifecycle.viewModelScope
import com.rextrem.anotador.data.repository.NoteRepository
import kotlinx.coroutines.flow.MutableStateFlow
import kotlinx.coroutines.flow.StateFlow
import kotlinx.coroutines.launch

class NoteCreateViewModel(
    private val repository: NoteRepository
) : ViewModel() {

    private val _text = MutableStateFlow("")
    val text: StateFlow<String> = _text

    fun onTextChange(value: String) {
        _text.value = value
    }

    fun save(onSaved: () -> Unit) {
        viewModelScope.launch {
            repository.addNote(_text.value)
            _text.value = ""
            onSaved()
        }
    }
}
```

---

## 4.4 Screens (las “Views”)

`presentation/notes_list/NotesListScreen.kt`
```kotlin
package com.rextrem.anotador.presentation.notes_list

import androidx.compose.foundation.clickable
import androidx.compose.foundation.layout.*
import androidx.compose.foundation.lazy.LazyColumn
import androidx.compose.foundation.lazy.items
import androidx.compose.material3.*
import androidx.compose.runtime.*
import androidx.compose.ui.Modifier
import androidx.compose.ui.unit.dp

@Composable
fun NotesListScreen(
    viewModel: NotesListViewModel,
    onAddClick: () -> Unit
) {
    val notes by viewModel.notes.collectAsState()

    Scaffold(
        topBar = { TopAppBar(title = { Text("Anotador") }) },
        floatingActionButton = {
            FloatingActionButton(onClick = onAddClick) {
                Text("+")
            }
        }
    ) { padding ->
        if (notes.isEmpty()) {
            Box(Modifier.padding(padding).fillMaxSize()) {
                Text(
                    text = "Sin notas todavía",
                    modifier = Modifier.padding(16.dp)
                )
            }
        } else {
            LazyColumn(
                modifier = Modifier.padding(padding).fillMaxSize(),
                contentPadding = PaddingValues(16.dp),
                verticalArrangement = Arrangement.spacedBy(8.dp)
            ) {
                items(notes) { note ->
                    Card(
                        modifier = Modifier.fillMaxWidth()
                    ) {
                        Text(
                            text = note.text,
                            modifier = Modifier.padding(16.dp)
                        )
                    }
                }
            }
        }
    }
}
```

`presentation/note_create/NoteCreateScreen.kt`
```kotlin
package com.rextrem.anotador.presentation.note_create

import androidx.compose.foundation.layout.*
import androidx.compose.material3.*
import androidx.compose.runtime.*
import androidx.compose.ui.Modifier
import androidx.compose.ui.unit.dp

@Composable
fun NoteCreateScreen(
    viewModel: NoteCreateViewModel,
    onBack: () -> Unit
) {
    val text by viewModel.text.collectAsState()

    Scaffold(
        topBar = {
            TopAppBar(
                title = { Text("Nueva nota") },
                navigationIcon = {
                    TextButton(onClick = onBack) { Text("Atrás") }
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
            OutlinedTextField(
                value = text,
                onValueChange = viewModel::onTextChange,
                modifier = Modifier.fillMaxWidth(),
                label = { Text("Escribe tu nota") }
            )

            Button(
                onClick = { viewModel.save(onSaved = onBack) },
                modifier = Modifier.fillMaxWidth(),
                enabled = text.isNotBlank()
            ) {
                Text("Guardar")
            }
        }
    }
}
```

---

## 4.5 Navegación (como “rutas”)
`presentation/navigation/NavGraph.kt`
```kotlin
package com.rextrem.anotador.presentation.navigation

import androidx.compose.runtime.Composable
import androidx.lifecycle.viewmodel.compose.viewModel
import androidx.navigation.NavHostController
import androidx.navigation.compose.NavHost
import androidx.navigation.compose.composable
import com.rextrem.anotador.data.repository.NoteRepository
import com.rextrem.anotador.presentation.note_create.NoteCreateScreen
import com.rextrem.anotador.presentation.note_create.NoteCreateViewModel
import com.rextrem.anotador.presentation.notes_list.NotesListScreen
import com.rextrem.anotador.presentation.notes_list.NotesListViewModel

object Routes {
    const val LIST = "list"
    const val CREATE = "create"
}

@Composable
fun NavGraph(
    navController: NavHostController,
    repository: NoteRepository
) {
    NavHost(navController = navController, startDestination = Routes.LIST) {
        composable(Routes.LIST) {
            val vm = viewModel<NotesListViewModel>(factory = SimpleVmFactory { NotesListViewModel(repository) })
            NotesListScreen(
                viewModel = vm,
                onAddClick = { navController.navigate(Routes.CREATE) }
            )
        }
        composable(Routes.CREATE) {
            val vm = viewModel<NoteCreateViewModel>(factory = SimpleVmFactory { NoteCreateViewModel(repository) })
            NoteCreateScreen(
                viewModel = vm,
                onBack = { navController.popBackStack() }
            )
        }
    }
}
```

Y un factory simple (sin DI todavía):
```kotlin
package com.rextrem.anotador.presentation.navigation

import androidx.lifecycle.ViewModel
import androidx.lifecycle.ViewModelProvider

class SimpleVmFactory<T : ViewModel>(
    private val creator: () -> T
) : ViewModelProvider.Factory {
    override fun <VM : ViewModel> create(modelClass: Class<VM>): VM {
        @Suppress("UNCHECKED_CAST")
        return creator() as VM
    }
}
```

---

## 4.6 MainActivity
`MainActivity.kt` (en `com.rextrem.anotador`)
```kotlin
package com.rextrem.anotador

import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.navigation.compose.rememberNavController
import com.rextrem.anotador.data.repository.InMemoryNoteRepository
import com.rextrem.anotador.presentation.navigation.NavGraph
import com.rextrem.anotador.ui.theme.AnotadorTheme

class MainActivity : ComponentActivity() {

    // Para demo. En producción: DI (Hilt/Koin) + singleton apropiado
    private val repository = InMemoryNoteRepository()

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            AnotadorTheme {
                val navController = rememberNavController()
                NavGraph(navController = navController, repository = repository)
            }
        }
    }
}
```

---

## 5) Cómo pensar “agregar 2 vistas con funcionalidades”
Cuando digas “necesito 2 vistas”, en MVVM normalmente haces:
1) **Un package por pantalla** (`presentation/<feature>/`)
2) Dentro:
   - `Screen` (UI)
   - `ViewModel` (estado + acciones)
   - (Opcional) `UiState` + `UiEvent`
3) Si comparten datos: `Repository` (como Spring Repository) y/o `UseCases` (como Spring Service).

---

## Pregunta para ajustarlo a tu caso real
¿Cuáles son exactamente tus “2 vistas” y su funcionalidad? (ej: “escuchar micrófono y mostrar palabras” + “historial de palabras”, o “configuración de sensibilidad”, etc.).  
Si me dices eso, te doy la estructura final por features (y si conviene 1 ViewModel compartido o separados, y cómo modelar estados/eventos).