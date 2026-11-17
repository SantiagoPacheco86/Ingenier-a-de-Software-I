# ADR-002: Usar Kotlin en la aplicación y en el backend, y Python solo en el servicio de inferencia

## Estado

Aceptada — 17 de noviembre de 2026.

## Contexto

ADR-001 definió un backend en monolito modular con un servicio de inferencia separado, pero no fijó tecnologías. El diagrama de contenedores no podía indicar con qué se construye cada parte. Hechos de BIOMA que condicionan la elección:

- BIOMA es una **aplicación móvil** que usa cámara y debe identificar especies de importancia médica **sin conexión** (RF-008), con paquetes regionales descargados (RF-009).
- La **regla de confirmación** (precisión del modelo y confianza de 90 % / 99 %) debe aplicarse igual en la nube y en el modo offline. Si se programa dos veces en lenguajes distintos, las dos versiones pueden divergir.
- El proyecto lo desarrolla **una sola persona** (ADR-001), que ya trabaja con Kotlin en Android.
- La identificación debe completarse en un máximo de **15 segundos** (RNF-REN-001).
- El historial y las observaciones son **privados por usuario** (RNF-SEG-001), y el modelo de datos tiene relaciones muchos-a-muchos (región–especie, resultado–especie).

Alternativas evaluadas:

1. **Kotlin en app y backend, Python en inferencia** (elegida).
2. **Flutter (Dart) multiplataforma + backend en Node.js**: daría iOS desde el inicio, pero implica tres lenguajes y obliga a reescribir la regla de validación fuera de Kotlin.
3. **Todo en Python** (backend y modelo) **+ app nativa en Kotlin**: unifica el backend con la inferencia, pero la regla de validación queda en un lenguaje distinto al de la app que la necesita offline.

## Decisión

| Contenedor | Tecnología |
|---|---|
| Aplicación móvil | Kotlin, Jetpack Compose (interfaz), CameraX (captura), LiteRT/TensorFlow Lite (inferencia offline) |
| Almacén local | Room sobre SQLite para paquetes y caché; archivo `.tflite` del paquete regional |
| Backend modular | Kotlin sobre JVM con Ktor; API REST/JSON sobre HTTPS |
| Módulo de dominio compartido | Biblioteca Kotlin pura (`bioma-dominio`) con `FabricaValidador`, `ValidadorGeneral` y `ValidadorMedico`, usada por la app y por el backend |
| Servicio de inferencia | Python, FastAPI y PyTorch; se comunica con el backend por HTTP interno/JSON |
| Base de datos | PostgreSQL |

La plataforma inicial es **Android**. iOS queda fuera de la primera versión.

## Consecuencias

**Positivas:**

- La regla del 99 % se escribe **una vez** y se ejecuta igual en línea y offline, porque el módulo de dominio es compartido.
- Un solo lenguaje (Kotlin) para casi todo el código que mantiene una persona.
- Python queda aislado en el contenedor donde su ecosistema de aprendizaje automático es necesario, que además es el primer candidato a escalar por separado según ADR-001.
- PostgreSQL resuelve las tablas puente del modelo ER y permite filtrar por usuario para cumplir RNF-SEG-001.

**Negativas y riesgos:**

- Hay **dos lenguajes y dos cadenas de compilación** (Kotlin y Python), con su costo de despliegue.
- **Sin iOS** en la primera versión: los usuarios de iPhone quedan fuera. Si se exige, habrá que revisar esta decisión (por ejemplo, con Kotlin Multiplatform).
- Convertir el modelo de PyTorch a LiteRT puede **reducir su precisión**. Cada paquete offline debe volver a medirse contra RNF-CON-003 (99 %) antes de publicarse.
- El paquete offline ocupa espacio en el dispositivo. CU-05 A2 ya contempla almacenamiento insuficiente.

**Condición para reconsiderar:** si se pide soporte para iOS, o si el modelo convertido a LiteRT no alcanza el 99 % de precisión en especies médicas.
