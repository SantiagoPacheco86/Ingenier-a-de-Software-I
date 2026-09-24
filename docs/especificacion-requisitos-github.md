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
| RF-006 | Especies visualmente similares | Importante | Alcance del producto |
| RF-007 | Registro de observaciones de usuario avanzado | Importante | Alcance del producto |
| RF-008 | Identificación offline | Imprescindible | Alcance del producto y entrevista de elicitación |
| RF-009 | Descarga de datos regionales para uso offline | Importante | Derivado de RF-008 |
| RF-010 | Identificación con baja confianza | Imprescindible | Entrevista de elicitación |
| RF-011 | Posible identificación | Importante | Entrevista de elicitación |

### 3.2 Fichas

#### RF-001 · Identificación de especie

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema identifica la especie de flora o fauna presente en una imagen capturada mediante la cámara del dispositivo móvil. |
| **Origen** | Documento de requisitos inicial. |
| **Prioridad** | Imprescindible |
| **Criterio de aceptación** | Al proporcionar una imagen de una especie incluida en el modelo disponible, el sistema procesa la imagen y genera un resultado de identificación. |
| **Relacionado con** | RF-002, RF-003, RF-005, RF-006, RF-010, RF-011, RNF-CON-001, RNF-CON-002, RNF-CON-003, RNF-REN-001 |

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
| **Descripción** | El sistema registra las identificaciones realizadas por el usuario en su historial. |
| **Origen** | Documento de requisitos inicial. La entrevista de elicitación confirmó que conservar información de identificaciones anteriores aporta valor al usuario. |
| **Prioridad** | Importante |
| **Criterio de aceptación** | Después de completar una identificación, esta aparece en el historial correspondiente al usuario con la información asociada que el sistema conserva. |
| **Relacionado con** | RF-001, RNF-SEG-001, RNF-ESC-001 |

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
| **Origen** | Alcance del producto. |
| **Prioridad** | Importante |
| **Criterio de aceptación** | Al consultar el resultado de una especie que cuenta con especies similares registradas para la región, el sistema muestra dichas especies como referencias adicionales. |
| **Relacionado con** | RF-001, RF-002 |

#### RF-007 · Registro de observaciones de usuario avanzado

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema registra los datos asociados a las identificaciones realizadas por usuarios avanzados para su posterior consulta y documentación. |
| **Origen** | Alcance del producto. |
| **Prioridad** | Importante |
| **Criterio de aceptación** | Después de que un usuario avanzado realiza una identificación, los datos asociados quedan registrados y disponibles para su consulta posterior. |
| **Relacionado con** | RF-001, RF-004, RNF-SEG-001 |

#### RF-008 · Identificación offline

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema identifica especies de importancia médica sin conexión a Internet cuando el usuario dispone previamente de los datos correspondientes a su región. |
| **Origen** | Alcance del producto y entrevista de elicitación. El entrevistado identificó como relevante disponer offline de información relacionada con especies de importancia médica. |
| **Prioridad** | Imprescindible |
| **Criterio de aceptación** | Con el dispositivo sin conexión a Internet y con los datos regionales previamente disponibles, el sistema procesa una imagen correspondiente a una especie de importancia médica incluida en dichos datos y genera un resultado de identificación. |
| **Relacionado con** | RF-001, RF-003, RF-009, RF-010, RNF-CON-003 |

#### RF-009 · Descarga de datos regionales para uso offline

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema permite al usuario descargar los datos de una región necesarios para realizar identificaciones offline de especies de importancia médica. |
| **Origen** | Derivado de RF-008 y del alcance del producto. |
| **Prioridad** | Importante |
| **Criterio de aceptación** | Cuando el usuario selecciona una región disponible y solicita su descarga con conexión a Internet, el sistema almacena los datos necesarios y posteriormente los reconoce como disponibles para identificación offline. |
| **Relacionado con** | RF-008 |

#### RF-010 · Identificación con baja confianza

| Campo | Contenido |
| --- | --- |
| **Descripción** | El sistema informa al usuario cuando una identificación no alcanza el nivel mínimo de confianza requerido para presentarse como confirmada. |
| **Origen** | Entrevista de elicitación. El entrevistado indicó que espera transparencia cuando el sistema no tenga suficiente certeza sobre una identificación. |
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

Los casos de uso se desarrollarán a partir de los requisitos funcionales
definidos y de los resultados obtenidos durante la entrevista de
elicitación.

---

## 6. Trazabilidad

| Requisito | Origen | Caso de uso | Elemento del prototipo |
| --- | --- | --- | --- |
|  |  |  |  |

---

## 7. Registro de cambios

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

---

## Antes de entregar

- [ ] Todos los requisitos tienen identificador único y ninguno está repetido
- [ ] Cada requisito expresa una sola idea
- [ ] Cada requisito funcional tiene criterio de aceptación comprobable
- [ ] Cada requisito no funcional tiene una métrica, no solo un adjetivo
- [ ] El campo Origen distingue lo confirmado por el cliente de lo que sigo suponiendo
- [ ] Hay al menos un requisito no funcional por cada atributo de calidad que impone mi tipo de sistema
- [ ] Ningún requisito impone una solución técnica
- [ ] Todos los requisitos caben dentro del alcance declarado
- [ ] La tabla de trazabilidad está completa
- [ ] Mi dupla revisó el documento y su revisión está registrada
- [ ] Borré los ejemplos y las instrucciones en cursiva
