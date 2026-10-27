Diagramas ADR - Ingeniería de Software

4. Diagrama de flujo con decisiones

flowchart TD
    ini([Inicio])
    val{"Monto mayor a cero?"}
    exc{"Excede el saldo?"}
    apl["Aplicar el abono"]
    err1["Monto invalido"]
    err2["Excede el saldo"]
    fin([Fin])

    ini --> val
    val -->|No| err1
    val -->|Si| exc
    exc -->|Si| err2
    exc -->|No| apl
    err1 --> fin
    err2 --> fin
    apl --> fin

    style apl fill:#ff5d00,color:#fff
    
5. Diagrama de secuencia

sequenceDiagram
    actor Rec as Recepcionista
    participant Web as App web
    participant Cob as Cobros
    participant Age as Agenda
    participant BD as Base de datos

    Rec->>Web: Registra un abono de 500
    Web->>Cob: abonar(cuenta, 500)
    Cob->>Age: Que servicio se atendio?
    Age-->>Cob: Consulta general
    Cob->>BD: Guarda el pago
    BD-->>Cob: Listo
    Cob-->>Web: Pago registrado
    Web-->>Rec: Muestra el nuevo saldo

6. Diagrama de clases

classDiagram
    class CuentaDePaciente {
        -double saldo
        -List~Pago~ pagos
        +abonar(monto) string
        +consultarSaldo() double
    }

    class Pago {
        -double monto
        -Date fecha
    }

    class Paciente {
        -string nombre
        -string especie
    }

    Paciente "1" --> "1" CuentaDePaciente : tiene
    CuentaDePaciente "1" --> "*" Pago : registra

7. Diagrama de estados

stateDiagram-v2
    [*] --> Agendada
    Agendada --> Confirmada: el dueno confirma
    Agendada --> Cancelada: se cancela a tiempo
    Confirmada --> Atendida: llega a consulta
    Confirmada --> NoAsistio: no se presenta

    Atendida --> [*]
    Cancelada --> [*]
    NoAsistio --> [*]

8. Diagrama entidad-relación

erDiagram
    PACIENTE ||--o{ CITA : tiene
    PACIENTE ||--|| CUENTA : tiene
    CITA ||--o| EXPEDIENTE : genera
    CUENTA ||--o{ PAGO : registra

    PACIENTE {
        int id
        string nombre
        string especie
    }

    CITA {
        int id
        date fecha
        string motivo
    }

    PAGO {
        int id
        decimal monto
        date fecha
    }

Registros de decisión y taller de diagramas

1. Diagrama de contexto — C4 Nivel 1

flowchart TD
    est(["Usuario estándar"])
    avan(["Usuario avanzado"])
    bioma["BIOMA<br/>Sistema de identificación de especies"]

    est -->|"Identifica especies y consulta resultados"| bioma
    avan -->|"Identifica especies y registra observaciones avanzadas"| bioma

    bioma -->|"Entrega identificaciones e información de especies"| est
    bioma -->|"Entrega resultados e historial autorizado"| avan

    style bioma fill:#ff5d00,color:#fff,stroke:#d94e00

2. Diagrama de contenedores — C4 Nivel 2

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

3. Diagrama de componentes — C4 Nivel 3

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
