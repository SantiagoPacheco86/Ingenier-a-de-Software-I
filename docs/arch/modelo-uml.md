# Modelo UML de BIOMA — estructura y comportamiento

**Sistema:** BIOMA — Sistema de detección de flora y fauna local para senderistas  
**Autor:** Santiago Pacheco Carrillo  
**Asignatura:** Ingeniería de Software I · SIS3407  
**Versión:** 2.0 · 17/11/2026  
**Arquitectura relacionada:** [`arquitectura-c4.md`](arquitectura-c4.md)  
**Versión anterior del modelo de clases:** [`DOO_S12S13.md`](DOO_S12S13.md) §5 (04/11/2026)

> Son modelos de **diseño**, no evidencia de implementación ejecutada. El repositorio no contiene código fuente.

---

## 1. Qué cambió al modelar la secuencia (v1 → v2)

Al dibujar la secuencia de CU-01 con el diagrama de clases de `DOO_S12S13.md` aparecieron tres huecos:

| # | Hueco detectado | Cómo apareció | Corrección en v2 |
|---|---|---|---|
| 1 | **Nadie verificaba la precisión del modelo.** `validarConfianza(umbral)` solo comparaba la confianza de una inferencia, pero el alcance exige además que el modelo cumpla 90 % o 99 % de precisión (RNF-CON-002 y RNF-CON-003). | El mensaje que debía decidir «modelo elegible» no tenía una operación a la que dirigirse. Quedó como nota sobre el backend. | `ResultadoInferencia` conserva `precisionModelo` y `versionModelo`. La interfaz `ValidadorConfirmacion` evalúa ambos criterios. `validarConfianza(umbral)` se sustituye por `evaluar(v)`. |
| 2 | **El patrón Factory/Strategy existía solo en C4.** | La secuencia necesitaba elegir un umbral y no había clase que lo hiciera. | Se agregan `FabricaValidador`, `ValidadorConfirmacion`, `ValidadorGeneral` y `ValidadorMedico`. |
| 3 | **Los estados no tenían operaciones que los produjeran.** `estado` era un `String` y la transición `evaluar` no existía en la clase. | El diagrama de estados usaba transiciones sin una operación correspondiente. | Se agrega la enumeración `EstadoIdentificacion` y las operaciones `asignarResultado()`, `marcarNoConfirmada()` y `marcarNoReconocida()`. |

Otras correcciones:
- La secuencia ahora crea la `Identificacion` y usa `esRegistrable()`.
- `aplicarLimite()` se ejecuta **antes** de agregar, como indica CU-09 A1.
- El diagrama de actividad limita el modo offline a especies de importancia médica (RF-008) y lo coloca en el carril de la aplicación, no en el del backend.

---

## 2. Diagrama de clases (v2)

```mermaid
classDiagram
    direction LR

    class Usuario {
        -String id
        -String tipoPerfil
        -Boolean cuentaHabilitada
        +puedeRegistrarObservacion() Boolean
        +puedeConsultarRegistro() Boolean
    }
    class ServicioIdentificacion {
        <<service>>
        +identificar(imagen: ByteArray, region: Region, u: Usuario) Identificacion
    }
    class Identificacion {
        -String id
        -Float confianza
        -Date fecha
        -EstadoIdentificacion estado
        +Identificacion(u: Usuario)
        +asignarResultado(r: ResultadoInferencia) void
        +evaluar(v: ValidadorConfirmacion) Boolean
        +confirmar() void
        +marcarNoConfirmada() void
        +marcarNoReconocida() void
        +esRegistrable() Boolean
    }
    class EstadoIdentificacion {
        <<enumeration>>
        PENDIENTE
        PROCESADA
        CONFIRMADA
        NO_CONFIRMADA
        NO_RECONOCIDA
    }
    class ResultadoInferencia {
        -Float confianzaMaxima
        -String origenInferencia
        -String versionModelo
        -Float precisionModelo
        +obtenerMejorCandidato() Especie
        +obtenerConfianza() Float
        +obtenerPrecisionModelo() Float
    }
    class ValidadorConfirmacion {
        <<interface>>
        +umbralConfianza() Float
        +precisionMinima() Float
        +validar(r: ResultadoInferencia) Boolean
    }
    class ValidadorGeneral {
        -Float UMBRAL = 0.90
        -Float PRECISION = 0.90
        +validar(r: ResultadoInferencia) Boolean
    }
    class ValidadorMedico {
        -Float UMBRAL = 0.99
        -Float PRECISION = 0.99
        +validar(r: ResultadoInferencia) Boolean
    }
    class FabricaValidador {
        +crearPara(e: Especie) ValidadorConfirmacion
    }
    class Especie {
        -String id
        -String nombreComun
        -String nombreCientifico
        -Boolean importanciaMedica
        -String nivelRiesgo
        +esDeImportanciaMedica() Boolean
        +obtenerFicha() String
    }
    class Historial {
        -Integer capacidadMaxima
        +agregarConfirmada(i: Identificacion) Boolean
        +consultar() List~Identificacion~
        +aplicarLimite() void
    }
    class Observacion {
        -String id
        -String notas
        -Date fecha
        +validarDatos() Boolean
        +actualizarContenido(notas: String) void
    }
    class Region {
        -String id
        -String nombre
        -String ambitoGeografico
        +contieneEspecie(e: Especie) Boolean
        +listarEspecies() List~Especie~
    }
    class PaqueteRegional {
        -String version
        -String estadoDescarga
        -Boolean disponibleOffline
        +descargar() void
        +verificarDisponibilidad() Boolean
        +habilitarUsoOffline() Boolean
    }

    Usuario "1" *-- "1" Historial : posee
    Usuario "1" --> "0..*" Identificacion : realiza
    Usuario "1" --> "0..*" Observacion : registra
    Historial "0..1" --> "0..50" Identificacion : conserva confirmadas
    Identificacion "1" *-- "0..1" ResultadoInferencia : contiene
    Identificacion "0..*" --> "0..1" Especie : identifica si se confirma
    ResultadoInferencia "0..*" --> "0..*" Especie : propone candidatas
    Observacion "0..*" --> "1" Especie : documenta
    Region "0..*" --> "0..*" Especie : cataloga
    PaqueteRegional "0..*" --> "1" Region : corresponde a
    ValidadorConfirmacion <|.. ValidadorGeneral
    ValidadorConfirmacion <|.. ValidadorMedico
    FabricaValidador ..> ValidadorConfirmacion : crea
    FabricaValidador ..> Especie : consulta
    Identificacion ..> ValidadorConfirmacion : usa
    ServicioIdentificacion ..> Identificacion : crea
    ServicioIdentificacion ..> FabricaValidador : usa
    ServicioIdentificacion ..> Historial : registra
```

**Decisiones de multiplicidad que cambiaron:**

- `Identificacion "1" *-- "0..1" ResultadoInferencia`: una identificación recién creada (`PENDIENTE`) todavía no tiene resultado.
- `ResultadoInferencia "0..*" --> "0..*" Especie`: antes era `1..*`. Una especie fuera del modelo no genera candidatas (RF-005, estado `NO_RECONOCIDA`).
- `0..50` sigue siendo la capacidad del **usuario estándar** (RNF-ESC-001). La capacidad del usuario avanzado no está especificada; queda pendiente.

**Agrupación por módulo (ADR-001):**

| Módulo | Clases |
|---|---|
| Identificación y reconocimiento | `ServicioIdentificacion`, `Identificacion`, `EstadoIdentificacion`, `ResultadoInferencia`, `FabricaValidador`, `ValidadorConfirmacion`, `ValidadorGeneral`, `ValidadorMedico` |
| Especies y regiones | `Especie`, `Region`, `PaqueteRegional` |
| Gestión de usuarios | `Usuario` |
| Historial y observaciones | `Historial`, `Observacion` |

---

## 3. Diagrama de secuencia — CU-01 Identificar una especie (en línea)

> `App`, `Servicio de inferencia` y el actor son contenedores o actores de C4: sus mensajes son llamadas HTTP, no operaciones de clase. **Cada mensaje dirigido a un objeto de dominio corresponde a una operación declarada en §2.**

```mermaid
sequenceDiagram
    autonumber
    actor U as Usuario
    participant App as App móvil
    participant S as :ServicioIdentificacion
    participant IA as Servicio de inferencia
    participant I as :Identificacion
    participant R as :ResultadoInferencia
    participant F as :FabricaValidador
    participant E as :Especie
    participant V as :ValidadorConfirmacion
    participant H as :Historial

    U->>App: Toca «Identificar» (imagen validada en CU-07)
    App->>S: identificar(imagen, region, usuario) [HTTPS]
    S->>I: Identificacion(usuario)
    Note right of I: PENDIENTE
    S->>IA: POST /inferir (imagen, region)
    IA-->>S: candidatas, confianza, versión y precisión del modelo
    S->>I: asignarResultado(r)
    Note right of I: PROCESADA
    I->>R: obtenerMejorCandidato()
    R-->>I: especie o null
    alt Sin especie candidata (RF-005)
        S->>I: marcarNoReconocida()
        S-->>App: «No fue posible reconocer la especie»
    else Hay especie candidata
        S->>F: crearPara(especie)
        F->>E: esDeImportanciaMedica()
        E-->>F: true / false
        F-->>S: ValidadorMedico o ValidadorGeneral
        S->>I: evaluar(validador)
        I->>V: validar(r)
        V->>R: obtenerPrecisionModelo()
        V->>R: obtenerConfianza()
        V-->>I: cumple / no cumple
        alt Cumple precisión y confianza
            I->>I: confirmar()
            S->>H: agregarConfirmada(identificacion)
            H->>I: esRegistrable()
            H->>H: aplicarLimite()
            H-->>S: true
            S-->>App: Identificación confirmada (especie, confianza)
        else No cumple (RF-010, RF-011)
            I->>I: marcarNoConfirmada()
            S-->>App: Posible identificación + advertencia (no se guarda)
        end
    end
    App-->>U: Muestra el resultado
```

### Correspondencia mensaje → operación

| Mensaje | Clase | Operación declarada |
|---|---|---|
| 2 `identificar(imagen, region, usuario)` | `ServicioIdentificacion` | `+identificar(imagen, region, u) Identificacion` |
| 3 `Identificacion(usuario)` | `Identificacion` | constructor `+Identificacion(u: Usuario)` |
| 6 `asignarResultado(r)` | `Identificacion` | `+asignarResultado(r) void` |
| 7 `obtenerMejorCandidato()` | `ResultadoInferencia` | `+obtenerMejorCandidato() Especie` |
| 11 `crearPara(especie)` | `FabricaValidador` | `+crearPara(e: Especie) ValidadorConfirmacion` |
| 12 `esDeImportanciaMedica()` | `Especie` | `+esDeImportanciaMedica() Boolean` |
| 15 `evaluar(validador)` | `Identificacion` | `+evaluar(v: ValidadorConfirmacion) Boolean` |
| 16 `validar(r)` | `ValidadorConfirmacion` | `+validar(r: ResultadoInferencia) Boolean` |
| 17–18 `obtenerPrecisionModelo()`, `obtenerConfianza()` | `ResultadoInferencia` | `+obtenerPrecisionModelo() Float`, `+obtenerConfianza() Float` |
| 20, 26, 9 `confirmar()`, `marcarNoConfirmada()`, `marcarNoReconocida()` | `Identificacion` | operaciones homónimas |
| 21 `agregarConfirmada(identificacion)` | `Historial` | `+agregarConfirmada(i: Identificacion) Boolean` |
| 22 `esRegistrable()` | `Identificacion` | `+esRegistrable() Boolean` |
| 23 `aplicarLimite()` | `Historial` | `+aplicarLimite() void` |

---

## 4. Diagrama de estados — ciclo de vida de `Identificacion`

Cada estado es un valor de `EstadoIdentificacion`, y cada transición se dispara con una operación de `Identificacion`.

```mermaid
stateDiagram-v2
    [*] --> PENDIENTE : Identificacion(usuario)
    PENDIENTE --> PROCESADA : asignarResultado(r)
    PROCESADA --> NO_RECONOCIDA : marcarNoReconocida() [sin candidata]
    PROCESADA --> CONFIRMADA : confirmar() [evaluar(v) = true]
    PROCESADA --> NO_CONFIRMADA : marcarNoConfirmada() [evaluar(v) = false]
    CONFIRMADA --> [*] : esRegistrable() = true → Historial
    NO_CONFIRMADA --> [*] : se muestra como posible identificación
    NO_RECONOCIDA --> [*]
```

`CONFIRMADA`, `NO_CONFIRMADA` y `NO_RECONOCIDA` son estados finales del **proceso** de identificación; no significan que la instancia se borre de inmediato. Compartir en redes (SC-001, propuesto) no agrega ningún estado, porque es una acción externa sobre un resultado y no altera su confirmación.

---

## 5. Diagrama de actividad — identificación en línea y sin conexión

```mermaid
flowchart TD
    subgraph usuario["Usuario"]
        A([Inicio]) --> B[Capturar imagen · CU-06]
    end
    subgraph app["Aplicación móvil [Kotlin]"]
        C[Verificar calidad · CU-07]
        D{¿Imagen adecuada?}
        E[Solicitar nueva captura con recomendaciones · RF-012]
        F{¿Hay conexión?}
        G{¿Paquete regional médico descargado?}
        Z[Informar que debe descargarse con Internet · CU-04 A1]
        H[Inferencia local LiteRT · solo especies médicas]
        HV[Aplicar ValidadorMedico · 99 %]
        P[Mostrar resultado con nivel de confianza · RF-003]
    end
    subgraph nube["Backend modular + servicio de inferencia"]
        I[Inferencia en la nube]
        K{¿Hay especie candidata?}
        NR[marcarNoReconocida · RF-005]
        FV[FabricaValidador.crearPara]
        N{¿Precisión del modelo y confianza suficientes?}
        O[confirmar]
        R[aplicarLimite · 50 estándar]
        Q[agregarConfirmada al historial]
        S[marcarNoConfirmada · posible identificación]
    end
    B --> C --> D
    D -->|No| E --> B
    D -->|Sí| F
    F -->|Sí| I --> K
    F -->|No| G
    G -->|No| Z --> T([Fin])
    G -->|Sí| H --> HV --> P
    K -->|No| NR --> P
    K -->|Sí| FV --> N
    N -->|Sí| O --> R --> Q --> P
    N -->|No| S --> P
    P --> T
```

> **Pendiente de especificar:** si una identificación confirmada offline se registra en el historial cuando se recupera la conexión. CU-04 no lo define y este diagrama no lo presupone.

---

## 6. Casos de uso (catálogo v1.2)

El diagrama editable está en [`../diagramas/casos-de-uso.drawio`](../diagramas/casos-de-uso.drawio), con su exportación [`casos-de-uso.drawio.png`](../diagramas/casos-de-uso.drawio.png). Esta versión en Mermaid es una aproximación textual:

```mermaid
flowchart LR
    est(["👤 Usuario estándar"])
    avan(["👤 Usuario avanzado"])
    avan -->|generalización| est

    subgraph BIOMA
        cu06([CU-06 Capturar imagen])
        cu07([CU-07 Verificar calidad])
        cu01([CU-01 Identificar especie])
        cu10([CU-10 Consultar nivel de confianza])
        cu08([CU-08 Consultar información de especie])
        cu09([CU-09 Registrar identificación confirmada])
        cu04([CU-04 Identificar especie médica sin conexión])
        cu05([CU-05 Descargar datos regionales])
        cu02([CU-02 Consultar historial])
        cu03([CU-03 Registrar observación avanzada])
    end

    est --- cu06
    est --- cu01
    est --- cu04
    est --- cu05
    est --- cu02
    avan --- cu03
    cu06 -.->|«include»| cu07
    cu01 -.->|«include»| cu10
    cu04 -.->|«include»| cu10
    cu08 -.->|«extend»| cu01
    cu09 -.->|«extend» si confirmada| cu01
```

---

## 7. Diagrama entidad-relación conceptual

> Propuesta de persistencia en PostgreSQL (ADR-002), **no esquema SQL verificado**. Las identificaciones no confirmadas no se vinculan al historial.

```mermaid
erDiagram
    USUARIO ||--|| HISTORIAL : posee
    USUARIO ||--o{ IDENTIFICACION : realiza
    USUARIO ||--o{ OBSERVACION : registra
    HISTORIAL o|--o{ IDENTIFICACION : conserva_confirmadas
    ESPECIE o|--o{ IDENTIFICACION : identificada_en
    ESPECIE ||--o{ OBSERVACION : documentada_en
    REGION }o--o{ ESPECIE : cataloga
    REGION ||--o{ PAQUETE_REGIONAL : tiene
    IDENTIFICACION ||--o| RESULTADO_INFERENCIA : genera
    RESULTADO_INFERENCIA }o--o{ ESPECIE : propone

    USUARIO {
        string id PK
        string tipoPerfil
        boolean cuentaHabilitada
    }
    HISTORIAL {
        string id PK
        string usuarioId FK
        int capacidadMaxima
    }
    IDENTIFICACION {
        string id PK
        string usuarioId FK
        string especieId FK
        float confianza
        date fecha
        string estado "PENDIENTE|PROCESADA|CONFIRMADA|NO_CONFIRMADA|NO_RECONOCIDA"
    }
    RESULTADO_INFERENCIA {
        string id PK
        string identificacionId FK
        float confianzaMaxima
        string origenInferencia
        string versionModelo
        float precisionModelo
    }
    ESPECIE {
        string id PK
        string nombreComun
        string nombreCientifico
        boolean importanciaMedica
        string nivelRiesgo
    }
    OBSERVACION {
        string id PK
        string usuarioId FK
        string especieId FK
        string notas
        date fecha
    }
    REGION {
        string id PK
        string nombre
        string ambitoGeografico
    }
    PAQUETE_REGIONAL {
        string id PK
        string regionId FK
        string version
        string estadoDescarga
        boolean disponibleOffline
    }
```

---

## 8. Revisión de consistencia (v2)

| Verificación | Resultado |
|---|---|
| Secuencia ↔ clases | Los 16 mensajes dirigidos a objetos de dominio corresponden a operaciones declaradas (tabla §3). |
| Estados ↔ clases | Los cinco estados son valores de `EstadoIdentificacion` y cada transición es una operación de `Identificacion`. |
| C4 ↔ clases | `ServicioIdentificacion`, `FabricaValidador`, `ValidadorGeneral` y `ValidadorMedico` aparecen en el nivel 3 de C4, en las clases y en la secuencia. |
| C4 ↔ secuencia | La app móvil, el backend y el servicio de inferencia corresponden a contenedores del nivel 2. |
| Actividad ↔ requisitos | La ruta offline aplica solo a especies médicas (RF-008) y siempre usa el umbral del 99 %. |
| Casos de uso ↔ especificación | Los 10 CU del catálogo v1.2 están en el `.drawio`, en el PNG y en §6. |
| SC-001 | **No incorporado a la línea base.** RF-016, CU-11 y ADR-003 son propuestas. |

### Pendientes declarados

1. Capacidad del historial del usuario avanzado.
2. Registro en el historial de identificaciones confirmadas offline.
3. RF-015 (cuentas): `Usuario.cuentaHabilitada` se conserva, pero el mecanismo de autenticación no está decidido.
4. Persistencia: el ER es conceptual; faltan tablas puente y la política para resultados no confirmados.
