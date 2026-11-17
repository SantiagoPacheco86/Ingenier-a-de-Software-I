
# Diagramas ADR - Ingeniería de Software

Este documento reúne los diagramas de arquitectura y modelado de BIOMA. Los diagramas 1–3 se conservan de la versión original; los restantes se adaptan al dominio de identificación de especies. Son modelos de diseño, no evidencia de implementación ejecutada.

---

# Registros de decisión y taller de diagramas

## 1. Diagrama de contexto — C4 Nivel 1

```mermaid
flowchart TD
    est(["Usuario estándar"])
    avan(["Usuario avanzado"])
    bioma["BIOMA<br/>Sistema de identificación de especies"]

    est -->|"Identifica especies y consulta resultados"| bioma
    avan -->|"Identifica especies y registra observaciones avanzadas"| bioma

    bioma -->|"Entrega identificaciones e información de especies"| est
    bioma -->|"Entrega resultados e historial autorizado"| avan

    style bioma fill:#ff5d00,color:#fff,stroke:#d94e00
```

## 2. Diagrama de contenedores — C4 Nivel 2

```mermaid
flowchart TD
    usuario(["Usuario de BIOMA"])

    subgraph sistema["Sistema BIOMA"]
        app["Aplicación móvil<br/>Interfaz y funciones offline"]

        subgraph nube["Infraestructura en la nube"]
            api["Backend modular<br/>API del sistema"]
            ia["Servicio de inferencia<br/>Modelo principal de IA"]
            db[("Base de datos compartida<br/>Aislamiento lógico por usuario")]
        end
    end

    usuario -->|"Utiliza"| app
    app -->|"HTTPS / Solicitudes y resultados"| api
    api -->|"Solicita identificación"| ia
    ia -->|"Devuelve predicción y confianza"| api
    api -->|"Consulta y almacena registros"| db
    api -->|"HTTPS / Respuesta"| app

    app -->|"Identificación sin conexión<br/>con recursos descargados"| app

    style api fill:#ff5d00,color:#fff,stroke:#d94e00
    style ia fill:#ffe2d1,stroke:#ff5d00,color:#222
```

## 3. Diagrama de componentes — C4 Nivel 3

```mermaid
flowchart TD
    app["Aplicación móvil"]
    ia["Motor de inferencia IA"]
    db[("Base de datos")]

    subgraph backend["Backend modular de BIOMA"]
        especies["Especies y regiones<br/>Catálogo y datos regionales"]
        identificacion["Identificación y reconocimiento<br/>Validación de resultados"]
        usuarios["Gestión de usuarios<br/>Cuentas y permisos"]
        historial["Historial y observaciones<br/>Registros autorizados"]

        fabrica["Factory<br/>Selección de validador"]
        general["Strategy general<br/>Confianza mínima 90%"]
        medico["Strategy médica<br/>Confianza mínima 99%"]
    end

    app -->|"Solicita identificación"| identificacion
    app -->|"Consulta catálogo"| especies
    app -->|"Gestiona cuenta"| usuarios
    app -->|"Consulta historial"| historial

    identificacion -->|"Solicita predicción"| ia
    identificacion -->|"Consulta especies regionales"| especies
    identificacion -->|"Selecciona criterio"| fabrica

    fabrica -->|"Especie general"| general
    fabrica -->|"Importancia médica"| medico

    general -->|"Validación aprobada"| identificacion
    medico -->|"Validación aprobada"| identificacion

    identificacion -->|"Envía resultados confirmados"| historial
    historial -->|"Verifica permisos"| usuarios

    especies -->|"Consulta catálogo"| db
    usuarios -->|"Gestiona cuentas"| db
    historial -->|"Conserva registros"| db

    style identificacion fill:#ff5d00,color:#fff,stroke:#d94e00
    style fabrica fill:#ffe2d1,stroke:#ff5d00,color:#222
```



---

# Diagramas de diseño y comportamiento de BIOMA

> **Alcance:** Los diagramas 4–9 representan el flujo de identificación de especies y sus datos. Los porcentajes del modelo son 90 % para especies generales y 99 % para especies de importancia médica. La confianza por sí sola no garantiza que el modelo cumpla su requisito de exactitud; ambos criterios deben verificarse.

## 4. Diagrama de flujo con decisiones — Identificación de especies

```mermaid
flowchart TD
    ini([Inicio]) --> captura[Capturar o seleccionar imagen]
    captura --> calidad{Imagen adecuada?}
    calidad -->|No| repetir[Solicitar nueva imagen]
    repetir --> captura
    calidad -->|Si| conexion{Hay conexion?}
    conexion -->|Si| nube[Inferencia con modelo principal en nube]
    conexion -->|No| paquete{Paquete regional disponible?}
    paquete -->|No| sinservicio[Informar que no es posible identificar offline]
    paquete -->|Si| local[Inferencia con recursos regionales]
    nube --> resultado[Obtener candidato y confianza]
    local --> resultado
    resultado --> tipo{Especie de importancia medica?}
    tipo -->|Si| medica{Modelo cumple 99% de exactitud y confianza >= 99%?}
    tipo -->|No| general{Modelo cumple 90% de exactitud y confianza >= 90%?}
    medica -->|Si| confirmar[Confirmar identificacion]
    general -->|Si| confirmar
    medica -->|No| insuficiente[Mostrar resultado no confirmado]
    general -->|No| insuficiente
    confirmar --> guardar[Agregar al historial autorizado]
    guardar --> limite{Usuario estandar y mas de 50 registros?}
    limite -->|Si| eliminar[Eliminar registro confirmado mas antiguo]
    limite -->|No| mostrar[Mostrar identificacion confirmada]
    eliminar --> mostrar
    insuficiente --> fin([Fin])
    mostrar --> fin
    sinservicio --> fin
    style confirmar fill:#ff5d00,color:#fff,stroke:#d94e00
```

## 5. Diagrama de secuencia — CU-01 Identificar especie

> Los participantes `Aplicación móvil`, `Backend modular` y `Motor IA` son componentes de arquitectura. Los mensajes dirigidos a objetos de dominio usan operaciones declaradas en el diagrama de clases. Las llamadas a componentes representan intercambios entre subsistemas, no métodos añadidos a clases.

```mermaid
sequenceDiagram
    actor U as Usuario
    participant App as Aplicacion movil
    participant API as Backend modular
    participant IA as Motor de inferencia IA
    participant R as ResultadoInferencia
    participant E as Especie
    participant I as Identificacion
    participant H as Historial

    U->>App: Captura imagen de especie
    App->>API: Solicita identificacion(imagen, region)
    API->>IA: Solicita inferencia(imagen)
    IA-->>API: Prediccion y confianza
    API->>R: obtenerMejorCandidato()
    R-->>API: Especie candidata
    API->>R: obtenerConfianza()
    R-->>API: Confianza del candidato
    API->>E: esDeImportanciaMedica()
    E-->>API: true o false
    Note over API,I: Selecciona umbral segun tipo de especie y exactitud del modelo
    API->>I: validarConfianza(umbral)
    I-->>API: Cumple o no cumple
    alt Modelo elegible y confianza suficiente
        API->>I: confirmar()
        I-->>API: Identificacion confirmada
        API->>H: agregarConfirmada(identificacion)
        H->>H: aplicarLimite()
        H-->>API: Resultado de registro
        API-->>App: Especie confirmada e historial actualizado
    else Criterios de confirmacion no cumplidos
        API-->>App: Resultado no confirmado, sin guardar en historial
    end
    App-->>U: Muestra resultado
```

**Consistencia:** `validarConfianza()` valida el umbral de confianza; la elegibilidad por exactitud del modelo se comprueba en el componente de identificación del backend. En una implementación real deben definirse las operaciones del servicio que realiza esta segunda verificación.

## 6. Diagrama de clases — Modelo de dominio BIOMA

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
    class Especie {
        -String id
        -String nombreComun
        -String nombreCientifico
        -Boolean importanciaMedica
        -String nivelRiesgo
        +esDeImportanciaMedica() Boolean
        +obtenerFicha() String
    }
    class Identificacion {
        -String id
        -Float confianza
        -Date fecha
        -String estado
        +validarConfianza(umbral: Float) Boolean
        +confirmar() Boolean
        +esRegistrable() Boolean
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
    class ResultadoInferencia {
        -Float confianzaMaxima
        -String origenInferencia
        +obtenerMejorCandidato() Especie
        +obtenerConfianza() Float
    }
    Usuario "1" *-- "1" Historial : posee
    Historial "0..1" --> "0..50" Identificacion : conserva confirmadas
    Usuario "1" --> "0..*" Identificacion : realiza
    Usuario "1" --> "0..*" Observacion : registra
    Identificacion "0..*" --> "0..1" Especie : identifica si se confirma
    Identificacion "1" *-- "1" ResultadoInferencia : contiene resultado
    ResultadoInferencia "0..*" --> "1..*" Especie : propone candidatas
    Observacion "0..*" --> "1" Especie : documenta
    Region "0..*" --> "0..*" Especie : cataloga
    PaqueteRegional "0..*" --> "1" Region : corresponde a
```

> **Nota de alcance:** La multiplicidad `0..50` representa el historial del usuario estándar (RNF-ESC-001). Si el perfil avanzado tiene otra capacidad, el modelo de clases deberá distinguir esa variante. Se conserva la multiplicidad original para no modificar silenciosamente el diseño previamente entregado.

## 7. Diagrama de estados — Ciclo de vida de Identificacion

> Máquina de estados de **una instancia de `Identificacion`**. Los nombres corresponden a valores propuestos para el atributo `estado` de esa clase; conviene formalizarlos como enumeración en la especificación.

```mermaid
stateDiagram-v2
    [*] --> Pendiente: crear identificacion
    Pendiente --> Procesada: recibir resultado de inferencia
    Procesada --> Confirmada: confirmar() [modelo elegible y confianza suficiente]
    Procesada --> NoConfirmada: evaluar [criterios insuficientes]
    Confirmada --> [*]: resultado disponible para historial
    NoConfirmada --> [*]: resultado fuera del historial
```

`Confirmada` y `NoConfirmada` son estados terminales del proceso de identificación, no una indicación de que la instancia deba borrarse inmediatamente. El diagrama no introduce un estado de "Compartida": compartir en redes es una acción externa sobre un resultado y no modifica su confirmación.

## 8. Diagrama entidad-relación — Modelo lógico conceptual de BIOMA

> Propuesta conceptual de persistencia derivada del dominio, **no esquema SQL verificado**. `ResultadoInferencia` puede ser transitorio y no requiere necesariamente una tabla persistente. Las identificaciones no confirmadas no se vinculan al historial.

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
    IDENTIFICACION ||--|| RESULTADO_INFERENCIA : genera
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
        string estado
    }
    RESULTADO_INFERENCIA {
        string id PK
        string identificacionId FK
        float confianzaMaxima
        string origenInferencia
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

**Restricciones de negocio no expresadas por el ER:** para usuarios estándar el historial conserva como máximo 50 identificaciones confirmadas; el ingreso 51 elimina la más antigua. Las relaciones muchos-a-muchos de región/especie y resultado/especie requerirían tablas puente si se implementan en una base relacional.

## 9. Diagrama de actividad — Identificación y registro

> Mermaid aproxima la notación UML de actividad mediante `flowchart`, decisiones y subgrafos por responsable.

```mermaid
flowchart TD
    subgraph usuario[Usuario]
        A([Inicio]) --> B[Capturar imagen]
    end
    subgraph app[Aplicacion movil]
        C[Verificar calidad de imagen]
        D{Imagen valida?}
        E[Solicitar nueva captura]
        F{Hay conexion?}
        G{Paquete regional descargado?}
        H[Ejecutar inferencia offline]
        Z[Informar indisponibilidad]
        P[Mostrar resultado]
    end
    subgraph nube[Backend modular e IA]
        I[Ejecutar inferencia en nube]
        J[Consultar especie candidata]
        K{Especie medica?}
        L[Aplicar criterio 99 por ciento]
        M[Aplicar criterio 90 por ciento]
        N{Modelo elegible y confianza suficiente?}
        O[Confirmar identificacion]
        Q[Conservar en historial]
        R[Aplicar limite de historial estandar]
        S[Marcar no confirmada]
    end
    B --> C --> D
    D -->|No| E --> B
    D -->|Si| F
    F -->|Si| I
    F -->|No| G
    G -->|Si| H
    G -->|No| Z
    I --> J
    H --> J
    J --> K
    K -->|Si| L --> N
    K -->|No| M --> N
    N -->|Si| O --> Q --> R --> P
    N -->|No| S --> P
    Z --> T([Fin])
    P --> T
    style O fill:#ff5d00,color:#fff,stroke:#d94e00
```

## 10. Taller de consistencia entre diagramas

| Verificación | Resultado |
|---|---|
| Clases ↔ Secuencia | `ResultadoInferencia.obtenerMejorCandidato()`, `obtenerConfianza()`, `Especie.esDeImportanciaMedica()`, `Identificacion.validarConfianza()`, `confirmar()` y `Historial.agregarConfirmada()` / `aplicarLimite()` aparecen en ambos. |
| Clases ↔ Estados | `Identificacion.estado` existe. Sus valores se proponen como `Pendiente`, `Procesada`, `Confirmada` y `NoConfirmada`; falta tiparlos formalmente en la clase. |
| Arquitectura ↔ Secuencia | La aplicación móvil, el backend y el motor IA corresponden a los contenedores C4. |
| Requisitos ↔ Diagramas | CU-01 identificación; CU-02 historial; CU-04 identificación offline; CU-05 paquetes regionales; RNF-ESC-001 límite de historial. Confirmar los identificadores contra la versión final de la especificación. |
| Impacto de SC-001 | **No incorporado a la línea base**: compartir escaneos es una solicitud propuesta y debe reflejarse en estos diagramas solo si se acepta y se actualiza la especificación. |

### Puntos que conviene resolver antes de cerrar el diseño

1. **Exactitud del modelo:** `validarConfianza(umbral)` solo recibe el umbral de confianza; la verificación de exactitud del modelo (90 % o 99 %) necesita una responsabilidad explícita en el backend o un ajuste de operaciones del dominio.
2. **Identificación offline:** la secuencia 5 describe la ruta en nube; la ruta offline aparece en los diagramas de flujo y actividad. Si se requiere una secuencia para CU-04, debe elaborarse por separado.
3. **Historial avanzado:** `0..50` es correcto para el perfil estándar, pero no describe necesariamente el avanzado.
4. **Persistencia:** el diagrama ER es conceptual. Antes de convertirlo en SQL hay que resolver tablas puente, claves externas y si se persisten resultados no confirmados.
