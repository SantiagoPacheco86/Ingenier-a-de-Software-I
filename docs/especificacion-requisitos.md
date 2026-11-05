# Especificación de requisitos

**Sistema:** BIOMA — Sistema de detección de flora y fauna local para senderistas  
**Autor:** Santiago Pacheco Carrillo  
**Versión:** 1.2  
**Fecha de la última actualización:** 04/11/2026
> **Repositorio: https://github.com/SantiagoPacheco86/Ingenier-a-de-Software-I**

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
| RF-001 | Identificar especies mediante una imagen | Imprescindible | Documento de requisitos inicial |
| RF-002 | Consultar información de una especie | Imprescindible | Documento de requisitos inicial y entrevista de elicitación |
| RF-003 | Mostrar el nivel de confianza | Imprescindible | Documento de requisitos inicial y entrevista de elicitación |
| RF-004 | Registrar identificaciones confirmadas | Importante | Documento de requisitos inicial y entrevista de elicitación |
| RF-005 | Notificar una especie no reconocida | Imprescindible | Documento de requisitos inicial |
| RF-006 | Consultar especies visualmente similares | Importante | Visión del producto |
| RF-007 | Registrar observaciones avanzadas | Importante | Visión del producto |
| RF-008 | Identificar especies de importancia médica sin conexión | Imprescindible | Visión del producto y entrevista de elicitación |
| RF-009 | Descargar datos regionales para uso offline | Importante | Derivado de RF-008 |
| RF-010 | Notificar una identificación de baja confianza | Imprescindible | Entrevista de elicitación y especificación |
| RF-011 | Mostrar una posible identificación | Importante | Entrevista de elicitación |
| RF-012 | Solicitar una nueva captura por calidad insuficiente | Importante | Visión del producto y entrevista de elicitación |
| RF-013 | Capturar una imagen para identificación | Imprescindible | Derivado de CU-01 y observación docente |
| RF-014 | Consultar el historial de identificaciones | Importante | Derivado de CU-02 y revisión de la dupla |
| RF-015 | Autenticar usuarios y administrar sesiones | Importante | Propuesta para resolver referencias a cuentas; pendiente de validar alcance |

### 3.2 Fichas

#### RF-001 · Identificar especies mediante una imagen

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema identifica la especie de flora o fauna presente en una imagen capturada mediante la cámara del dispositivo móvil. |
| **Origen** | Documento de requisitos inicial. |
| **Prioridad** | Imprescindible |
| **Criterio de aceptación** | Al proporcionar una imagen de una especie incluida en el modelo disponible, el sistema procesa la imagen y genera un resultado de identificación. |
| **Relacionado con** | RF-002, RF-003, RF-005, RF-006, RF-010, RF-011, RF-012, RNF-CON-001, RNF-CON-002, RNF-CON-003, RNF-REN-001 |

#### RF-002 · Consultar información de una especie

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema muestra el nombre común, nombre científico, región y nivel de riesgo o importancia médica de la especie identificada. |
| **Origen** | Documento de requisitos inicial. La entrevista de elicitación confirmó el interés por consultar información descriptiva y de importancia médica. |
| **Prioridad** | Imprescindible |
| **Criterio de aceptación** | Al obtener una identificación confirmada, el sistema presenta el nombre común, nombre científico, región y nivel de riesgo o importancia médica registrados para la especie. |
| **Relacionado con** | RF-001, RF-003, RF-006 |

#### RF-003 · Mostrar el nivel de confianza

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema muestra el nivel de confianza asociado a cada resultado de identificación. |
| **Origen** | Documento de requisitos inicial y entrevista de elicitación. El entrevistado indicó que conocer la certeza del resultado influye en la confianza para actuar sobre la identificación. |
| **Prioridad** | Imprescindible |
| **Criterio de aceptación** | Después de procesar una imagen, el resultado presenta el porcentaje de confianza asociado a la identificación obtenida. |
| **Relacionado con** | RF-001, RF-005, RF-010, RF-011 |

#### RF-004 · Registrar identificaciones confirmadas

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema registra en el historial únicamente las identificaciones que alcanzan el nivel de confianza requerido para presentarse como confirmadas. |
| **Origen** | Documento de requisitos inicial. La entrevista de elicitación confirmó que conservar información de identificaciones anteriores aporta valor al usuario. La exclusión de identificaciones no confirmadas fue definida durante la especificación. |
| **Prioridad** | Importante |
| **Criterio de aceptación** | Cuando una identificación alcanza el nivel de confianza requerido para presentarse como confirmada, el sistema la registra en el historial. Si el resultado se presenta únicamente como posible identificación por no alcanzar el nivel de confianza requerido, el sistema no lo registra en el historial. |
| **Relacionado con** | RF-001, RF-003, RF-010, RF-011, RNF-SEG-001, RNF-ESC-001 |

#### RF-005 · Notificar una especie no reconocida

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema notifica al usuario que la especie no pudo reconocerse cuando el modelo regional no ofrece una identificación válida. |
| **Origen** | Documento de requisitos inicial. |
| **Prioridad** | Imprescindible |
| **Criterio de aceptación** | Al analizar una especie que no pueda ser identificada mediante el modelo disponible, el sistema informa que no fue posible realizar la identificación y no presenta una especie como resultado confirmado. |
| **Relacionado con** | RF-001, RF-003, RF-010, RF-011 |

#### RF-006 · Consultar especies visualmente similares

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema muestra especies visualmente similares presentes en la región de la especie identificada. |
| **Origen** | Visión del producto. |
| **Prioridad** | Importante |
| **Criterio de aceptación** | Al consultar el resultado de una especie que cuenta con especies similares registradas para la región, el sistema muestra dichas especies como referencias adicionales. |
| **Relacionado con** | RF-001, RF-002 |

#### RF-007 · Registrar observaciones avanzadas

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema permite al usuario avanzado guardar una observación asociada a una identificación, con especie candidata o confirmada, fecha, región y notas opcionales, para documentación y consulta privada. La conservación de fotografías y ubicación exacta requiere consentimiento y definición posterior de alcance. |
| **Origen** | Visión del producto. |
| **Prioridad** | Importante |
| **Criterio de aceptación** | Después de que un usuario avanzado realiza una identificación, los datos asociados quedan registrados y disponibles para su consulta posterior. |
| **Relacionado con** | RF-001, RF-004, RNF-SEG-001 |

#### RF-008 · Identificar especies de importancia médica sin conexión

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema identifica especies de importancia médica sin conexión a Internet cuando el usuario dispone previamente de los datos correspondientes a su región. |
| **Origen** | Visión del producto y entrevista de elicitación. El entrevistado identificó como relevante disponer offline de información relacionada con especies de importancia médica. |
| **Prioridad** | Imprescindible |
| **Criterio de aceptación** | Con el dispositivo sin conexión a Internet y con los datos regionales previamente disponibles, el sistema procesa una imagen correspondiente a una especie de importancia médica incluida en dichos datos y genera un resultado de identificación. |
| **Relacionado con** | RF-001, RF-003, RF-009, RF-010, RF-012, RNF-CON-003 |

#### RF-009 · Descargar datos regionales para uso offline

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema permite al usuario descargar los datos de una región necesarios para realizar identificaciones offline de especies de importancia médica. |
| **Origen** | Derivado de RF-008 y de la Visión del producto. |
| **Prioridad** | Importante |
| **Criterio de aceptación** | Cuando el usuario selecciona una región disponible y solicita su descarga con conexión a Internet, el sistema almacena los datos necesarios y posteriormente los reconoce como disponibles para identificación offline. |
| **Relacionado con** | RF-008 |

#### RF-010 · Notificar una identificación de baja confianza

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema informa al usuario cuando una identificación no alcanza el nivel mínimo de confianza requerido para presentarse como confirmada. |
| **Origen** | Entrevista de elicitación y especificación. La entrevista confirmó la necesidad de comunicar la incertidumbre; los umbrales fueron definidos posteriormente durante la especificación. |
| **Prioridad** | Imprescindible |
| **Criterio de aceptación** | Si una identificación general obtiene una confianza inferior al 90 %, o una identificación de importancia médica obtiene una confianza inferior al 99 %, el sistema informa que el resultado no alcanza la confianza requerida y no lo presenta como identificación confirmada. |
| **Relacionado con** | RF-001, RF-003, RF-005, RF-011, RNF-CON-002, RNF-CON-003 |

#### RF-011 · Mostrar una posible identificación

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema muestra la especie con mayor nivel de confianza como posible identificación cuando el resultado no alcanza el umbral requerido para presentarse como confirmado. |
| **Origen** | Entrevista de elicitación. El entrevistado indicó que, ante una identificación incierta, espera conocer la mejor aproximación disponible sin ocultar la incertidumbre. |
| **Prioridad** | Importante |
| **Criterio de aceptación** | Cuando existe al menos una especie candidata pero ninguna alcanza el umbral correspondiente, el sistema muestra la candidata con mayor confianza identificándola explícitamente como posible identificación y muestra su nivel de confianza. |
| **Relacionado con** | RF-003, RF-005, RF-010 |

#### RF-012 · Solicitar una nueva captura por calidad insuficiente

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema solicita una nueva captura cuando detecta que la imagen es inadecuada para la identificación y presenta una recomendación de mejora. |
| **Origen** | Visión del producto. La entrevista de elicitación reforzó este requisito al identificar fotografías con contraluz, poca iluminación o colores poco visibles como una dificultad del proceso actual. |
| **Prioridad** | Importante |
| **Criterio de aceptación** | Cuando una imagen no cumple las condiciones mínimas necesarias para realizar la identificación, el sistema no presenta una especie como resultado, solicita una nueva captura y muestra recomendaciones para mejorar la imagen. |
| **Relacionado con** | RF-001, RF-008, RF-010, RNF-CON-002, RNF-CON-003 |

---

### 3.3 Requisitos incorporados en la revisión 1.2

#### RF-013 · Capturar una imagen para identificación

| Campo | Contenido |
| --- | --- |
| Descripción | El sistema permite capturar una imagen del organismo mediante la cámara del dispositivo móvil para utilizarla en el proceso de identificación. |
| Origen | Derivado del flujo del prototipo y de la observación docente sobre la separación de casos de uso. |
| Prioridad | Imprescindible |
| Criterio de aceptación | Con permiso de cámara concedido, al pulsar capturar, el sistema obtiene una imagen y permite continuar a la verificación de calidad; si se cancela, no inicia identificación. |
| Relacionado con | RF-001, RF-012, CU-06 |

#### RF-014 · Consultar el historial de identificaciones

| Campo | Contenido |
| --- | --- |
| Descripción | El sistema permite al usuario consultar la lista de sus identificaciones confirmadas previamente registradas. |
| Origen | Observación RD-004 de la dupla y CU-02 ya existente. |
| Prioridad | Importante |
| Criterio de aceptación | Al abrir historial, el usuario ve únicamente sus identificaciones confirmadas; si no existen, se muestra un estado vacío; no puede consultar registros privados de otro usuario. |
| Relacionado con | RF-004, RNF-SEG-001, CU-02 |

#### RF-015 · Autenticar usuarios y administrar sesiones (propuesta pendiente)

| Campo | Contenido |
| --- | --- |
| Descripción propuesta | El sistema autentica a usuarios que requieren acceder a información privada y permite cerrar la sesión. |
| Origen | RD-002 de la revisión de la dupla; requiere decisión de alcance. |
| Prioridad | Por definir |
| Criterio de aceptación propuesto | Con credenciales válidas se inicia sesión; con credenciales inválidas se rechaza; al cerrar sesión se impide acceder a datos privados sin autenticación. |
| Relacionado con | RNF-SEG-001, RF-007, RF-014 |

**Decisión pendiente:** definir si BIOMA requiere cuentas en su primera versión o si utilizará identidad local para el historial. RF-015 no se considera aprobado hasta resolver esta decisión.

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

La revisión docente identificó que CU-01 reunía captura, validación de imagen, identificación y consulta del resultado. La versión 1.2 separa estas responsabilidades en casos de uso con un objetivo principal definido. Se conserva CU-01 como identificación para mantener la trazabilidad histórica. Los casos nuevos deben incorporarse también al diagrama editable de `docs/diagramas/casos-de-uso.drawio` y exportarse nuevamente a PNG; esta actualización documental no significa que el archivo gráfico ya se haya modificado.

### 5.1 Catálogo revisado

| ID | Caso de uso | Actor principal | Requisitos |
| --- | --- | --- | --- |
| CU-01 | Identificar una especie a partir de una imagen válida | Estándar / avanzado | RF-001, RF-003, RF-005, RF-010, RF-011 |
| CU-02 | Consultar historial de identificaciones | Estándar / avanzado | RF-014 |
| CU-03 | Registrar observación avanzada | Avanzado | RF-007 |
| CU-04 | Identificar una especie de importancia médica sin conexión | Estándar / avanzado | RF-008, RF-003, RF-010 |
| CU-05 | Descargar datos regionales para uso offline | Estándar / avanzado | RF-009 |
| CU-06 | Capturar imagen de una especie | Estándar / avanzado | RF-013 |
| CU-07 | Verificar calidad de imagen capturada | Estándar / avanzado | RF-012 |
| CU-08 | Consultar información de una especie | Estándar / avanzado | RF-002, RF-006 |
| CU-09 | Registrar identificación confirmada | Estándar / avanzado | RF-004 |
| CU-10 | Consultar nivel de confianza de una identificación | Estándar / avanzado | RF-003 |

**Nota de modelado:** los CU-07 y CU-09 representan comportamientos automáticos iniciados dentro de un objetivo del usuario. En el diagrama UML se pueden representar como inclusiones (`<<include>>`) cuando proceda, sin presentarlos como acciones manuales independientes. CU-10 puede integrarse en CU-08 si se prefiere evitar un caso de uso sin objetivo autónomo.

### 5.2 Fichas de casos de uso

#### CU-06 · Capturar imagen de una especie

| Campo | Contenido |
| --- | --- |
| Actor | Usuario estándar o avanzado |
| Objetivo | Proporcionar una fotografía para su análisis. |
| Precondición | La aplicación está abierta y tiene permiso para usar la cámara. |
| Flujo principal | 1. El usuario abre la cámara. 2. Enfoca el organismo. 3. Captura la fotografía. 4. El sistema entrega la imagen a la verificación de calidad. |
| Alternos | A1. Si se deniega el permiso, se solicita habilitarlo. A2. Si el usuario cancela, no se procesa ni registra ninguna imagen. |
| Postcondición | Imagen capturada disponible temporalmente para verificación. |
| Requisitos | RF-013 |

#### CU-07 · Verificar calidad de imagen capturada

| Campo | Contenido |
| --- | --- |
| Actor | Usuario estándar o avanzado (inicia la captura); sistema (ejecuta la verificación) |
| Objetivo | Determinar si la imagen puede utilizarse para identificación. |
| Precondición | Existe una imagen capturada. |
| Flujo principal | 1. El sistema evalúa condiciones mínimas de calidad. 2. La imagen resulta adecuada. 3. El sistema habilita la identificación. |
| Alternos | A1. Si la imagen es inadecuada, el sistema indica el problema y recomienda mejorar iluminación o enfoque; permite repetir la captura sin enviar la imagen al reconocimiento. |
| Postcondición | Imagen aceptada o nueva captura solicitada. |
| Requisitos | RF-012 |

#### CU-01 · Identificar una especie a partir de una imagen válida

| Campo | Contenido |
| --- | --- |
| Actor | Usuario estándar o avanzado |
| Objetivo | Obtener una identificación de la especie presente en una imagen válida. |
| Precondición | Existe una imagen validada y un modelo regional disponible. |
| Flujo principal | 1. El usuario solicita identificar la imagen. 2. El sistema procesa la imagen con el modelo disponible. 3. Obtiene una especie candidata y un valor de confianza. 4. Compara la confianza con el umbral correspondiente (90 % general; 99 % importancia médica). 5. Si cumple, presenta identificación confirmada y habilita la consulta de su información. |
| Alternos | A1. Especie fuera del modelo: notifica que no fue reconocida, sin confirmar ni registrar. A2. Confianza insuficiente: muestra advertencia y, si existe candidata, la presenta únicamente como posible identificación con porcentaje; no la registra como confirmada. A3. Modelo regional no disponible: informa que no puede procesarse la solicitud. |
| Postcondición | Resultado confirmado, posible o no reconocido; solo los confirmados son elegibles para historial. |
| Requisitos | RF-001, RF-003, RF-005, RF-010, RF-011, RNF-CON-002, RNF-CON-003, RNF-REN-001 |

#### CU-08 · Consultar información de una especie

| Campo | Contenido |
| --- | --- |
| Actor | Usuario estándar o avanzado |
| Objetivo | Conocer la información de la especie identificada. |
| Precondición | Existe un resultado o especie seleccionada con información disponible. |
| Flujo principal | 1. El usuario abre el detalle. 2. El sistema muestra nombre común, científico, región e importancia médica. 3. Muestra especies similares cuando están disponibles. |
| Alternos | A1. Sin especies similares: omite esa sección. A2. Resultado posible: conserva una advertencia visible de incertidumbre. |
| Postcondición | Información consultada sin alterar la identificación. |
| Requisitos | RF-002, RF-006, RF-003 |

#### CU-10 · Consultar nivel de confianza de una identificación

| Campo | Contenido |
| --- | --- |
| Actor principal | Usuario estándar / Usuario avanzado |
| Objetivo | Consultar el porcentaje de confianza de una identificación para conocer si el resultado cumple con el umbral requerido para considerarse confirmado. |
| Precondición | El sistema ha procesado una imagen y dispone de una especie candidata con un valor de confianza calculado. |
| Escenario principal | 1. El usuario consulta el resultado de la identificación. 2. El sistema muestra la especie candidata y su porcentaje de confianza. 3. El sistema determina el umbral correspondiente según la clasificación de la especie. 4. Si es una especie general, aplica el umbral del 90 %. 5. Si es una especie de importancia médica, aplica el umbral del 99 %. 6. El sistema informa si la identificación está confirmada. |
| Flujo alterno A1 | Si la confianza es inferior al umbral correspondiente, el sistema presenta el resultado como identificación no confirmada y muestra una advertencia. |
| Flujo alterno A2 | Si el modelo no genera una especie candidata o un valor de confianza válido, el sistema informa que no fue posible obtener una identificación confiable. |
| Postcondición | El usuario conoce el nivel de confianza y el estado de confirmación. La consulta no modifica el resultado ni genera registros adicionales en el historial. |
| Requisitos que realiza | RF-003 |

#### CU-09 · Registrar identificación confirmada

| Campo | Contenido |
| --- | --- |
| Actor | Usuario estándar o avanzado (beneficiario); sistema (registra) |
| Objetivo | Conservar una identificación confirmada en el historial. |
| Precondición | La identificación alcanzó su umbral de confianza. |
| Flujo principal | 1. El sistema registra especie, fecha, región y confianza. 2. El registro queda asociado al usuario. |
| Alternos | A1. Si es usuario estándar y existen 50 registros, elimina el más antiguo antes de incorporar el nuevo. A2. Si el resultado no es confirmado, no lo registra. A3. Si falla el almacenamiento, informa el error sin afirmar que se guardó. |
| Postcondición | Historial actualizado o error comunicado. |
| Requisitos | RF-004, RNF-ESC-001, RNF-SEG-001 |

#### CU-02 · Consultar historial de identificaciones

| Campo | Contenido |
| --- | --- |
| Actor | Usuario estándar o avanzado |
| Objetivo | Recuperar las identificaciones confirmadas propias. |
| Precondición | Usuario identificado por el mecanismo de acceso definido para la versión. |
| Flujo principal | 1. Abre historial. 2. El sistema obtiene únicamente sus registros. 3. Muestra la lista y permite abrir un registro. |
| Alternos | A1. Sin registros: muestra estado vacío. A2. Sin conexión y sin datos locales: informa indisponibilidad. A3. Acceso a registros ajenos: rechaza la solicitud. |
| Postcondición | Consulta realizada sin modificar los registros. |
| Requisitos | RF-014, RNF-SEG-001 |

#### CU-03 · Registrar observación avanzada

| Campo | Contenido |
| --- | --- |
| Actor | Usuario avanzado |
| Objetivo | Documentar una observación de campo. |
| Precondición | Usuario con perfil avanzado y especie o resultado disponible. |
| Flujo principal | 1. Abre registro de observación. 2. Agrega notas opcionales. 3. Confirma guardar. 4. El sistema almacena los datos autorizados de forma privada. |
| Alternos | A1. Cancelación: no almacena. A2. Datos obligatorios faltantes: solicita completarlos. A3. Usuario sin permisos: rechaza la operación. |
| Postcondición | Observación privada almacenada o rechazo explicado. |
| Requisitos | RF-007, RNF-SEG-001 |

#### CU-04 · Identificar una especie de importancia médica sin conexión

| Campo | Contenido |
| --- | --- |
| Actor | Usuario estándar o avanzado |
| Objetivo | Identificar una especie de importancia médica sin Internet. |
| Precondición | Paquete regional y recursos de inferencia offline compatibles ya descargados. |
| Flujo principal | 1. El usuario solicita identificación offline con una imagen válida. 2. El sistema utiliza recursos locales. 3. Aplica el umbral de confianza del 99 %. 4. Muestra el resultado con su nivel de certeza. |
| Alternos | A1. Paquete no disponible: informa que debe descargarse con Internet. A2. Confianza inferior al 99 %: presenta solo posible identificación y advertencia. A3. Especie no incluida: informa que no fue reconocida. |
| Postcondición | Resultado disponible sin depender de inferencia en la nube. |
| Requisitos | RF-008, RF-003, RF-010, RF-011 |

#### CU-05 · Descargar datos regionales para uso offline

| Campo | Contenido |
| --- | --- |
| Actor | Usuario estándar o avanzado |
| Objetivo | Preparar recursos regionales para identificación sin Internet. |
| Precondición | Existe conexión a Internet y un paquete regional publicado. |
| Flujo principal | 1. Selecciona región. 2. Solicita descarga. 3. El sistema descarga y verifica el paquete. 4. Confirma disponibilidad offline. |
| Alternos | A1. Descarga interrumpida: informa fallo y permite reintentar. A2. Almacenamiento insuficiente: informa espacio requerido. |
| Postcondición | Paquete regional verificado y disponible o error comunicado. |
| Requisitos | RF-009 |

### 5.3 Relaciones recomendadas para actualizar el diagrama UML

- CU-01 `<<include>>` CU-07 únicamente si el flujo de identificación siempre realiza esa verificación; si CU-07 ya se ejecutó al capturar, evitar duplicarla.
- CU-01 puede desencadenar CU-09 al confirmar una identificación, como comportamiento automático condicionado, no como `<<include>>` incondicional.
- CU-08 puede iniciarse desde el resultado de CU-01; no es obligatorio incluirlo para que la identificación concluya.
- CU-04 reutiliza la lógica de identificación de CU-01 con recursos locales y umbral médico, sin exigir un segundo flujo de captura independiente.

---

## 6. Trazabilidad

La columna **Estado de documentación** indica que el requisito está especificado, no que se haya implementado o demostrado. Las referencias de pantallas corresponden al prototipo V1 previamente documentado; las nuevas pantallas o cambios del diagrama siguen pendientes de verificación.

| Requisito | Caso de uso | Pantalla V1 | Estado de documentación |
| --- | --- | --- | --- |
| RF-001 | CU-01, CU-04 | P04, P05 | Actualizado |
| RF-002 | CU-08 | P05 | Actualizado |
| RF-003 | CU-01, CU-04, CU-08, CU-10 | P05, A-02 | Actualizado |
| RF-004 | CU-09 | P05, P06 | Actualizado |
| RF-005 | CU-01, CU-04 | — | Actualizado; representación pendiente |
| RF-006 | CU-08 | P05 | Actualizado |
| RF-007 | CU-03 | — | Revisado; alcance de datos pendiente |
| RF-008 | CU-04 | — | Actualizado; representación pendiente |
| RF-009 | CU-05 | — | Actualizado; representación pendiente |
| RF-010 | CU-01, CU-04 | A-02 | Actualizado |
| RF-011 | CU-01, CU-04 | A-02 | Actualizado |
| RF-012 | CU-07 | A-01 | Actualizado |
| RF-013 | CU-06 | P02, P03 | Nuevo; representado en V1 |
| RF-014 | CU-02 | P06 | Nuevo; representado en V1 |
| RF-015 | Pendiente de caso de uso y decisión de alcance | — | Propuesto, no aprobado |
| RNF-CON-001 | CU-01, CU-04 | — | Pendiente de prueba |
| RNF-CON-002 | CU-01 | — | Pendiente de prueba |
| RNF-CON-003 | CU-01, CU-04 | — | Pendiente de prueba |
| RNF-REN-001 | CU-01, CU-04 | P04 | Pendiente de medición |
| RNF-SEG-001 | CU-02, CU-03, CU-09 | — | Pendiente de prueba |
| RNF-ESC-001 | CU-02, CU-09 | P06 | Pendiente de prueba |

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
| RD-001 | No existe un requisito no funcional de usabilidad, aunque la facilidad de uso forma parte de las expectativas del usuario estándar. | **Válida.** La facilidad de uso aparece como una característica relevante del sistema, pero actualmente no existe un RNF con una métrica que permita verificarla. | Definir `RNF-USA-001` con una condición o métrica comprobable de usabilidad durante la siguiente revisión. | Pendiente; no es observación de la maestra |
| RD-002 | Se mencionan cuentas y propiedad de información o fotografías, pero no existen requisitos funcionales que definan el comportamiento de las cuentas. | **Parcialmente válida.** Existe una inconsistencia si la documentación presupone la existencia de cuentas sin especificar su comportamiento. Sin embargo, antes de crear nuevos requisitos debe determinarse si la gestión de cuentas pertenece realmente al alcance del sistema. | Revisar las referencias a cuentas. Si forman parte del alcance, definir los requisitos correspondientes; de lo contrario, eliminar o reformular dichas referencias. | Pendiente de decisión |
| RD-003 | No queda suficientemente claro por qué se almacenan las fotografías y datos de los usuarios avanzados ni cuál es la finalidad de conservar esta información. | **Válida.** El registro de observaciones avanzadas necesita una finalidad y comportamiento más claramente delimitados para evitar interpretaciones distintas. | Revisar `RF-007` y el alcance relacionado con usuarios avanzados para especificar qué información se conserva, con qué finalidad y dentro de qué límites. | Pendiente |
| RD-004 | Existe el caso de uso `CU-02 · Consultar historial de identificaciones`, pero no existe un requisito funcional independiente que especifique la consulta del historial. | **Válida.** Registrar información y consultarla constituyen comportamientos distintos y deben expresarse mediante requisitos separados. | Se incorporó RF-014 y se actualizó CU-02 y la trazabilidad. | Atendida documentalmente |

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
| 04/11/2026 | Versión 1.2 / RF-001–RF-012 | Se normalizaron los nombres de los requisitos funcionales con verbos de acción y se revisaron las descripciones de RF-005, RF-007 y RF-012. | Atender la observación docente sobre redacción orientada a acciones y claridad de la necesidad funcional. |
| 04/11/2026 | RF-013 | Se agregó el requisito de capturar una imagen mediante la cámara. | Separar captura de imagen e identificación conforme a la observación docente. |
| 04/11/2026 | RF-014 / RD-004 | Se agregó el requisito de consultar historial. | Resolver la discrepancia entre CU-02 y los requisitos identificada por la dupla. |
| 04/11/2026 | RF-015 / RD-002 | Se documentó como propuesta pendiente la autenticación y gestión de sesiones. | No asumir cuentas obligatorias sin validar el alcance. |
| 04/11/2026 | Sección 5 / CU-01–CU-10 | Se redefinieron las responsabilidades y se documentaron casos de uso separados para captura, validación, identificación, consulta y registro; se ampliaron fichas y alternos. | Atender la observación docente sobre casos de uso con múltiples objetivos y falta de desarrollo de los demás casos. |
| 04/11/2026 | Sección 6 / Trazabilidad | Se actualizaron asociaciones de requisitos a casos de uso y se distinguió documentación de implementación. | Mantener consistencia después del desglose y evitar presentar prototipos como pruebas funcionales. |
| 04/11/2026 | Diagrama UML de casos de uso | Se documentaron las modificaciones necesarias, pendientes de aplicar al archivo draw.io y a su exportación PNG. | Alinear el diagrama gráfico con el catálogo revisado, sin declarar falsamente un archivo gráfico actualizado. |
| 04/11/2026 | Sección 7 / Revisión de la dupla | Se marcó RD-004 como atendida documentalmente; RD-001, RD-002 y RD-003 requieren decisiones o requisitos complementarios. | Conservar seguimiento verificable de observaciones anteriores. |

---

## Antes de entregar

- [x] Todos los requisitos tienen identificador único y ninguno está repetido
- [x] Cada requisito expresa una sola idea
- [x] Cada requisito funcional tiene criterio de aceptación comprobable
- [x] Los RNF vigentes tienen métrica; RNF-USA-001 sigue pendiente de definición
- [x] El campo Origen distingue lo confirmado por el cliente de lo que sigo suponiendo
- [x] Hay al menos un requisito no funcional por cada atributo de calidad que impone mi tipo de sistema
- [ ] Revisar la consistencia entre procesamiento en nube e identificación offline en la próxima decisión arquitectónica
- [ ] Validar el alcance de cuentas, almacenamiento de observaciones y RF-015
- [x] La tabla de trazabilidad documental está actualizada; quedan pendientes las evidencias de implementación
- [x] Mi dupla revisó el documento y su revisión está registrada
- [x] Borré los ejemplos y las instrucciones en cursiva
