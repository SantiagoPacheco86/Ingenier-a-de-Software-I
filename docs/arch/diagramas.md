flowchart TD
    est(["Usuario estándar"])
    avan(["Usuario avanzado"])
    bioma["BIOMA<br/>Sistema de identificación de especies"]

    est -->|"Identifica especies y consulta resultados"| bioma
    avan -->|"Identifica especies y registra observaciones avanzadas"| bioma

    bioma -->|"Entrega identificaciones e información de especies"| est
    bioma -->|"Entrega resultados e historial autorizado"| avan

    style bioma fill:#ff5d00,color:#fff,stroke:#d94e00
