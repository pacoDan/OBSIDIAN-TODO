
#1 — ANÁLISIS DE DEMANDA Y POPULARIDAD POR TAGS/CATEGORÍAS
Necesidad identificada
La organización necesita saber qué libros circulan más, en qué zonas, por qué perfiles de usuario y en qué épocas, para tomar decisiones estratégicas sobre qué libros incorporar o promover.

┌─────────────────────────────────────────────────────────┐
│              SISTEMA DE TAGS Y CATEGORÍAS               │
│                                                         │
│  Obra                                                   │
│  ├── categoria: (Ficción, Ciencia, Historia, etc.)      │
│  ├── subcategoria: (Novela, Cuento, Ensayo, etc.)       │
│  ├── tags: [#clasico, #juvenil, #premiado, #local]      │
│  ├── nivel_lectura: (Básico, Intermedio, Avanzado)      │
│  └── idioma: (Español, Inglés, etc.)                    │
│                                                         │
│  Métricas calculadas por obra/tag:                      │
│  ├── cantidad_prestamos_totales                         │
│  ├── cantidad_prestamos_ultimo_mes                      │
│  ├── promedio_dias_en_prestamo                          │
│  ├── cantidad_usuarios_distintos_que_lo_leyeron         │
│  └── longitud_promedio_cadena_prestamos                 │
└─────────────────────────────────────────────────────────┘

"Similar al Resumen Estadístico de "Mis Gastos" y al Módulo de Indicadores (V) del Sistema ISO — ambos calculan métricas agregadas sobre datos históricos"

Operaciones ──► Cola de eventos ──► Job nocturno ──► DB Analytics
                                    (Cron Task)       (desnormalizada
                                                       para reportes)

#2 — VALIDACIÓN DEL ESTADO FÍSICO DEL LIBRO POR IA
Necesidad identificada
Antes de registrar un préstamo o al momento de una devolución, es necesario verificar el estado físico del ejemplar para detectar daños, deterioro o pérdida de páginas. Esto protege a los usuarios y a la organización.
┌─────────────────────────────────────────────────────────┐
│           VALIDACIÓN POR IA - FLUJO COMPLETO            │
│                                                         │
│  1. Usuario toma foto del ejemplar                      │
│           │                                             │
│           ▼                                             │
│  2. Sistema envía imagen a API de IA externa            │
│           │                                             │
│           ▼                                             │
│  3. IA analiza y devuelve:                              │
│     {                                                   │
│       "estado": "DETERIORADO",                          │
│       "confianza": 0.91,                                │
│       "daños_detectados": ["tapa rota", "páginas        │
│                             manchadas"],                │
│       "porcentaje_deterioro": 35                        │
│     }                                                   │
│           │                                             │
│  4. Si confianza > 85% Y daño detectado:                │
│     → Ejemplar marcado como "SOSPECHOSO"                │
│     → Operador humano debe revisar                      │
│           │                                             │
│  5. Operador confirma o descarta la alerta              │
└─────────────────────────────────────────────────────────┘

Diagrama de estados:
DISPONIBLE ──prestar()──► PRESTADO
     │                        │
     │                    devolver()
     │                        │
     │              ┌─────────▼──────────┐
     │              │  VALIDACION_IA     │
     │              │  (foto requerida)  │
     │              └─────────┬──────────┘
     │                        │
     │              IA OK ◄───┴───► IA detecta daño
     │                │                    │
     └────────────────┘            SOSPECHOSO
                                        │
                              Operador revisa
                              │              │
                         Confirma OK    Confirma daño
                              │              │
                         DISPONIBLE    DADO_DE_BAJA

"Idéntico al Servicio III de ProtegePro ("Validación Inteligente"): "Si la IA detecta una coincidencia de daño con una confianza mayor al 85%, la solicitud se marca como Sospechosa""


#3 — TRAZABILIDAD COMPLETA DE LA CADENA DE PRÉSTAMOS
Necesidad identificada
La organización necesita saber en todo momento dónde está cada ejemplar, quién lo tiene, cuánto tiempo lleva en cada mano y cuál es el historial completo desde que se incorporó al sistema.

"Similar a la trazabilidad de estados de ProtegePro ("bitácora completa"), al historial de pólizas de SafeDrive y a la trazabilidad de donaciones en el sistema de ONG (Final 20250925)"

#4 — PERFIL LECTOR Y RECOMENDACIONES PERSONALIZADAS
Necesidad identificada
La organización quiere fomentar la lectura activa recomendando libros según el historial, preferencias y perfil de cada usuario, similar a como lo hacen plataformas modernas.

┌─────────────────────────────────────────────────────────┐
│              PERFIL LECTOR DEL USUARIO                  │
│                                                         │
│  Usuario: Carlos Pérez                                  │
│  ├── Libros leídos: 23                                  │
│  ├── Géneros favoritos: [Ficción, Historia]             │
│  ├── Tags más frecuentes: [#clasico, #latinoamerica]    │
│  ├── Promedio días por libro: 12                        │
│  ├── Libros prestados a otros: 8                        │
│  ├── Libros recibidos en préstamo: 15                   │
│  └── Nivel lector: INTERMEDIO                           │
│                                                         │
│  Recomendaciones generadas:                             │
│  ├── Por historial propio                               │
│  ├── Por lo que leen usuarios similares                 │
│  └── Por libros disponibles en su red de contactos      │
└─────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────┐
│           CRITERIOS DE RECOMENDACIÓN (Strategy)         │
│                                                         │
│  Criterio 1: Por afinidad de tags                       │
│  → Si leyó 3 libros con #clasico, recomendar más        │
│                                                         │
│  Criterio 2: Por red social de préstamos                │
│  → Libros que leyeron personas que me prestaron         │
│                                                         │
│  Criterio 3: Por disponibilidad cercana                 │
│  → Libros disponibles en mi zona geográfica             │
│                                                         │
│  Criterio 4: Por tendencia general                      │
│  → Los más prestados del último mes en mi categoría     │
└─────────────────────────────────────────────────────────┘


"Similar al Recomendador de TalentHub, al sistema de recomendación de EducAR+ y a los mensajes motivacionales de HealthMe generados por IA generativa"


 #5 — SISTEMA DE NOTIFICACIONES Y ENGAGEMENT
Necesidad identificada
Para que la circulación de libros sea efectiva, la organización necesita mantener activos a los usuarios, recordarles devoluciones, notificarles préstamos recibidos y motivarlos a seguir participando.

┌─────────────────────────────────────────────────────────┐
│           EVENTOS QUE DISPARAN NOTIFICACIONES           │
│                                                         │
│  INMEDIATAS (sincrónicas):                              │
│  ├── Alguien te prestó un libro                         │
│  ├── Te cedieron la propiedad de un libro               │
│  ├── Tu libro fue dado de baja (por daño)               │
│  └── Tu solicitud de préstamo fue aceptada/rechazada    │
│                                                         │
│  PROGRAMADAS (Cron Jobs):                               │
│  ├── Recordatorio: tu préstamo vence en 3 días          │
│  ├── Tu libro lleva 30 días sin volver                  │
│  ├── Recomendación semanal de libros                    │
│  └── Resumen mensual de tu actividad lectora            │
│                                                         │
│  BASADAS EN EVENTOS DE IA:                              │
│  ├── Se detectó daño en tu libro (foto analizada)       │
│

┌─────────────────────────────────────────────────────────────┐
│                    FUENTES DE EVENTOS                       │
│                                                             │
│  Servicio II          Servicio III         Cron Jobs        │
│  (Operaciones)        (Trazabilidad)       (Scheduler)      │
│       │                    │                   │            │
└───────┼────────────────────┼───────────────────┼────────────┘
        │                    │                   │
        └────────────────────┴───────────────────┘
                             │
                             ▼
                    ┌─────────────────┐
                    │  Cola de        │
                    │  Mensajes       │
                    │  (RabbitMQ/SQS) │
                    └────────┬────────┘
                             │
                             ▼
                    ┌─────────────────┐
                    │  Servicio IV    │
                    │  Notificaciones │
                    │  (Worker)       │
                    └────────┬────────┘
                             │
              ┌──────────────┼──────────────┐
              │              │              │
              ▼              ▼              ▼
         ┌────────┐    ┌──────────┐   ┌──────────┐
         │ Email  │    │WhatsApp  │   │  Push    │
         │(SMTP / │    │(Twilio / │   │Notif.    │
         │SendGrid│    │ Meta API)│   │(Firebase)│
         └────────┘    └──────────┘   └──────────┘



┌──────────────────────────────────────────────────────────┐
│          RESUMEN DE ENERO - Carlos Pérez                 │
│                                                          │
│  📖 Este mes leíste:        3 libros                     │
│  🤝 Prestaste a otros:      2 libros                     │
│  📬 Recibiste en préstamo:  1 libro                      │
│  🔗 Tu libro más viajero:   "El Principito"              │
│     └── Pasó por 4 manos este mes                        │
│                                                          │
│  📊 Tu impacto social:                                   │
│     └── Contribuiste a 6 lecturas en tu comunidad        │
│                                                          │
│  💡 Recomendación para febrero:                          │
│     "Basado en tu historial, te puede gustar             │
│      'Rayuela' de Cortázar"                              │
│                                                          │
│  🏆 Logro desbloqueado: PROMOTOR LECTOR                  │
└──────────────────────────────────────────────────────────┘

"Referencia en exámenes anteriores: HealthMe Servicio V → notificaciones push diarias + IA generativa Mi Amigo Invisible → engagement post-evento con recordatorios EasyTech → notificaciones en cada cambio de estado de la orden"

---
	
### 1. Arquitectura de Notificaciones Asincrónica

Para garantizar la fluidez del sistema y evitar errores de **Time Out**, el envío de notificaciones no debe realizarse dentro del proceso principal de préstamo o devolución.

- **Componente de Notificaciones:** Se debe implementar un servicio desacoplado que consuma eventos de una **cola de mensajes** (RabbitMQ o Kafka). Cuando un libro cambia de manos (A $\rightarrow$ B), el servicio de préstamos deja un mensaje en la cola y el **Worker de Notificaciones** se encarga de enviarlo al usuario sin bloquear la aplicación.
- **Integración Multicanal:** Siguiendo el modelo de _EducAR+_ y _Mi Amis Invisible_, se deben utilizar **Adapters** para integrarse con servicios externos como **SendGrid** (Email) o **Twilio** (WhatsApp/SMS), permitiendo al usuario elegir su medio preferido.

### 2. Automatización de Recordatorios (Batch Processing)

Para la necesidad de "recordar devoluciones", el sistema requiere un proceso programado:

- **Jobs/CRON:** Implementar un componente de tareas programadas (similar a _DataCat-Jobs_ o _VideoTracker_) que se ejecute diariamente para identificar ejemplares cuya fecha de préstamo esté por vencer o vencida.
- **Lógica de Reintentos:** Si una notificación falla por problemas en el proveedor externo, se debe aplicar un patrón de **Retry** o persistir la notificación fallida para intentarlo más tarde, asegurando que el recordatorio llegue efectivamente.

### 3. Estrategias de Engagement y Motivación (IA Generativa)

Para "motivar a seguir participando", el sistema puede adoptar técnicas de personalización avanzada vistas en _HealthMe_ y _MES_:

- **Mensajes Motivacionales con IA:** Integrar una **IA Generativa** (OpenAI o Claude) que reciba el perfil del lector, sus géneros favoritos (basados en **tags** de los libros usados) y su historial de lecturas para generar mensajes personalizados. Por ejemplo: _"Hola, vimos que terminaste 'Cien años de soledad', ¿por qué no lo cedes a alguien más para que la magia continúe?"_.
- **Notificaciones por Inactividad:** Si un usuario no registra interacción (préstamos o búsquedas) por más de 20 días, el sistema debe disparar automáticamente un mensaje de incentivo para retomar la lectura.

### 4. Gamificación y Puntuación Social

Para mantener a los usuarios "activos y comprometidos", se pueden aplicar los conceptos de membresías y recompensas de _Caminantes CCA_:

- **Niveles de Lector:** Otorgar puntos por cada devolución a tiempo o cesión de propiedad realizada, permitiendo a los usuarios subir de categoría (Bronce, Plata, Oro).
- **Beneficios por Nivel:** Los usuarios de niveles superiores podrían tener acceso prioritario a "Obras" muy demandadas o habilitar funcionalidades especiales de recomendación.

### 5. Reducción de Fricción mediante SSO

Para facilitar que los usuarios se mantengan activos sin tener que recordar múltiples credenciales, es fundamental implementar un **SSO (Single Sign-On)** como **Auth0 o Google**. Esto permite un acceso rápido desde cualquier dispositivo (Web o Mobile), aumentando la probabilidad de que el usuario entre a la plataforma para registrar un movimiento de libro de forma inmediata.

¿Deseas que elabore un **diagrama de componentes** específico para este sistema de notificaciones o un **reporte** sobre cómo aplicar el patrón **State** para disparar estas alertas automáticamente?










---

# Documento de Requerimientos Funcionales
## Sistema de Circulación de Libros — Análisis Funcional Completo

**Versión:** 1.0 | **Equipo:** Analistas Funcionales | **Estado:** Borrador

---

# ÍNDICE

```
RF-01  Análisis de Demanda y Popularidad por Tags/Categorías
RF-02  Validación del Estado Físico del Libro por IA
RF-03  Trazabilidad Completa de la Cadena de Préstamos
RF-04  Perfil Lector y Recomendaciones Personalizadas
RF-05  Sistema de Notificaciones y Engagement Lector
```

---

# RF-01 — ANÁLISIS DE DEMANDA Y POPULARIDAD POR TAGS/CATEGORÍAS

## 1.1 Descripción General

| Campo | Detalle |
|-------|---------|
| **ID** | RF-01 |
| **Nombre** | Análisis de Demanda y Popularidad |
| **Prioridad** | Alta |
| **Módulo** | Estadísticas y Reportes |
| **Actor principal** | Administrador de la Organización |
| **Referencia** | "Mis Gastos" (Resumen Estadístico), DataCat (Métricas), Sistema ISO (Módulo de Indicadores) |

## 1.2 Necesidad Identificada

La organización necesita saber **qué libros circulan más**, en qué zonas, por qué perfiles de usuario y en qué épocas del año, para tomar decisiones estratégicas sobre:
- Qué títulos incorporar al inventario
- Qué libros promover activamente
- Dónde colocar más ejemplares físicamente
- Cómo medir el impacto social del proyecto

## 1.3 Problema sin este Requerimiento

```
❌ No saben qué géneros son más populares por zona
❌ No pueden justificar nuevas adquisiciones con datos
❌ No detectan libros que nadie lee (stock muerto)
❌ No pueden medir el impacto social del proyecto
❌ No identifican épocas de mayor/menor circulación
```

## 1.4 Modelo de Datos de Tags y Categorías

```
┌─────────────────────────────────────────────────────────┐
│              SISTEMA DE TAGS Y CATEGORÍAS               │
│                                                         │
│  Obra                                                   │
│  ├── categoria:     (Ficción, Ciencia, Historia, etc.)  │
│  ├── subcategoria:  (Novela, Cuento, Ensayo, etc.)      │
│  ├── tags:          [#clasico, #juvenil,                │
│  │                   #premiado, #local]                 │
│  ├── nivel_lectura: (Básico, Intermedio, Avanzado)      │
│  └── idioma:        (Español, Inglés, etc.)             │
│                                                         │
│  Métricas calculadas por obra/tag:                      │
│  ├── cantidad_prestamos_totales                         │
│  ├── cantidad_prestamos_ultimo_mes                      │
│  ├── promedio_dias_en_prestamo                          │
│  ├── cantidad_usuarios_distintos_que_lo_leyeron         │
│  └── longitud_promedio_cadena_prestamos                 │
└─────────────────────────────────────────────────────────┘
```

## 1.5 Dashboard de Demanda

```
┌──────────────────────────────────────────────────────┐
│              DASHBOARD DE DEMANDA                    │
│                                                      │
│  Top Tags del mes:                                   │
│  #juvenil      ████████████  142 préstamos  +23%    │
│  #clasico      █████████      98 préstamos   +5%    │
│  #premiado     ████████       87 préstamos   -2%    │
│                                                      │
│  Obra más prestada:    "Cien años de soledad"        │
│  Categoría más activa: Ficción (45% del total)       │
│  Cadena promedio:      3.2 eslabones por libro       │
│  Sin movimiento:       23 ejemplares > 90 días       │
└──────────────────────────────────────────────────────┘
```

## 1.6 Arquitectura del Componente

```
Operaciones
    │
    ▼
Cola de Eventos
    │
    ▼
Cron Job nocturno ──► DB Analytics (desnormalizada para reportes)
    │
    ▼
Dashboard Web (consultas de solo lectura)
```

> **Decisión arquitectónica:** El cálculo de métricas se realiza de forma
> **asincrónica** mediante un Job nocturno para no impactar la performance
> del sistema transaccional durante el día.

## 1.7 Endpoints del Servicio

```
GET /estadisticas/tags/ranking?periodo=mes
GET /estadisticas/obras/mas-prestadas?categoria=ficcion
GET /estadisticas/ejemplares/sin-movimiento?dias=90
GET /estadisticas/zonas/calor-lectura
GET /estadisticas/usuarios/perfil-agregado
```

## 1.8 Criterios de Aceptación

```
✅ El sistema calcula métricas por tag al menos 1 vez por día
✅ El dashboard muestra top 10 obras más prestadas del mes
✅ Se identifican ejemplares sin movimiento > 90 días
✅ Las métricas no impactan la performance transaccional
✅ Los reportes son exportables en formato CSV/PDF
```

---

# RF-02 — VALIDACIÓN DEL ESTADO FÍSICO DEL LIBRO POR IA

## 2.1 Descripción General

| Campo | Detalle |
|-------|---------|
| **ID** | RF-02 |
| **Nombre** | Validación por IA del Estado del Ejemplar |
| **Prioridad** | Alta |
| **Módulo** | Validación Inteligente |
| **Actor principal** | Usuario prestador / Usuario que devuelve |
| **Actor secundario** | Operador humano (revisión manual) |
| **Referencia** | ProtegePro Servicio III, ZonaPropi (moderación OpenAI) |

## 2.2 Necesidad Identificada

Antes de registrar un préstamo y al momento de una devolución, verificar el **estado físico del ejemplar** para:
- Detectar daños, deterioro o pérdida de páginas
- Proteger al prestador de responsabilidades injustas
- Decidir si el ejemplar debe darse de baja
- Generar evidencia objetiva ante conflictos entre usuarios

## 2.3 Problema sin este Requerimiento

```
❌ Un usuario devuelve un libro roto y nadie lo detecta
❌ Se presta un libro ya dañado y culpan al siguiente
❌ No hay evidencia objetiva del estado en cada operación
❌ Conflictos entre usuarios sin pruebas documentadas
❌ Ejemplares deteriorados siguen circulando
```

## 2.4 Flujo Completo de Validación

```
┌─────────────────────────────────────────────────────────┐
│                FLUJO DE VALIDACIÓN IA                   │
│                                                         │
│  1. Usuario toma foto del ejemplar                      │
│              │                                          │
│              ▼                                          │
│  2. Sistema envía imagen a API IA externa               │
│     (proceso ASINCRÓNICO - puede tardar > 1 min)        │
│              │                                          │
│              ▼                                          │
│  3. IA responde:                                        │
│     {                                                   │
│       "estado": "DETERIORADO",                          │
│       "confianza": 0.91,                                │
│       "daños_detectados": [                             │
│           "tapa rota",                                  │
│           "páginas manchadas"                           │
│       ],                                                │
│       "porcentaje_deterioro": 35                        │
│     }                                                   │
│              │                                          │
│  4. Confianza > 85% Y daño detectado?                   │
│     ├── SI → Ejemplar = SOSPECHOSO                      │
│     │         Operador humano debe revisar              │
│     └── NO → Operación continúa normalmente             │
│              │                                          │
│  5. Operador confirma o descarta la alerta              │
│     ├── Confirma OK   → DISPONIBLE                      │
│     └── Confirma daño → DADO_DE_BAJA                    │
└─────────────────────────────────────────────────────────┘
```

## 2.5 Diagrama de Estados del Ejemplar

```
DISPONIBLE ──prestar()──► PRESTADO
     │                        │
     │                    devolver()
     │                        │
     │              ┌─────────▼──────────┐
     │              │   VALIDACION_IA    │
     │              │  (foto requerida)  │
     │              └─────────┬──────────┘
     │                        │
     │              IA OK ◄───┴───► IA detecta daño
     │                │                    │
     └────────────────┘              SOSPECHOSO
                                          │
                                  Operador revisa
                                  │              │
                             Confirma OK    Confirma daño
                                  │              │
                             DISPONIBLE    DADO_DE_BAJA
```

## 2.6 Consideración Arquitectónica Clave

```
⚠️  PROBLEMA: La IA puede tardar más de 1 minuto en responder

SOLUCIÓN: Procesamiento ASINCRÓNICO

Usuario sube foto
      │
      ▼
Cola de mensajes (RabbitMQ / SQS)
      │
      ▼
Worker procesa IA en background
      │
      ▼
Webhook notifica resultado al sistema
      │
      ▼
Sistema notifica al usuario por push/email
```

## 2.7 Entidad ValidacionIA

```
ValidacionIA
├── id:                    INT          (PK)
├── ejemplar_id:           UUID         (FK → Ejemplar)
├── operacion_tipo:        ENUM         (PRESTAMO / DEVOLUCION)
├── foto_url:              VARCHAR(500)
├── confianza:             FLOAT
├── estado_detectado:      ENUM         (OK / DETERIORADO / GRAVE)
├── daños_detectados:      JSON
├── revisado_por_operador: BOOLEAN      DEFAULT FALSE
├── operador_id:           INT          (FK → Usuario, nullable)
├── comentario_operador:   TEXT         (nullable)
└── fecha_validacion:      DATETIME
```

## 2.8 Criterios de Aceptación

```
✅ El sistema solicita foto obligatoria antes de cada préstamo
✅ El sistema solicita foto obligatoria en cada devolución
✅ Si confianza IA > 85% y hay daño → estado SOSPECHOSO
✅ El operador puede confirmar o descartar en menos de 48hs
✅ Toda validación queda registrada con foto y resultado
✅ El proceso no bloquea al usuario más de 5 segundos
```

---

# RF-03 — TRAZABILIDAD COMPLETA DE LA CADENA DE PRÉSTAMOS

## 3.1 Descripción General

| Campo | Detalle |
|-------|---------|
| **ID** | RF-03 |
| **Nombre** | Trazabilidad de Cadena de Préstamos |
| **Prioridad** | Alta |
| **Módulo** | Auditoría y Trazabilidad |
| **Actor principal** | Propietario del ejemplar / Administrador |
| **Referencia** | ProtegePro (bitácora completa), SafeDrive (historial de pólizas), ONG Final 20250925 |

## 3.2 Necesidad Identificada

La organización necesita saber **en todo momento**:
- Dónde está cada ejemplar físicamente
- Quién lo tiene actualmente
- Cuánto tiempo lleva en cada mano
- El historial completo desde su incorporación
- Quién es el propietario legal en cada momento

## 3.3 Problema sin este Requerimiento

```
❌ "¿Dónde está mi libro?" → No hay respuesta posible
❌ No se puede responsabilizar a nadie por daños
❌ No se detectan préstamos que nunca se devuelven
❌ No hay auditoría de las operaciones realizadas
❌ El propietario pierde el rastro de su ejemplar
```

## 3.4 Visualización de la Cadena

```
Ejemplar #42 — "El Principito"
Propietario original: Ana García
─────────────────────────────────────────────────────
HISTORIAL COMPLETO:

[01/01] ALTA        Ana incorpora el ejemplar al sistema
[10/01] PRÉSTAMO    Ana ──────────────► Bob
[15/01] PRÉSTAMO    Bob ──────────────► Carlos  (nivel 2)
[20/01] PRÉSTAMO    Carlos ───────────► Diana   (nivel 3)
[01/02] DEVOLUCIÓN  Diana ────────────► Carlos
[05/02] DEVOLUCIÓN  Carlos ───────────► Bob
[10/02] DEVOLUCIÓN  Bob ──────────────► Ana
[01/03] PRÉSTAMO    Ana ──────────────► Elena
[10/03] CESIÓN      Ana cede propiedad a Elena
─────────────────────────────────────────────────────
Estado actual:  DISPONIBLE
Propietario:    Elena  (desde 10/03)
Tenedor actual: Elena
```

## 3.5 Alertas Automáticas por Cron Jobs

```
┌──────────────────────────────────────────────────────┐
│                 ALERTAS PROGRAMADAS                  │
│                                                      │
│  ⚠️  Préstamo sin devolver > 15 días                 │
│      → Notifica al tenedor actual                    │
│                                                      │
│  ⚠️  Préstamo sin devolver > 30 días                 │
│      → Notifica tenedor + propietario                │
│                                                      │
│  ⚠️  Cadena de préstamos > 4 eslabones               │
│      → Alerta a la organización + propietario        │
│                                                      │
│  ⚠️  Ejemplar sin movimiento > 90 días               │
│      → Sugiere al propietario prestarlo o donarlo    │
│                                                      │
│  ⚠️  Validación IA pendiente > 48 horas              │
│      → Escala automáticamente a operador humano      │
└──────────────────────────────────────────────────────┘
```

# RF-04 — PERFIL LECTOR Y RECOMENDACIONES PERSONALIZADAS

## 4.1 Descripción General

| Campo | Detalle |
|-------|---------|
| **ID** | RF-04 |
| **Nombre** | Perfil Lector y Recomendaciones Personalizadas |
| **Prioridad** | Media-Alta |
| **Módulo** | Recomendaciones e Inteligencia |
| **Actor principal** | Usuario lector registrado |
| **Actor secundario** | Sistema de IA Generativa (OpenAI) |
| **Referencia** | TalentHub (Recomendador con criterios), HealthMe (mensajes IA), EducAR+ (recomendaciones semanales) |

---

## 4.2 Necesidad Identificada

La organización quiere **fomentar la lectura activa** recomendando libros según el historial, preferencias y perfil de cada usuario. Sin este módulo:

```
❌ Los usuarios no saben qué leer después de terminar un libro
❌ Libros disponibles no llegan a quienes los quieren
❌ No se aprovecha el historial de préstamos acumulado
❌ La organización no puede medir impacto por perfil lector
❌ Se desperdicia el conocimiento colectivo de la red
```

---

## 4.3 Perfil Lector del Usuario

### **Datos calculados automáticamente por el sistema**

```
┌─────────────────────────────────────────────────────────┐
│              PERFIL LECTOR DEL USUARIO                  │
│                                                         │
│  Usuario: Carlos Pérez                                  │
│                                                         │
│  Actividad:                                             │
│  ├── Libros leídos:              23                     │
│  ├── Libros prestados a otros:    8                     │
│  ├── Libros recibidos:           15                     │
│  ├── Promedio días por libro:    12                     │
│  └── Nivel lector:               INTERMEDIO             │
│                                                         │
│  Preferencias detectadas:                               │
│  ├── Géneros:  [Ficción 60%, Historia 30%]              │
│  ├── Tags:     [#clasico, #latinoamerica]               │
│  └── Autores:  [García Márquez, Borges]                 │
│                                                         │
│  Recomendaciones activas:                               │
│  ├── Por historial propio                               │
│  ├── Por lo que leen usuarios similares                 │
│  └── Por libros disponibles en su red de contactos      │
└─────────────────────────────────────────────────────────┘
```

### **Cálculo del Nivel Lector**

```
NIVEL LECTOR se calcula automáticamente:

BÁSICO       → 0 a 5 libros leídos
INTERMEDIO   → 6 a 20 libros leídos
AVANZADO     → 21 a 50 libros leídos
EXPERTO      → más de 50 libros leídos

Recalculo: automático cada vez que se registra
           una devolución a nombre del usuario
```

---

## 4.4 Criterios de Recomendación

### **Patrón Strategy aplicado**

```
┌─────────────────────────────────────────────────────────┐
│           CRITERIOS DE RECOMENDACIÓN (Strategy)         │
│                                                         │
│  Criterio 1: Por afinidad de tags                       │
│  → Si leyó 3 libros con #clasico, recomendar más        │
│  → Peso sugerido: 40%                                   │
│                                                         │
│  Criterio 2: Por red social de préstamos                │
│  → Libros que leyeron personas que me prestaron         │
│  → Peso sugerido: 25%                                   │
│                                                         │
│  Criterio 3: Por disponibilidad cercana                 │
│  → Libros disponibles en mi zona geográfica             │
│  → Peso sugerido: 20%                                   │
│                                                         │
│  Criterio 4: Por tendencia general                      │
│  → Los más prestados del último mes en mi categoría     │
│  → Peso sugerido: 15%                                   │
└─────────────────────────────────────────────────────────┘
```

### **Implementación con Patrón Strategy**

```java
// Interfaz común para todos los criterios
interface CriterioRecomendacion {
    List<Obra> recomendar(Usuario usuario, int cantidad);
    String getNombre();
    double getPeso(); // configurable por administrador
}

// Criterio 1: Por afinidad de tags
class RecomendacionPorTags implements CriterioRecomendacion {
    @Override
    public List<Obra> recomendar(Usuario usuario, int cantidad) {
        // Obtiene los tags más frecuentes del historial
        // Busca obras con esos tags que no haya leído
        List<String> tagsFavoritos = usuario
            .getHistorial()
            .getTagsMasFrecuentes(3);
        return repositorioObras
            .buscarPorTags(tagsFavoritos, usuario.getObrasLeidas());
    }
}

// Criterio 2: Por red de préstamos
class RecomendacionPorRed implements CriterioRecomendacion {
    @Override
    public List<Obra> recomendar(Usuario usuario, int cantidad) {
        // Busca qué leyeron las personas que me prestaron libros
        List<Usuario> miRed = usuario.getRedDePrestamos();
        return miRed.stream()
            .flatMap(u -> u.getObrasLeidas().stream())
            .filter(o -> !usuario.getObrasLeidas().contains(o))
            .distinct()
            .limit(cantidad)
            .collect(Collectors.toList());
    }
}

// Criterio 3: Por disponibilidad cercana
class RecomendacionPorCercania implements CriterioRecomendacion {
    @Override
    public List<Obra> recomendar(Usuario usuario, int cantidad) {
        // Busca ejemplares DISPONIBLES en la zona del usuario
        return repositorioEjemplares
            .buscarDisponiblesEnZona(
                usuario.getZona(),
                usuario.getObrasLeidas()
            );
    }
}

// Criterio 4: Por tendencia general
class RecomendacionPorTendencia implements CriterioRecomendacion {
    @Override
    public List<Obra> recomendar(Usuario usuario, int cantidad) {
        // Busca las más prestadas del último mes
        // en las categorías favoritas del usuario
        return estadisticasService
            .getMasPrestadas(
                usuario.getCategoriasFavoritas(),
                Periodo.ULTIMO_MES,
                cantidad
            );
    }
}

// Motor de recomendaciones que combina criterios
class MotorRecomendaciones {

    private final List<CriterioRecomendacion> criterios;
    private final IAGenerativaClient iaClient;

    public List<RecomendacionPersonalizada> recomendar(
            Usuario usuario, int cantidad) {

        // 1. Ejecutar todos los criterios
        Map<Obra, Double> scoring = new HashMap<>();

        criterios.forEach(criterio -> {
            List<Obra> resultados = criterio.recomendar(
                usuario, cantidad
            );
            resultados.forEach(obra ->
                scoring.merge(
                    obra,
                    criterio.getPeso(),
                    Double::sum
                )
            );
        });

        // 2. Ordenar por scoring combinado
        List<Obra> topObras = scoring.entrySet().stream()
            .sorted(Map.Entry.<Obra, Double>
                comparingByValue().reversed())
            .limit(cantidad)
            .map(Map.Entry::getKey)
            .collect(Collectors.toList());

        // 3. Enriquecer con IA Generativa
        return topObras.stream()
            .map(obra -> enriquecerConIA(obra, usuario))
            .collect(Collectors.toList());
    }

    private RecomendacionPersonalizada enriquecerConIA(
            Obra obra, Usuario usuario) {
        String prompt = construirPrompt(obra, usuario);
        String mensajeIA = iaClient.generar(prompt);
        return new RecomendacionPersonalizada(obra, mensajeIA);
    }
}
```

---

## 4.5 Integración con IA Generativa

### **Flujo de generación de mensaje personalizado**

```
Perfil del usuario
+ Historial de lecturas
+ Obra recomendada
+ Disponibilidad actual
        │
        ▼
Construcción del Prompt
        │
        ▼
API OpenAI / IA Generativa
        │
        ▼
Mensaje personalizado en prosa:

"Hola Carlos, basado en tu amor por García Márquez
 y la literatura latinoamericana, creemos que vas
 a disfrutar 'El amor en los tiempos del cólera'.
 Actualmente está disponible: María López lo tiene
 y puede prestártelo directamente. ¡Es tu momento!"
```

### **Consideración arquitectónica**

```
⚠️  La IA puede tardar varios segundos en responder

SOLUCIÓN: Generación ASINCRÓNICA

Cron Job semanal genera recomendaciones
        │
        ▼
Worker llama a IA para cada usuario
        │
        ▼
Resultados guardados en caché/DB
        │
        ▼
Usuario consulta recomendaciones ya listas
(respuesta inmediata desde caché)
```

---

## 4.6 Entidades del Módulo

```
PerfilLector
├── id:                    INT      (PK)
├── usuario_id:            INT      (FK → Usuario, UNIQUE)
├── nivel_lector:          ENUM     (BASICO/INTERMEDIO/
│                                    AVANZADO/EXPERTO)
├── libros_leidos:         INT      DEFAULT 0
├── libros_prestados:      INT      DEFAULT 0
├── promedio_dias_libro:   FLOAT
└── ultima_actualizacion:  DATETIME

RecomendacionGenerada
├── id:                    INT      (PK)
├── usuario_id:            INT      (FK → Usuario)
├── obra_id:               INT      (FK → Obra)
├── criterio_origen:       ENUM     (TAGS/RED/CERCANIA/
│                                    TENDENCIA)
├── scoring:               FLOAT
├── mensaje_ia:            TEXT     (nullable)
├── fecha_generacion:      DATETIME
├── vista_por_usuario:     BOOLEAN  DEFAULT FALSE
└── fecha_vista:           DATETIME (nullable)
```

---

## 4.7 Endpoints del Servicio

```
GET  /recomendaciones/usuarios/{id}
     → Lista de recomendaciones personalizadas activas

GET  /recomendaciones/usuarios/{id}/perfil-lector
     → Perfil lector calculado del usuario

POST /recomendaciones/usuarios/{id}/regenerar
     → Fuerza regeneración de recomendaciones

PUT  /recomendaciones/{id}/marcar-vista
     → Registra que el usuario vio la recomendación
```

---

## 4.8 Criterios de Aceptación

```
✅ El perfil lector se actualiza automáticamente
   tras cada devolución registrada

✅ Se generan al menos 5 recomendaciones por usuario
   una vez por semana

✅ Cada recomendación incluye mensaje personalizado
   generado por IA

✅ Los criterios de recomendación son configurables
   por el administrador (pesos ajustables)

✅ Se puede agregar un nuevo criterio sin modificar
   el motor existente (OCP - Open/Closed Principle)

✅ Las recomendaciones se muestran en menos de 1 segundo
   (servidas desde caché)
```

---

---

# RF-05 — SISTEMA DE NOTIFICACIONES Y ENGAGEMENT LECTOR

## 5.1 Descripción General

| Campo | Detalle |
|-------|---------|
| **ID** | RF-05 |
| **Nombre** | Notificaciones y Engagement Lector |
| **Prioridad** | Alta |
| **Módulo** | Comunicaciones y Retención |
| **Actor principal** | Usuario lector registrado |
| **Actor secundario** | Operador / Administrador |
| **Referencia** | HealthMe (notificaciones push + IA), Mi Amigo Invisible (engagement post-evento), EasyTech (notificaciones por cambio de estado) |

---

## 5.2 Necesidad Identificada

Para que la circulación de libros sea efectiva, la organización necesita **mantener activos y comprometidos** a los usuarios. Sin este módulo:

```
❌ Los libros se quedan sin devolver por simple olvido
❌ Los usuarios no saben que alguien quiere su libro
❌ Propietarios pierden rastro de su ejemplar
❌ La cadena A→B→C→D se rompe sin aviso
❌ Usuarios se desconectan del proyecto social
❌ La organización no puede medir engagement
```

---

## 5.3 Mapa Completo de Notificaciones

### **Tipo 1 — Inmediatas (disparadas por evento)**

```
┌──────────────────────────────────────────────────────────┐
│           NOTIFICACIONES INMEDIATAS                      │
│                                                          │
│  EVENTO                    DESTINATARIO   MENSAJE        │
│  ──────────────────────────────────────────────────────  │
│  Préstamo registrado    →  Prestatario  → "Ana te        │
│                                            prestó        │
│                                            'El Principito'│
│                                                          │
│  Devolución registrada  →  Prestador    → "Carlos te     │
│                                            devolvió      │
│                                            tu libro"     │
│                                                          │
│  Cesión realizada       →  Nuevo dueño  → "¡Ana te cedió │
│                                            la propiedad!"│
│                                                          │
│  Daño detectado por IA  →  Propietario  → "Se detectó   │
│                                            daño en tu    │
│                                            ejemplar #42" │
│                                                          │
│  Baja del ejemplar      →  Propietario  → "Tu ejemplar  │
│                                            fue dado      │
│                                            de baja"      │
└──────────────────────────────────────────────────────────┘
```

### **Tipo 2 — Programadas (Cron Jobs)**

```
┌──────────────────────────────────────────────────────────┐
│           NOTIFICACIONES PROGRAMADAS                     │
│                                                          │
│  CONDICIÓN               FRECUENCIA    DESTINATARIO      │
│  ──────────────────────────────────────────────────────  │
│  Préstamo sin devolver   A los 15 días  Tenedor actual   │
│                          A los 25 días  Tenedor +        │
│                                         Propietario      │
│                          A los 30 días  Tenedor +        │
│                                         Propietario +    │
│                                         Organización     │
│                                                          │
│  Cadena