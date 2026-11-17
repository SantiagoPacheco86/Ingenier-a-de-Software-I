# BIOMA

**Autor:** Santiago Pacheco Carrillo  
**Nombre del sistema:** BIOMA — Sistema de detección de flora y fauna local

## Descripción

BIOMA es un sistema orientado a la identificación de especies de flora y fauna local mediante la cámara de un teléfono inteligente.

El sistema utiliza modelos de inteligencia artificial entrenados con bases de datos regionales para analizar imágenes y proporcionar al usuario información relacionada con la especie identificada, incluyendo su nombre común y científico, región, nivel de confianza, importancia médica y especies similares.

El proyecto contempla dos tipos principales de usuario: **usuario estándar** y **usuario avanzado**, además de funciones como historial de identificaciones, reconocimiento de especies de importancia médica y disponibilidad de datos regionales para identificación offline.

## Documentación

Toda la documentación está en la carpeta [`doc`](./doc/).

| Etapa | Documento |
|---|---|
| Problema y alcance | [`Visión del producto`](./doc/vision-del-producto.md) |
| Elicitación | [`Requisitos iniciales`](./doc/requisitos-iniciales.md) · [`Guion y resultados de la entrevista`](./doc/guion-entrevista.md) |
| Requisitos | [`Especificación de requisitos v1.2`](./doc/especificacion-requisitos.md) · [`Diagrama de casos de uso`](./doc/diagramas/casos-de-uso.drawio.png) ([editable](./doc/diagramas/casos-de-uso.drawio)) |
| Arquitectura | [`Arquitectura C4`](./doc/arch/arquitectura-c4.md) · [`ADR-001 Monolito modular`](./doc/arch/adr-001-monolito-modular.md) · [`ADR-002 Tecnologías`](./doc/arch/adr-002-tecnologias.md) · [`ADR-003 Compartir nativo (propuesto)`](./doc/arch/adr-003-compartir-nativo.md) |
| Diseño UML | [`Modelo UML v2`](./doc/arch/modelo-uml.md) (clases, secuencia, estados, actividad, casos de uso, ER) · [`De los requisitos a las clases (v1)`](./doc/arch/DOO_S12S13.md) |
| Cambio | [`SC-001 Solicitud`](./doc/cambios/sc-001-compartir-escaneos-en-redes.md) · [`AI-001 Análisis de impacto`](./doc/cambios/ai-001-compartir-escaneos-en-redes.md) |

## Prototipo

El prototipo de BIOMA fue desarrollado en Figma y representa el flujo principal del caso de uso **CU-01 · Realizar identificación**, además de flujos alternos para imágenes inadecuadas e identificaciones con un nivel de confianza insuficiente.

### Archivo del proyecto en Figma

[Ver archivo de diseño de BIOMA en Figma](https://www.figma.com/design/N0iMemoAABgWZndAI7fMSr/Prototipo-BIOMA?node-id=0-1&t=kMmxGlxkqMvpMQp9-1)

### Prototipo navegable

[Ejecutar prototipo navegable de BIOMA](https://www.figma.com/proto/N0iMemoAABgWZndAI7fMSr/Prototipo-BIOMA?node-id=4-4&p=f&t=BahaH1r685r2VcuE-1&scaling=min-zoom&content-scaling=fixed&page-id=0%3A1&starting-point-node-id=4%3A4)

### Video

[Ver video BIOMA](https://youtu.be/3EXiWZ7SUwA)

## Flujo principal del prototipo

El prototipo permite recorrer el flujo principal de identificación:

1. Inicio.
2. Captura de una imagen mediante la cámara.
3. Vista previa de la fotografía.
4. Procesamiento de la identificación.
5. Presentación del resultado.
6. Consulta del historial de identificaciones.

También se contemplan flujos alternos para:

- Imágenes cuya calidad no permite realizar una identificación.
- Identificaciones que no alcanzan el nivel de confianza requerido y, por lo tanto, no se almacenan en el historial.

## Estado del proyecto

BIOMA se encuentra en fase de **diseño** para la materia **Ingeniería de Software I (SIS3407)**: requisitos especificados (v1.2), prototipo navegable en Figma, arquitectura C4 con decisiones registradas y modelo UML. **No existe implementación en código**; las tecnologías de ADR-002 son decisiones de diseño. La solicitud SC-001 está analizada y pendiente de aprobación.
