# BIOMA

**Autor:** Santiago Pacheco Carrillo  
**Nombre del sistema:** BIOMA — Sistema de detección de flora y fauna local

## Descripción

BIOMA es un sistema orientado a la identificación de especies de flora y fauna local mediante la cámara de un teléfono inteligente.

El sistema utiliza modelos de inteligencia artificial entrenados con bases de datos regionales para analizar imágenes y proporcionar al usuario información relacionada con la especie identificada, incluyendo su nombre común y científico, región, nivel de confianza, importancia médica y especies similares.

El proyecto contempla dos tipos principales de usuario: **usuario estándar** y **usuario avanzado**, además de funciones como historial de identificaciones, reconocimiento de especies de importancia médica y disponibilidad de datos regionales para identificación offline.

## Documentación

La documentación del proyecto se encuentra en la carpeta [`docs`](./docs/) del repositorio.

Entre los documentos principales se encuentran:

- [`Especificación de requisitos`](./docs/especificacion-requisitos-github.md)
- [`Visión del producto`](./docs/vision-del-producto.md)
- [`Requisitos iniciales`](./docs/requisitos-iniciales.md)
- [`Guía de redacción de requisitos`](./docs/guia-redaccion-requisitos.md)

El diagrama de casos de uso y sus archivos asociados se encuentran en:

- [`docs/diagramas`](./docs/diagramas/)

## Prototipo

El prototipo de BIOMA fue desarrollado en Figma y representa el flujo principal del caso de uso **CU-01 · Realizar identificación**, además de flujos alternos para imágenes inadecuadas e identificaciones con un nivel de confianza insuficiente.

### Archivo del proyecto en Figma

[Ver archivo de diseño de BIOMA en Figma](https://www.figma.com/design/N0iMemoAABgWZndAI7fMSr/Prototipo-BIOMA?node-id=0-1&t=kMmxGlxkqMvpMQp9-1)

### Prototipo navegable

[Ejecutar prototipo navegable de BIOMA](https://www.figma.com/proto/N0iMemoAABgWZndAI7fMSr/Prototipo-BIOMA?node-id=4-4&p=f&t=BahaH1r685r2VcuE-1&scaling=min-zoom&content-scaling=fixed&page-id=0%3A1&starting-point-node-id=4%3A4)

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

BIOMA se encuentra actualmente en fase de **especificación de requisitos y prototipado** para la materia **Ingeniería de Software I (SIS3407)**.
