### 1) De MVC (Java) a MVVM (Compose): mapeo mental rápido

Si vienes de un MVC típico en backend Java con **Controllers + Services + Repositories + DTOs**, en Android con Jetpack Compose el equivalente práctico suele verse así:

| MVC (Java) | MVVM (Compose) | Rol |
|---|---|---|
| View (JSP/Thymeleaf/Front) | **Composable(s)** | Renderiza UI en función del estado |
| Controller | **ViewModel** | Orquesta acciones de UI, valida, llama casos de uso/repos, expone estado |
| Service | **UseCase / Interactor (opcional)** | Reglas de negocio (útil cuando crece) |
| Repository | **Repository** | Abstracción de datos (network/db/cache) |
| DTOs | **DTOs** + **Mappers** | Estructuras de red/DB, se transforman a modelos de dominio/UI |
| Model | **Domain models** | Modelos limpios para negocio/UI |

En Compose (MVVM) la clave es el **flujo unidireccional (UDF)**:
1. La **UI** emite eventos (click, refresh, input).
2. El **ViewModel** procesa el evento, llama repos/usecases.
3. El **ViewModel** actualiza un **estado observable**.
4. Compose “recompone” la UI automáticamente cuando cambia el estado.

---

### 2) Qué cambia con Jetpack Compose (vs “View” tradicional)

- No hay XML: la UI son funciones `@Composable`.
- La UI debe ser una **función pura del estado**: `UI = f(state)`.
- El estado observable típico es `StateFlow` (o `LiveData`) desde el ViewModel.
- La UI **no** debería llamar a repos directamente (equivalente a no meter lógica en la vista).

---

### 3) Capas recomendadas para un MVP (mínimo viable)

Para un MVP móvil “bien armado” pero sin sobre-ingeniería:

**UI (Compose)**
- `Screen` / `Route` (conecta ViewModel con UI)
- `Composable` puros (solo pintan)

**Presentation**
- `ViewModel`
- `UiState` (estado)
- `UiEvent` (eventos de UI, opcional pero recomendable)

**Data**
- `Repository` (interface)
- `RepositoryImpl`
- `RemoteDataSource` (Retrofit) / `LocalDataSource` (Room) según aplique
- `DTO` + `Mapper`

**Domain (opcional en MVP, útil si crece)**
- `UseCase` (casos de uso)

---

### 4) Ejemplo end-to-end simple (Lista de “Productos”)

#### 4.1 DTO (red) y modelo de dominio

```kotlin
data class ProductDto(
    val id: String,
    val title: String,
    val price: Double
)

data class Product(
    val id: String,
    val name: String,
    val price: Double
)

// Mapper (DTO -> Domain)
fun ProductDto.toDomain(): Product = Product(
    id = id,
    name = title,
    price = price
)
````

#### 4.2 API + Repository

```kotlin
import retrofit2.http.GET

interface ProductApi {
    @GET("products")
    suspend fun getProducts(): List<ProductDto>
}

interface ProductRepository {
    suspend fun fetchProducts(): List<Product>
}

class ProductRepositoryImpl(
    private val api: ProductApi
) : ProductRepository {

    override suspend fun fetchProducts(): List<Product> {
        return api.getProducts().map { it.toDomain() }
    }
}
````

> Equivalencia Java:
> - `ProductApi` sería como tu “client/service HTTP”
> - `ProductRepository` como tu repositorio
> - `ProductRepositoryImpl` como implementación concreta (inyección de dependencias)

#### 4.3 UiState (estado) + ViewModel

```kotlin
import androidx.lifecycle.ViewModel
import androidx.lifecycle.viewModelScope
import kotlinx.coroutines.flow.MutableStateFlow
import kotlinx.coroutines.flow.StateFlow
import kotlinx.coroutines.flow.update
import kotlinx.coroutines.launch

data class ProductListUiState(
    val isLoading: Boolean = false,
    val items: List<Product> = emptyList(),
    val errorMessage: String? = null
)

class ProductListViewModel(
    private val repository: ProductRepository
) : ViewModel() {

    private val _uiState = MutableStateFlow(ProductListUiState())
    val uiState: StateFlow<ProductListUiState> = _uiState

    fun load() {
        viewModelScope.launch {
            _uiState.update { it.copy(isLoading = true, errorMessage = null) }
            try {
                val products = repository.fetchProducts()
                _uiState.update { it.copy(isLoading = false, items = products) }
            } catch (e: Exception) {
                _uiState.update {
                    it.copy(isLoading = false, errorMessage = e.message ?: "Error desconocido")
                }
            }
        }
    }
}
````

**Qué hace el ViewModel aquí (equivalente a “Controller + parte de Service”):**
- Maneja el “caso” `load()`
- Llama al repositorio
- Publica estado (loading/datos/error)

#### 4.4 UI en Compose (Screen)

```kotlin
import androidx.compose.foundation.layout.*
import androidx.compose.foundation.lazy.LazyColumn
import androidx.compose.foundation.lazy.items
import androidx.compose.material3.*
import androidx.compose.runtime.*
import androidx.compose.ui.Modifier
import androidx.compose.ui.unit.dp
import kotlinx.coroutines.flow.collectAsState

@Composable
fun ProductListRoute(viewModel: ProductListViewModel) {
    val state by viewModel.uiState.collectAsState()

    // Carga inicial (simple para MVP)
    LaunchedEffect(Unit) {
        viewModel.load()
    }

    ProductListScreen(
        state = state,
        onRetry = { viewModel.load() }
    )
}

@Composable
fun ProductListScreen(
    state: ProductListUiState,
    onRetry: () -> Unit
) {
    when {
        state.isLoading -> {
            Box(Modifier.fillMaxSize(), contentAlignment = androidx.compose.ui.Alignment.Center) {
                CircularProgressIndicator()
            }
        }

        state.errorMessage != null -> {
            Column(Modifier.padding(16.dp)) {
                Text("Error: ${state.errorMessage}", color = MaterialTheme.colorScheme.error)
                Spacer(Modifier.height(12.dp))
                Button(onClick = onRetry) { Text("Reintentar") }
            }
        }

        else -> {
            LazyColumn(contentPadding = PaddingValues(16.dp)) {
                items(state.items) { product ->
                    Text("${product.name} - $${product.price}")
                    Spacer(Modifier.height(8.dp))
                }
            }
        }
    }
}
````

**Puntos clave:**
- La UI **no** sabe de Retrofit, DTOs, etc.
- La UI reacciona solo a `state`.
- `Route` conecta ViewModel con `Screen` (patrón común en Compose).

---

### 5) Cómo encajan “Services” en MVVM (si los quieres mantener)

En Android moderno, el “Service” como capa (similar a backend) suele transformarse en:

- **UseCases**: `GetProductsUseCase`, `CreateOrderUseCase`, etc.
- O una capa `DomainService` si hay reglas complejas (cálculos, validaciones, composición de repos).

Ejemplo rápido (opcional):

```kotlin
class GetProductsUseCase(
    private val repository: ProductRepository
) {
    suspend operator fun invoke(): List<Product> = repository.fetchProducts()
}
````

Luego el ViewModel llama al use case en vez del repositorio directo.

---

### 6) Recomendaciones prácticas para un MVP real

- **StateFlow + UiState** (como arriba): simple y robusto.
- **Mappers** entre DTO ↔ Domain: evita acoplar UI a red.
- **Inyección de dependencias**: Hilt/Koin (para MVP Hilt es estándar).
- **Errores y loading** desde el ViewModel, no desde la UI.
- Si usarás navegación: `Navigation Compose` y separar `Route`/`Screen`.

---

### 7) Preguntas para ajustar a tu caso (y darte un esqueleto exacto)

1) ¿Tu MVP consumirá **API REST**, **base local (Room)** o ambos?  
2) ¿Necesitas login/token (JWT/OAuth) y manejo de sesión?  
3) ¿Prefieres arquitectura “simple” (UI + ViewModel + Repository) o con **UseCases** desde el día 1?

Si me respondes eso, te armo una estructura de paquetes y un “template” completo (con Hilt + Retrofit + estados + pantalla) listo para arrancar el MVP.


---

###  Stack: **Android nativo (Kotlin) + Jetpack**

- **UI**: Jetpack Compose (o Views si ya lo manejas).
- **Concurrencia**: Coroutines + Flow.
- **Audio**:
    
    - `AudioRecord` (bien para muchos casos),
    - y si necesitas **muy baja latencia**: **AAudio** vía **Oboe (C++)**.
    
- **Reconocimiento de voz (ASR)** (depende de si puedes usar red o no):
    
    - **Online (fácil, rápido de integrar)**: `SpeechRecognizer` de Android (parciales/streaming).
    - **Offline / control total / timestamps por palabra**: motor integrado tipo **Vosk** o **Whisper** (ej. `whisper.cpp` con JNI). Esto te da más control, pero requiere más trabajo y optimización.

