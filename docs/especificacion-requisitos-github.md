# Especificación de requisitos

**Sistema:** BIOMA --- Sistema de detección de flora y fauna local para
senderistas\
**Autor:** Santiago Pacheco Carrillo\
**Versión:** 1.0\
**Fecha de la última actualización:** 21/09/2026

------------------------------------------------------------------------

## 1. Propósito y alcance

**Propósito del documento:**

El propósito de este documento es especificar los requisitos del sistema
BIOMA, estableciendo de manera clara y verificable las funcionalidades,
restricciones y atributos de calidad que deberá cumplir el sistema
durante su desarrollo.

El documento está dirigido al equipo de desarrollo y a las personas
involucradas en la definición, revisión y validación del sistema.
Servirá como referencia para el diseño, implementación, pruebas y
posterior análisis de cambios de los requisitos del producto.

**Alcance del sistema:**

BIOMA es un sistema para la identificación de especies de flora y fauna
local mediante la cámara de un teléfono inteligente. El sistema utiliza
modelos de inteligencia artificial entrenados con bases de datos
regionales para analizar las imágenes proporcionadas y presentar al
usuario información relacionada con la especie identificada.

El sistema contempla:

-   Identificación de especies mediante la cámara de un teléfono
    inteligente.
-   Presentación de información de la especie identificada, incluyendo
    nombre común, nombre científico, región, nivel de riesgo o
    importancia médica, nivel de confianza y especies visualmente
    similares presentes en la región.
-   Historial de las especies identificadas por el usuario, incluyendo
    los datos asociados con cada identificación.
-   Recopilación y almacenamiento de datos de las identificaciones
    realizadas por usuarios avanzados con el propósito de apoyar la
    documentación de flora y fauna regional.
-   Reconocimiento offline de especies de importancia médica, siempre
    que el usuario haya descargado previamente la base de datos o modelo
    correspondiente a su región.

**Fuera del alcance:**

-   El sistema no almacena la imagen utilizada para realizar la
    detección cuando se trata de un usuario estándar.
-   El sistema no constituye una plataforma científica de validación
    colaborativa.
-   El sistema no garantiza una identificación definitiva de una
    especie.
-   El sistema no identifica especies que se encuentren fuera de las
    bases de datos o modelos disponibles para la región seleccionada.

------------------------------------------------------------------------

## 2. Usuarios y su contexto

BIOMA contempla dos tipos principales de usuario: el **usuario
estándar** y el **usuario avanzado**.

| Usuario | Qué hace hoy sin el sistema | Qué espera del sistema |
| --- | --- | --- |
| **Usuario estándar — excursionista, turista o persona interesada en la naturaleza** | Observa el organismo, registra o recuerda sus características, las compara con referencias disponibles, descarta posibles especies hasta obtener una identificación probable y, cuando es necesario, busca validación de una persona con mayor conocimiento. | Facilidad de uso y acceso rápido al reconocimiento mediante la cámara, con una experiencia similar a Shazam: apuntar y obtener una identificación sin requerir conocimientos especializados. Espera una respuesta rápida acompañada de fotografías, características visuales y datos que le permitan corroborar que la especie identificada corresponde con lo observado. |
| **Usuario avanzado — estudiantes, científicos, investigadores o entusiastas con conocimientos de flora y fauna** | Realiza observaciones y compara las características del organismo con referencias y conocimiento especializado para determinar una identificación. Posteriormente puede registrar y organizar manualmente sus observaciones para utilizarlas en documentación, investigación o trabajo de campo. | Acceso a información detallada y técnica de la especie identificada, como nombre científico, taxonomía, nivel de confianza, características distintivas y especies similares. Espera poder acceder preliminarmente a bases de datos y modelos en fase beta con mayor cobertura regional, además de registrar, organizar y documentar observaciones que puedan utilizarse como apoyo para estudios biológicos, monitoreo de especies o trabajo de campo. |


**Conflictos identificados entre usuarios:**

Existe un conflicto entre las prioridades del usuario estándar y las del
usuario avanzado.

El **usuario estándar** prioriza la rapidez y simplicidad del sistema y
espera identificar una especie casi inmediatamente después de apuntar la
cámara o proporcionar una imagen. La interacción debe requerir pocos
conocimientos especializados y permitir interpretar fácilmente el
resultado.

El **usuario avanzado**, en cambio, prioriza la calidad, precisión y
profundidad de la identificación. Puede aceptar un mayor tiempo de
procesamiento a cambio de analizar una mayor cantidad de especies,
obtener un nivel de confianza más fiable y disponer de información
técnica adicional que le permita contrastar y validar los resultados.

Este conflicto deberá considerarse durante la definición de los
requisitos del sistema para evitar que la búsqueda de mayor profundidad
de información perjudique la facilidad de uso esperada por el usuario
estándar o que la simplificación de la experiencia limite la información
requerida por los usuarios avanzados.

## 3. Requisitos funcionales

### 3.1 Resumen

| ID | Nombre | Prioridad | Origen |
| --- | --- | --- | --- |
| RF-001 | Identificación de especie | Imprescindible | Documento de requisitos inicial |
| RF-002 | Información de la especie | Imprescindible | Documento de requisitos inicial y entrevista de elicitación |
| RF-003 | Nivel de confianza | Imprescindible | Documento de requisitos inicial y entrevista de elicitación |
| RF-004 | Historial de identificaciones | Importante | Documento de requisitos inicial y entrevista de elicitación |
| RF-005 | Especie no reconocida | Imprescindible | Documento de requisitos inicial y entrevista de elicitación |

### 3.2 Fichas

#### RF-001 · Identificación de especie

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema identifica la especie de flora o fauna presente en una imagen capturada mediante la cámara del dispositivo móvil. |
| **Origen** | Documento de requisitos inicial. |
| **Prioridad** | Imprescindible |
| **Criterio de aceptación** | Al proporcionar una imagen de una especie incluida en el modelo disponible, el sistema presenta como resultado una identificación de dicha especie. |
| **Relacionado con** | RF-002, RF-003, RF-004, RF-005, RNF-REN-001 |

#### RF-002 · Información de la especie

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema muestra el nombre común, nombre científico, región y nivel de riesgo o importancia médica de la especie identificada. |
| **Origen** | Documento de requisitos inicial. La entrevista de elicitación confirmó el interés del usuario por consultar información descriptiva y de importancia médica de la especie. |
| **Prioridad** | Imprescindible |
| **Criterio de aceptación** | Al obtener una identificación, el sistema presenta el nombre común, nombre científico, región y nivel de riesgo o importancia médica registrados para la especie identificada. |
| **Relacionado con** | RF-001, RF-003 |

#### RF-003 · Nivel de confianza

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema muestra el nivel de confianza asociado a cada identificación realizada. |
| **Origen** | Documento de requisitos inicial. Confirmado durante la entrevista de elicitación, donde el usuario indicó que conocer la certeza de la identificación influye en la confianza para actuar sobre el resultado. |
| **Prioridad** | Imprescindible |
| **Criterio de aceptación** | Al obtener una identificación, el resultado presenta el nivel de confianza correspondiente a dicha identificación. |
| **Relacionado con** | RF-001, RF-005 |

#### RF-004 · Historial de identificaciones

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema registra las identificaciones realizadas por el usuario en su historial. |
| **Origen** | Documento de requisitos inicial. La entrevista de elicitación confirmó que conservar información de identificaciones anteriores aporta valor al usuario. |
| **Prioridad** | Importante |
| **Criterio de aceptación** | Después de completar una identificación, esta aparece en el historial correspondiente al usuario con la información asociada que el sistema conserva. |
| **Relacionado con** | RF-001, RNF-ESC-001 |

#### RF-005 · Especie no reconocida

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema informa que no fue posible identificar la especie cuando esta no se encuentra dentro del modelo disponible. |
| **Origen** | Documento de requisitos inicial. La entrevista de elicitación confirmó la necesidad de comunicar al usuario cuando una identificación no tiene suficiente certeza, aunque también reveló la necesidad de evaluar la presentación de posibles aproximaciones. |
| **Prioridad** | Imprescindible |
| **Criterio de aceptación** | Al analizar una especie que no pueda ser identificada mediante el modelo disponible, el sistema informa al usuario que no fue posible realizar la identificación y no presenta una especie como resultado confirmado. |
| **Relacionado con** | RF-001, RF-003 |

---

## 4. Requisitos no funcionales

### 4.1 Resumen

| ID | Atributo | Nombre | Prioridad | Origen |
| --- | --- | --- | --- | --- |
| RNF-REN-001 | Rendimiento | Tiempo de identificación | Imprescindible | Documento de requisitos inicial |
| RNF-SEG-001 | Seguridad | Protección de credenciales | Imprescindible | Documento de requisitos inicial |
| RNF-ESC-001 | Escalabilidad / Capacidad | Capacidad del historial | Importante | Documento de requisitos inicial; supuesto pendiente de validación |

### 4.2 Fichas

#### RNF-REN-001 · Tiempo de identificación

| Campo | Contenido |
| --- | --- |
| **Atributo de calidad** | Rendimiento |
| **Descripción** | El sistema presenta el resultado de una identificación en un tiempo máximo de 15 segundos desde que el usuario solicita la identificación. |
| **Métrica** | Tiempo transcurrido desde la solicitud de identificación hasta la presentación del resultado: máximo 15 segundos. Las condiciones específicas de medición quedan pendientes de definir. |
| **Origen** | Documento de requisitos inicial. El límite de 15 segundos no fue validado durante la entrevista de elicitación. |
| **Prioridad** | Imprescindible |
| **Por qué importa** | La identificación se realiza durante la observación de flora o fauna y un tiempo de respuesta elevado puede dificultar que el usuario consulte el resultado durante su recorrido. |
| **Afecta a** | RF-001, RF-002, RF-003, RF-005 |

#### RNF-SEG-001 · Protección de credenciales

| Campo | Contenido |
| --- | --- |
| **Atributo de calidad** | Seguridad |
| **Descripción** | Las credenciales persistidas por el sistema no se almacenan en texto legible. |
| **Métrica** | El 100 % de las credenciales persistidas por el sistema se encuentran protegidas y ninguna puede consultarse directamente en texto plano desde el almacenamiento. |
| **Origen** | Documento de requisitos inicial, derivado de la necesidad de proteger la información de autenticación de los usuarios. |
| **Prioridad** | Imprescindible |
| **Por qué importa** | El almacenamiento de credenciales en texto legible permitiría exponer información de autenticación de los usuarios en caso de acceso no autorizado a los datos almacenados. |
| **Afecta a** | Funciones de registro, autenticación y administración de cuentas de usuario. |

#### RNF-ESC-001 · Capacidad del historial

| Campo | Contenido |
| --- | --- |
| **Atributo de calidad** | Escalabilidad / Capacidad |
| **Descripción** | El historial de un usuario estándar conserva un máximo de 50 identificaciones. |
| **Métrica** | Cantidad máxima de identificaciones disponibles simultáneamente en el historial de un usuario estándar: 50. |
| **Origen** | Documento de requisitos inicial. El límite de 50 identificaciones es un supuesto pendiente de validación. |
| **Prioridad** | Importante |
| **Por qué importa** | Establecer un límite define la capacidad prevista del historial para un usuario estándar y permite comprobar el comportamiento del sistema al alcanzar dicha capacidad. |
| **Afecta a** | RF-004 |

---


## 5. Casos de uso

------------------------------------------------------------------------

## 6. Trazabilidad

  Requisito   Origen   Caso de uso   Elemento del prototipo
  ----------- -------- ------------- ------------------------
                                     

------------------------------------------------------------------------

## 7. Registro de cambios

  Fecha   Requisito   Qué cambió   Por qué
  ------- ----------- ------------ ---------
                                   

------------------------------------------------------------------------

## Antes de entregar

-   [ ] Todos los requisitos tienen identificador único y ninguno está
    repetido
-   [ ] Cada requisito expresa una sola idea
-   [ ] Cada requisito funcional tiene criterio de aceptación
    comprobable
-   [ ] Cada requisito no funcional tiene una métrica, no solo un
    adjetivo
-   [ ] El campo Origen distingue lo confirmado por el cliente de lo que
    sigo suponiendo
-   [ ] Hay al menos un requisito no funcional por cada atributo de
    calidad que impone mi tipo de sistema
-   [ ] Ningún requisito impone una solución técnica
-   [ ] Todos los requisitos caben dentro del alcance declarado
-   [ ] La tabla de trazabilidad está completa
-   [ ] Mi dupla revisó el documento y su revisión está registrada
-   [ ] Borré los ejemplos y las instrucciones en cursiva
