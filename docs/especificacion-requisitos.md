# Especificación de requisitos

**Sistema:** BIOMA — Sistema de detección de flora y fauna local para senderistas  
**Autor:** Santiago Pacheco Carrillo  
**Versión:** 1.1  
**Fecha de la última actualización:** 24/09/2026

---

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
local mediante la cámara de un teléfono inteligente. El sistema analiza
las imágenes proporcionadas mediante modelos de identificación entrenados
con datos regionales y presenta al usuario información relacionada con
la especie identificada.

Para las especies generales incluidas en el modelo, BIOMA establece una
precisión mínima del modelo del 90 %. Una identificación individual
requiere un nivel de confianza mínimo del 90 % para presentarse como
identificación confirmada.

Para especies clasificadas como de importancia médica, BIOMA establece
una precisión mínima del modelo del 99 %. Una identificación individual
de una especie de importancia médica requiere un nivel de confianza
mínimo del 99 % para presentarse como identificación confirmada.

Cuando una identificación no alcance el nivel de confianza requerido,
el sistema deberá comunicar la incertidumbre al usuario y podrá presentar
la especie con mayor nivel de confianza únicamente como una posible
identificación, sin presentarla como resultado confirmado.

El sistema contempla:

- Identificación de especies mediante la cámara de un teléfono inteligente.
- Presentación de información de la especie identificada, incluyendo
  nombre común, nombre científico, región, nivel de riesgo o importancia
  médica y nivel de confianza.
- Presentación de especies visualmente similares presentes en la región.
- Historial de las especies identificadas por el usuario, incluyendo los
  datos asociados con cada identificación.
- Recopilación y almacenamiento de datos de las identificaciones
  realizadas por usuarios avanzados con el propósito de apoyar la
  documentación de flora y fauna regional.
- Reconocimiento offline de especies de importancia médica, siempre que
  el usuario haya descargado previamente los datos correspondientes a su
  región.
- Descarga previa de los datos regionales necesarios para realizar
  identificaciones offline de especies de importancia médica.
- Comunicación explícita de identificaciones que no alcancen el nivel
  de confianza requerido.
- Presentación de la especie con mayor nivel de confianza como posible
  identificación cuando no se alcance el umbral requerido.

**Fuera del alcance:**

- El sistema no almacena la imagen utilizada para realizar la detección
  cuando se trata de un usuario estándar.
- El sistema no constituye una plataforma científica de validación
  colaborativa.
- El sistema no garantiza una identificación definitiva cuando no se
  alcance el nivel de confianza establecido.
- El sistema no presenta como identificación confirmada una especie que
  no alcance el nivel de confianza correspondiente.
- El sistema no identifica como confirmadas especies que se encuentren
  fuera de los datos o modelos disponibles para la región seleccionada.

---

## 2. Usuarios y su contexto

BIOMA contempla dos tipos principales de usuario: el **usuario estándar**
y el **usuario avanzado**.

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

---

## 3. Requisitos funcionales

### 3.1 Resumen

| ID | Nombre | Prioridad | Origen |
| --- | --- | --- | --- |
| RF-001 | Identificación de especie | Imprescindible | Documento de requisitos inicial |
| RF-002 | Información de la especie | Imprescindible | Documento de requisitos inicial y entrevista de elicitación |
| RF-003 | Nivel de confianza | Imprescindible | Documento de requisitos inicial y entrevista de elicitación |
| RF-004 | Historial de identificaciones | Importante | Documento de requisitos inicial y entrevista de elicitación |
| RF-005 | Especie no reconocida | Imprescindible | Documento de requisitos inicial |
| RF-006 | Especies visualmente similares | Importante | Visión del producto |
| RF-007 | Registro de observaciones de usuario avanzado | Importante | Visión del producto |
| RF-008 | Identificación offline | Imprescindible | Visión del producto y entrevista de elicitación |
| RF-009 | Descarga de datos regionales para uso offline | Importante | Derivado de RF-008 |
| RF-010 | Identificación con baja confianza | Imprescindible | Entrevista de elicitación y especificación |
| RF-011 | Posible identificación | Importante | Entrevista de elicitación |
| RF-012 | Imagen inadecuada para identificación | Importante | Visión del producto y entrevista de elicitación |

### 3.2 Fichas

#### RF-001 · Identificación de especie

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema identifica la especie de flora o fauna presente en una imagen capturada mediante la cámara del dispositivo móvil. |
| **Origen** | Documento de requisitos inicial. |
| **Prioridad** | Imprescindible |
| **Criterio de aceptación** | Al proporcionar una imagen de una especie incluida en el modelo disponible, el sistema procesa la imagen y genera un resultado de identificación. |
| **Relacionado con** | RF-002, RF-003, RF-005, RF-006, RF-010, RF-011, RF-012, RNF-CON-001, RNF-CON-002, RNF-CON-003, RNF-REN-001 |

#### RF-002 · Información de la especie

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema muestra el nombre común, nombre científico, región y nivel de riesgo o importancia médica de la especie identificada. |
| **Origen** | Documento de requisitos inicial. La entrevista de elicitación confirmó el interés por consultar información descriptiva y de importancia médica. |
| **Prioridad** | Imprescindible |
| **Criterio de aceptación** | Al obtener una identificación confirmada, el sistema presenta el nombre común, nombre científico, región y nivel de riesgo o importancia médica registrados para la especie. |
| **Relacionado con** | RF-001, RF-003, RF-006 |

#### RF-003 · Nivel de confianza

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema muestra el nivel de confianza asociado a cada resultado de identificación. |
| **Origen** | Documento de requisitos inicial y entrevista de elicitación. El entrevistado indicó que conocer la certeza del resultado influye en la confianza para actuar sobre la identificación. |
| **Prioridad** | Imprescindible |
| **Criterio de aceptación** | Después de procesar una imagen, el resultado presenta el porcentaje de confianza asociado a la identificación obtenida. |
| **Relacionado con** | RF-001, RF-005, RF-010, RF-011 |

#### RF-004 · Historial de identificaciones

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema registra en el historial únicamente las identificaciones que alcanzan el nivel de confianza requerido para presentarse como confirmadas. |
| **Origen** | Documento de requisitos inicial. La entrevista de elicitación confirmó que conservar información de identificaciones anteriores aporta valor al usuario. La exclusión de identificaciones no confirmadas fue definida durante la especificación. |
| **Prioridad** | Importante |
| **Criterio de aceptación** | Cuando una identificación alcanza el nivel de confianza requerido para presentarse como confirmada, el sistema la registra en el historial. Si el resultado se presenta únicamente como posible identificación por no alcanzar el nivel de confianza requerido, el sistema no lo registra en el historial. |
| **Relacionado con** | RF-001, RF-003, RF-010, RF-011, RNF-SEG-001, RNF-ESC-001 |

#### RF-005 · Especie no reconocida

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema informa que no fue posible identificar la especie cuando esta no se encuentra dentro del modelo disponible. |
| **Origen** | Documento de requisitos inicial. |
| **Prioridad** | Imprescindible |
| **Criterio de aceptación** | Al analizar una especie que no pueda ser identificada mediante el modelo disponible, el sistema informa que no fue posible realizar la identificación y no presenta una especie como resultado confirmado. |
| **Relacionado con** | RF-001, RF-003, RF-010, RF-011 |

#### RF-006 · Especies visualmente similares

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema muestra especies visualmente similares presentes en la región de la especie identificada. |
| **Origen** | Visión del producto. |
| **Prioridad** | Importante |
| **Criterio de aceptación** | Al consultar el resultado de una especie que cuenta con especies similares registradas para la región, el sistema muestra dichas especies como referencias adicionales. |
| **Relacionado con** | RF-001, RF-002 |

#### RF-007 · Registro de observaciones de usuario avanzado

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema registra los datos asociados a las identificaciones realizadas por usuarios avanzados para su posterior consulta y documentación. |
| **Origen** | Visión del producto. |
| **Prioridad** | Importante |
| **Criterio de aceptación** | Después de que un usuario avanzado realiza una identificación, los datos asociados quedan registrados y disponibles para su consulta posterior. |
| **Relacionado con** | RF-001, RF-004, RNF-SEG-001 |

#### RF-008 · Identificación offline

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema identifica especies de importancia médica sin conexión a Internet cuando el usuario dispone previamente de los datos correspondientes a su región. |
| **Origen** | Visión del producto y entrevista de elicitación. El entrevistado identificó como relevante disponer offline de información relacionada con especies de importancia médica. |
| **Prioridad** | Imprescindible |
| **Criterio de aceptación** | Con el dispositivo sin conexión a Internet y con los datos regionales previamente disponibles, el sistema procesa una imagen correspondiente a una especie de importancia médica incluida en dichos datos y genera un resultado de identificación. |
| **Relacionado con** | RF-001, RF-003, RF-009, RF-010, RF-012, RNF-CON-003 |

#### RF-009 · Descarga de datos regionales para uso offline

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema permite al usuario descargar los datos de una región necesarios para realizar identificaciones offline de especies de importancia médica. |
| **Origen** | Derivado de RF-008 y de la Visión del producto. |
| **Prioridad** | Importante |
| **Criterio de aceptación** | Cuando el usuario selecciona una región disponible y solicita su descarga con conexión a Internet, el sistema almacena los datos necesarios y posteriormente los reconoce como disponibles para identificación offline. |
| **Relacionado con** | RF-008 |

#### RF-010 · Identificación con baja confianza

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema informa al usuario cuando una identificación no alcanza el nivel mínimo de confianza requerido para presentarse como confirmada. |
| **Origen** | Entrevista de elicitación y especificación. La entrevista confirmó la necesidad de comunicar la incertidumbre; los umbrales fueron definidos posteriormente durante la especificación. |
| **Prioridad** | Imprescindible |
| **Criterio de aceptación** | Si una identificación general obtiene una confianza inferior al 90 %, o una identificación de importancia médica obtiene una confianza inferior al 99 %, el sistema informa que el resultado no alcanza la confianza requerida y no lo presenta como identificación confirmada. |
| **Relacionado con** | RF-001, RF-003, RF-005, RF-011, RNF-CON-002, RNF-CON-003 |

#### RF-011 · Posible identificación

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema muestra la especie con mayor nivel de confianza como posible identificación cuando el resultado no alcanza el umbral requerido para presentarse como confirmado. |
| **Origen** | Entrevista de elicitación. El entrevistado indicó que, ante una identificación incierta, espera conocer la mejor aproximación disponible sin ocultar la incertidumbre. |
| **Prioridad** | Importante |
| **Criterio de aceptación** | Cuando existe al menos una especie candidata pero ninguna alcanza el umbral correspondiente, el sistema muestra la candidata con mayor confianza identificándola explícitamente como posible identificación y muestra su nivel de confianza. |
| **Relacionado con** | RF-003, RF-005, RF-010 |

#### RF-012 · Imagen inadecuada para identificación

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema solicita una nueva imagen y muestra recomendaciones para mejorar la captura cuando la imagen proporcionada no tiene calidad suficiente para realizar una identificación. |
| **Origen** | Visión del producto. La entrevista de elicitación reforzó este requisito al identificar fotografías con contraluz, poca iluminación o colores poco visibles como una dificultad del proceso actual. |
| **Prioridad** | Importante |
| **Criterio de aceptación** | Cuando una imagen no cumple las condiciones mínimas necesarias para realizar la identificación, el sistema no presenta una especie como resultado, solicita una nueva captura y muestra recomendaciones para mejorar la imagen. |
| **Relacionado con** | RF-001, RF-008, RF-010, RNF-CON-002, RNF-CON-003 |

---

## 4. Requisitos no funcionales

### 4.1 Resumen

| ID | Atributo | Nombre | Prioridad | Origen |
| --- | --- | --- | --- | --- |
| RNF-CON-001 | Confiabilidad | Calidad de datos de referencia | Imprescindible | Derivado del tipo de sistema |
| RNF-CON-002 | Confiabilidad | Precisión general de identificación | Imprescindible | Derivado del tipo de sistema y especificación |
| RNF-CON-003 | Confiabilidad | Precisión en especies de importancia médica | Imprescindible | Entrevista de elicitación y especificación |
| RNF-REN-001 | Rendimiento | Tiempo de identificación | Imprescindible | Documento de requisitos inicial |
| RNF-SEG-001 | Seguridad | Protección de datos | Imprescindible | Derivado del tipo de sistema |
| RNF-ESC-001 | Escalabilidad | Capacidad del historial | Importante | Documento de requisitos inicial y especificación |

### 4.2 Fichas

#### RNF-CON-001 · Calidad de datos de referencia

| Campo | Contenido |
| --- | --- |
| **Atributo de calidad** | Confiabilidad |
| **Descripción** | Los datos utilizados como referencia por el sistema corresponden a especies identificadas y clasificadas antes de su incorporación al conjunto de datos disponible. |
| **Métrica** | El 100 % de las especies incorporadas al conjunto de datos cuenta con una identificación y clasificación asociada. |
| **Origen** | Derivado del tipo de sistema: la identificación depende de datos representativos y correctamente clasificados. |
| **Prioridad** | Imprescindible |
| **Por qué importa** | Datos incorrectamente clasificados pueden provocar identificaciones erróneas y reducir la confiabilidad de los resultados. |
| **Afecta a** | RF-001, RF-002, RF-003, RF-005, RF-006, RF-008, RF-010, RF-011 |

#### RNF-CON-002 · Precisión general de identificación

| Campo | Contenido |
| --- | --- |
| **Atributo de calidad** | Confiabilidad |
| **Descripción** | El modelo alcanza una precisión mínima del 90 % en la identificación general de especies incluidas en el modelo disponible. |
| **Métrica** | Al menos el 90 % de las identificaciones realizadas sobre un conjunto de imágenes de prueba previamente clasificadas de especies generales debe coincidir con la especie correcta. |
| **Origen** | Derivado del tipo de sistema. El umbral mínimo del 90 % fue establecido durante la especificación de requisitos. |
| **Prioridad** | Imprescindible |
| **Por qué importa** | Una precisión insuficiente reduce la confiabilidad del sistema y puede proporcionar información incorrecta sobre las especies observadas. |
| **Afecta a** | RF-001, RF-003, RF-005, RF-010, RF-011 |

#### RNF-CON-003 · Precisión en especies de importancia médica

| Campo | Contenido |
| --- | --- |
| **Atributo de calidad** | Confiabilidad |
| **Descripción** | El modelo alcanza una precisión mínima del 99 % en la identificación de especies clasificadas como de importancia médica e incluidas en el modelo disponible. |
| **Métrica** | Al menos el 99 % de las identificaciones realizadas sobre un conjunto de imágenes de prueba previamente clasificadas de especies de importancia médica debe coincidir con la especie correcta. |
| **Origen** | Entrevista de elicitación y especificación. La entrevista estableció la necesidad de una certeza mayor para especies de importancia médica y el umbral del 99 % fue definido posteriormente durante la especificación. |
| **Prioridad** | Imprescindible |
| **Por qué importa** | Una identificación incorrecta de una especie de importancia médica puede llevar al usuario a interpretar incorrectamente el riesgo asociado con el organismo observado. |
| **Afecta a** | RF-001, RF-002, RF-003, RF-005, RF-008, RF-010, RF-011 |

#### RNF-REN-001 · Tiempo de identificación

| Campo | Contenido |
| --- | --- |
| **Atributo de calidad** | Rendimiento |
| **Descripción** | El sistema presenta el resultado de una identificación en un tiempo máximo de 15 segundos desde que el usuario solicita la identificación. |
| **Métrica** | Tiempo transcurrido desde la solicitud de identificación hasta la presentación del resultado: máximo 15 segundos. |
| **Origen** | Documento de requisitos inicial. |
| **Prioridad** | Imprescindible |
| **Por qué importa** | Un tiempo de procesamiento elevado reduce la utilidad del reconocimiento durante actividades en campo. |
| **Afecta a** | RF-001, RF-002, RF-003, RF-005, RF-008, RF-010, RF-011 |

#### RNF-SEG-001 · Protección de datos

| Campo | Contenido |
| --- | --- |
| **Atributo de calidad** | Seguridad |
| **Descripción** | El sistema restringe el acceso a los datos privados asociados a una identificación al usuario propietario de dichos datos. |
| **Métrica** | En el 100 % de las pruebas de acceso realizadas con una cuenta diferente a la propietaria, el sistema impide consultar los datos privados asociados a la identificación. |
| **Origen** | Derivado del tipo de sistema: los registros pueden contener información asociada al usuario o a la ubicación donde se realizó una observación. |
| **Prioridad** | Imprescindible |
| **Por qué importa** | El acceso no autorizado puede comprometer la privacidad del usuario y revelar información sobre la ubicación de determinadas especies. |
| **Afecta a** | RF-004, RF-007 |

#### RNF-ESC-001 · Capacidad del historial

| Campo | Contenido |
| --- | --- |
| **Atributo de calidad** | Escalabilidad |
| **Descripción** | El historial de un usuario estándar conserva un máximo de 50 identificaciones y, al registrar una nueva identificación cuando se alcanza este límite, elimina la identificación más antigua. |
| **Métrica** | El historial mantiene un máximo de 50 identificaciones simultáneamente. Al registrar la identificación número 51, se elimina la identificación con mayor antigüedad y el historial permanece con 50 registros. |
| **Origen** | Documento de requisitos inicial. El comportamiento al alcanzar el límite fue definido durante la especificación de requisitos. |
| **Prioridad** | Importante |
| **Por qué importa** | Establecer un límite permite controlar la cantidad de identificaciones conservadas para un usuario estándar y define de manera predecible el comportamiento del historial cuando alcanza su capacidad máxima. |
| **Afecta a** | RF-004 |

---

## 5. Casos de uso

El diagrama de casos de uso de BIOMA representa los actores que interactúan
con el sistema y los principales casos de uso asociados a cada uno.

El diagrama se encuentra disponible en la carpeta `docs/diagramas/` del
repositorio en los siguientes formatos:

- `casos-de-uso.drawio`: archivo editable del diagrama.
- `casos-de-uso.drawio.png`: versión en imagen para su visualización directa
  desde el repositorio.

Los casos de uso representados en el diagrama se detallan a continuación y
se relacionan con los requisitos funcionales que realizan.

### 5.1 Detalle

| ID | Nombre | Actor principal | Requisitos que realiza |
| --- | --- | --- | --- |
| CU-01 | Realizar identificación | Usuario estándar / Usuario avanzado | RF-001, RF-002, RF-003, RF-004, RF-005, RF-006, RF-010, RF-011, RF-012 |
| CU-02 | Consultar historial de identificaciones | Usuario estándar / Usuario avanzado | RF-004 |
| CU-03 | Registrar observación avanzada | Usuario avanzado | RF-007 |
| CU-04 | Realizar identificación offline | Usuario estándar / Usuario avanzado | RF-001, RF-002, RF-003, RF-004, RF-005, RF-008, RF-010, RF-011, RF-012 |
| CU-05 | Descargar datos regionales para uso offline | Usuario estándar / Usuario avanzado | RF-009 |

### 5.2 Caso de uso principal

#### CU-01 · Realizar identificación

| Campo | Contenido |
| --- | --- |
| **Actor principal** | Usuario estándar / Usuario avanzado |
| **Objetivo** | Identificar una especie de flora o fauna observada mediante una imagen capturada con la cámara del dispositivo móvil y consultar la información asociada al resultado. |
| **Precondición** | El sistema dispone de un modelo de identificación correspondiente a la región seleccionada. |
| **Escenario principal** | 1. El usuario accede a la función de identificación.<br>2. El usuario apunta la cámara del dispositivo hacia el organismo que desea identificar.<br>3. El usuario captura una imagen del organismo.<br>4. El sistema verifica que la imagen tenga condiciones suficientes para realizar la identificación.<br>5. El sistema procesa la imagen utilizando el modelo disponible para la región seleccionada.<br>6. El sistema obtiene la especie candidata y determina el nivel de confianza del resultado.<br>7. El sistema verifica que el nivel de confianza alcance el umbral correspondiente al tipo de especie.<br>8. El sistema presenta la especie como identificación confirmada.<br>9. El sistema muestra el nivel de confianza de la identificación.<br>10. El sistema muestra el nombre común, nombre científico, región y nivel de riesgo o importancia médica de la especie identificada.<br>11. El sistema muestra las especies visualmente similares registradas para la región, cuando existan.<br>12. El sistema registra la identificación confirmada en el historial del usuario. |
| **Flujos alternos** | **4a. La imagen no tiene calidad suficiente:** el sistema informa que la imagen no es adecuada, muestra recomendaciones para mejorar la captura y solicita una nueva imagen. El flujo regresa al paso 2.<br><br>**6a. La especie no se encuentra dentro del modelo disponible:** el sistema informa que no fue posible realizar la identificación, no presenta ninguna especie como identificación confirmada y no registra el resultado en el historial. El caso de uso finaliza.<br><br>**7a. Una especie general obtiene un nivel de confianza inferior al 90 %:** el sistema informa que el resultado no alcanza la confianza requerida. Si existe una especie candidata, muestra la de mayor confianza como posible identificación junto con su porcentaje de confianza. El sistema indica que no se trata de una identificación confirmada y no registra el resultado en el historial. El caso de uso finaliza.<br><br>**7b. Una especie de importancia médica obtiene un nivel de confianza inferior al 99 %:** el sistema informa que el resultado no alcanza la confianza requerida para una especie de importancia médica. Si existe una especie candidata, muestra la de mayor confianza como posible identificación junto con su porcentaje de confianza. El sistema indica que no se trata de una identificación confirmada y no registra el resultado en el historial. El caso de uso finaliza.<br><br>**11a. No existen especies visualmente similares registradas para la región:** el sistema omite la presentación de especies similares y continúa con el paso 12.<br><br>**12a. El historial del usuario estándar ya contiene 50 identificaciones:** el sistema elimina la identificación más antigua, registra la nueva identificación confirmada y mantiene el historial con un máximo de 50 registros. |
| **Postcondición** | Si el resultado alcanza el nivel de confianza requerido, la especie queda presentada como identificación confirmada y registrada en el historial. Si el resultado no alcanza el nivel requerido o no puede realizarse la identificación, no se registra en el historial. |
| **Requisitos que realiza** | RF-001, RF-002, RF-003, RF-004, RF-005, RF-006, RF-010, RF-011, RF-012, RNF-CON-001, RNF-CON-002, RNF-CON-003, RNF-REN-001, RNF-ESC-001 |

---

## 6. Trazabilidad

La siguiente tabla relaciona cada requisito del sistema con su origen, los
casos de uso en los que participa y las pantallas del prototipo V1 en las
que actualmente puede observarse su comportamiento.

El estado **Vigente** indica que el requisito se encuentra representado
en el prototipo V1. El estado **Pendiente** indica que el requisito forma
parte de la especificación del sistema, pero su comportamiento todavía
no se encuentra representado o no puede verificarse completamente en
la versión actual del prototipo.

| Requisito | Origen | Caso de uso | Pantalla del prototipo | Estado |
| --- | --- | --- | --- | --- |
| RF-001 | Documento de requisitos inicial | CU-01, CU-04 | P02, P03, P04, P05 | Vigente |
| RF-002 | Documento de requisitos inicial y entrevista de elicitación | CU-01, CU-04 | P05 | Vigente |
| RF-003 | Documento de requisitos inicial y entrevista de elicitación | CU-01, CU-04 | P05, A-02 | Vigente |
| RF-004 | Documento de requisitos inicial y entrevista de elicitación | CU-01, CU-02, CU-04 | P05, P06, A-02 | Vigente |
| RF-005 | Documento de requisitos inicial | CU-01, CU-04 | — | Pendiente |
| RF-006 | Visión del producto | CU-01 | P05 | Vigente |
| RF-007 | Visión del producto | CU-03 | — | Pendiente |
| RF-008 | Visión del producto y entrevista de elicitación | CU-04 | — | Pendiente |
| RF-009 | Derivado de RF-008 | CU-05 | — | Pendiente |
| RF-010 | Entrevista de elicitación y especificación | CU-01, CU-04 | A-02 | Vigente |
| RF-011 | Entrevista de elicitación | CU-01, CU-04 | A-02 | Vigente |
| RF-012 | Visión del producto y entrevista de elicitación | CU-01, CU-04 | A-01 | Vigente |
| RNF-CON-001 | Derivado del tipo de sistema | CU-01, CU-04 | — | Pendiente |
| RNF-CON-002 | Derivado del tipo de sistema y especificación | CU-01 | — | Pendiente |
| RNF-CON-003 | Entrevista de elicitación y especificación | CU-01, CU-04 | — | Pendiente |
| RNF-REN-001 | Documento de requisitos inicial | CU-01, CU-04 | P04 | Pendiente |
| RNF-SEG-001 | Derivado del tipo de sistema | CU-02, CU-03 | — | Pendiente |
| RNF-ESC-001 | Documento de requisitos inicial y especificación | CU-01, CU-02 | P06 | Pendiente |

---
## 7. Revisión de la dupla

La especificación de requisitos fue revisada por la dupla antes de la entrega.
Las observaciones recibidas se analizaron con el propósito de identificar
inconsistencias, requisitos faltantes y aspectos que requieren mayor
clarificación.

Las observaciones aceptadas no implican necesariamente una modificación
inmediata del alcance. Los cambios identificados se incorporarán o resolverán
durante la siguiente revisión de la especificación.

| ID | Observación de la dupla | Evaluación | Acción propuesta | Estado |
| --- | --- | --- | --- | --- |
| RD-001 | No existe un requisito no funcional de usabilidad, aunque la facilidad de uso forma parte de las expectativas del usuario estándar. | **Válida.** La facilidad de uso aparece como una característica relevante del sistema, pero actualmente no existe un RNF con una métrica que permita verificarla. | Definir `RNF-USA-001` con una condición o métrica comprobable de usabilidad durante la siguiente revisión. | Pendiente |
| RD-002 | Se mencionan cuentas y propiedad de información o fotografías, pero no existen requisitos funcionales que definan el comportamiento de las cuentas. | **Parcialmente válida.** Existe una inconsistencia si la documentación presupone la existencia de cuentas sin especificar su comportamiento. Sin embargo, antes de crear nuevos requisitos debe determinarse si la gestión de cuentas pertenece realmente al alcance del sistema. | Revisar las referencias a cuentas. Si forman parte del alcance, definir los requisitos correspondientes; de lo contrario, eliminar o reformular dichas referencias. | Pendiente de decisión |
| RD-003 | No queda suficientemente claro por qué se almacenan las fotografías y datos de los usuarios avanzados ni cuál es la finalidad de conservar esta información. | **Válida.** El registro de observaciones avanzadas necesita una finalidad y comportamiento más claramente delimitados para evitar interpretaciones distintas. | Revisar `RF-007` y el alcance relacionado con usuarios avanzados para especificar qué información se conserva, con qué finalidad y dentro de qué límites. | Pendiente |
| RD-004 | Existe el caso de uso `CU-02 · Consultar historial de identificaciones`, pero no existe un requisito funcional independiente que especifique la consulta del historial. | **Válida.** Registrar información y consultarla constituyen comportamientos distintos y deben expresarse mediante requisitos separados. | Incorporar un requisito funcional específico para consultar el historial y actualizar posteriormente la relación de `CU-02` y la tabla de trazabilidad. | Pendiente |

### Resultado de la revisión

La revisión permitió identificar tres aspectos que requieren modificación y uno
que requiere una decisión previa de alcance.

Las observaciones no se incorporan automáticamente como requisitos en esta
versión. Se registran como trabajo pendiente para la siguiente revisión, donde
deberán actualizarse, según corresponda, los requisitos funcionales y no
funcionales, los casos de uso y la tabla de trazabilidad.

La revisión también permitió comprobar que los principales elementos del
sistema —identificación de especies, tratamiento del nivel de confianza,
historial, funcionamiento offline y manejo de imágenes inadecuadas— se
encuentran representados en la especificación actual.
---
## 8. Registro de cambios

| Fecha | Requisito / sección | Qué cambió | Por qué |
| --- | --- | --- | --- |
| 21/09/2026 | Documento | Creación de la versión inicial de la especificación de requisitos. | Establecer la primera especificación formal de BIOMA. |
| 24/09/2026 | Sección 1 · Alcance | Se establecieron umbrales mínimos de precisión del modelo del 90 % para especies generales y 99 % para especies de importancia médica. | Definir de manera verificable la precisión requerida para los modelos de identificación. |
| 24/09/2026 | Sección 1 · Alcance | Se establecieron niveles mínimos de confianza del 90 % para identificaciones generales y 99 % para especies de importancia médica. | Diferenciar la precisión global del modelo de la confianza requerida para presentar una identificación individual como confirmada. |
| 24/09/2026 | RF-006 | Se agregó el requisito de mostrar especies visualmente similares presentes en la región. | La funcionalidad ya estaba declarada dentro del alcance, pero no contaba con un requisito funcional asociado. |
| 24/09/2026 | RF-007 | Se agregó el registro de datos de identificaciones realizadas por usuarios avanzados. | La recopilación de observaciones de usuarios avanzados estaba contemplada en el alcance sin un requisito funcional asociado. |
| 24/09/2026 | RF-008 | Se agregó la identificación offline de especies de importancia médica. | La funcionalidad estaba declarada en el alcance y fue reforzada durante la entrevista de elicitación. |
| 24/09/2026 | RF-009 | Se agregó la descarga previa de datos regionales para identificación offline. | Se requiere disponer previamente de los datos regionales para hacer posible RF-008. |
| 24/09/2026 | RF-010 | Se agregó el tratamiento de identificaciones con confianza inferior al umbral establecido. | La entrevista reveló que el usuario espera que el sistema comunique explícitamente la incertidumbre de una identificación. |
| 24/09/2026 | RF-011 | Se agregó la presentación de una posible identificación cuando no se alcanza el umbral de confianza. | La entrevista reveló que el usuario considera útil conocer la mejor aproximación disponible aun cuando no pueda presentarse como identificación confirmada. |
| 24/09/2026 | RNF-CON-002 | Se estableció una precisión mínima general del modelo del 90 %. | Convertir el atributo de precisión general en un requisito no funcional medible. |
| 24/09/2026 | RNF-CON-003 | Se estableció una precisión mínima del modelo del 99 % para especies de importancia médica. | La entrevista evidenció la necesidad de mayor certeza en especies de importancia médica y durante la especificación se definió el umbral cuantitativo. |
| 24/09/2026 | RNF-ESC-001 | Se definió que, al superar las 50 identificaciones del historial estándar, se elimina la identificación más antigua. | El requisito original establecía el límite, pero no especificaba el comportamiento al alcanzar la capacidad máxima. |
| 24/09/2026 | RF-012 | Se agregó el tratamiento de imágenes con calidad insuficiente para realizar una identificación. | La regla ya existía en la Visión del producto y la entrevista de elicitación confirmó que condiciones como contraluz, poca iluminación o colores poco visibles dificultan el proceso de identificación. |
| 29/09/2026 | RF-004 | Se especificó que únicamente las identificaciones confirmadas se registran en el historial y que las posibles identificaciones por baja confianza no se almacenan. | Evitar conservar como parte del historial resultados que no alcanzaron el nivel mínimo de confianza requerido. |
| 01/10/2026 | Sección 6 · Trazabilidad | Se relacionaron los requisitos con las pantallas correspondientes del prototipo V1 y se actualizó su estado. | Registrar qué requisitos se encuentran actualmente representados en el prototipo navegable y cuáles permanecen pendientes. |
| 01/10/2026 | Prototipo V1 | Se incorporó el flujo principal de CU-01 y los flujos alternos de imagen inadecuada e identificación con baja confianza. | Permitir validar mediante un prototipo navegable el caso de uso principal y situaciones alternativas relevantes. |

---

## Antes de entregar

- [x] Todos los requisitos tienen identificador único y ninguno está repetido
- [x] Cada requisito expresa una sola idea
- [x] Cada requisito funcional tiene criterio de aceptación comprobable
- [x] Cada requisito no funcional tiene una métrica, no solo un adjetivo
- [x] El campo Origen distingue lo confirmado por el cliente de lo que sigo suponiendo
- [x] Hay al menos un requisito no funcional por cada atributo de calidad que impone mi tipo de sistema
- [x] Ningún requisito impone una solución técnica
- [x] Todos los requisitos caben dentro del alcance declarado
- [x] La tabla de trazabilidad está completa
- [x] Mi dupla revisó el documento y su revisión está registrada
- [x] Borré los ejemplos y las instrucciones en cursiva
