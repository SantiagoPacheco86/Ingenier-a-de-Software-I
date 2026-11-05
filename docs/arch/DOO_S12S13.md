# De los requisitos a las clases

**Asignatura:** Diseño Orientado a Objetos · SIS3407  
**Sistema:** BIOMA — Sistema de detección de flora y fauna local para senderistas  
**Autor:** Santiago Pacheco Carrillo  
**Documento:** DOO_S12S13  
**Especificación de referencia:** BIOMA_especificacion_requisitos_v1.2.md (04/11/2026)

> **Criterio de trabajo:** Se aplica la técnica de sustantivos presentada en clase. El punto 1 reproduce las secciones 1 a 6 de la especificación original, sin modificar sus requisitos, y marca sustantivos con `<u>subrayado</u>`. Los puntos 2 a 4 son decisiones de análisis y diseño propuestas, no clases ya implementadas.

---

## 1. Especificación de requisitos con sustantivos subrayados

Se conserva el texto de propósito, usuarios, requisitos funcionales, requisitos no funcionales, casos de uso y trazabilidad. El subrayado es deliberadamente amplio: todavía **no se descartan** sustantivos.

### 1. <u>Propósito</u> y <u>alcance</u>

**<u>Propósito</u> del <u>documento</u>:**

El <u>propósito</u> de este <u>documento</u> es especificar los <u>requisitos</u> del <u>sistema</u>
BIOMA, estableciendo de manera clara y verificable las <u>funcionalidades</u>,
<u>restricciones</u> y <u>atributos</u> de <u>calidad</u> que deberá cumplir el <u>sistema</u>
durante su <u>desarrollo</u>.

El <u>documento</u> está dirigido al <u>equipo</u> de <u>desarrollo</u> y a las <u>personas</u>
involucradas en la <u>definición</u>, <u>revisión</u> y <u>validación</u> del <u>sistema</u>.
Servirá como referencia para el <u>diseño</u>, <u>implementación</u>, <u>pruebas</u> y
posterior análisis de <u>cambios</u> de los <u>requisitos</u> del <u>producto</u>.

**<u>Alcance</u> del <u>sistema</u>:**

BIOMA es un <u>sistema</u> para la <u>identificación</u> de <u>especies</u> de <u>flora</u> y <u>fauna</u>
local mediante la <u>cámara</u> de un <u>teléfono inteligente</u>. El <u>sistema</u> analiza
las <u>imágenes</u> proporcionadas mediante <u>modelos de identificación</u> entrenados
con <u>datos regionales</u> y presenta al <u>usuario</u> <u>información</u> relacionada con
la <u>especie</u> identificada.

Para las <u>especies</u> generales incluidas en el <u>modelo</u>, BIOMA establece una
<u>precisión</u> mínima del <u>modelo</u> del 90 %. Una <u>identificación</u> individual
requiere un <u>nivel de confianza</u> mínimo del 90 % para presentarse como
<u>identificación confirmada</u>.

Para <u>especies</u> clasificadas como de <u>importancia médica</u>, BIOMA establece
una <u>precisión</u> mínima del <u>modelo</u> del 99 %. Una <u>identificación</u> individual
de una <u>especie</u> de <u>importancia médica</u> requiere un <u>nivel de confianza</u>
mínimo del 99 % para presentarse como <u>identificación confirmada</u>.

Cuando una <u>identificación</u> no <u>alcance</u> el <u>nivel de confianza</u> requerido,
el <u>sistema</u> deberá comunicar la <u>incertidumbre</u> al <u>usuario</u> y podrá presentar
la <u>especie</u> con mayor <u>nivel de confianza</u> únicamente como una posible
<u>identificación</u>, sin presentarla como <u>resultado</u> confirmado.

El <u>sistema</u> contempla:

- <u>Identificación</u> de <u>especies</u> mediante la <u>cámara</u> de un <u>teléfono inteligente</u>.
- <u>Presentación</u> de <u>información</u> de la <u>especie</u> identificada, incluyendo
  <u>nombre común</u>, <u>nombre científico</u>, <u>región</u>, <u>nivel</u> de <u>riesgo</u> o importancia
  médica y <u>nivel de confianza</u>.
- <u>Presentación</u> de <u>especies visualmente similares</u> presentes en la <u>región</u>.
- <u>Historial</u> de las <u>especies</u> identificadas por el <u>usuario</u>, incluyendo los
  <u>datos</u> asociados con cada <u>identificación</u>.
- <u>Recopilación</u> y <u>almacenamiento</u> de <u>datos</u> de las <u>identificaciones</u>
  realizadas por <u>usuarios avanzados</u> con el <u>propósito</u> de apoyar la
  <u>documentación</u> de <u>flora</u> y <u>fauna</u> regional.
- <u>Reconocimiento</u> offline de <u>especies</u> de <u>importancia médica</u>, siempre que
  el <u>usuario</u> haya descargado previamente los <u>datos</u> correspondientes a su
  <u>región</u>.
- <u>Descarga</u> previa de los <u>datos regionales</u> necesarios para realizar
  <u>identificaciones</u> offline de <u>especies</u> de <u>importancia médica</u>.
- <u>Comunicación</u> explícita de <u>identificaciones</u> que no alcancen el <u>nivel</u>
  de <u>confianza</u> requerido.
- <u>Presentación</u> de la <u>especie</u> con mayor <u>nivel de confianza</u> como posible
  <u>identificación</u> cuando no se <u>alcance</u> el <u>umbral</u> requerido.

**Fuera del <u>alcance</u>:**

- El <u>sistema</u> no almacena la <u>imagen</u> utilizada para realizar la <u>detección</u>
  cuando se trata de un <u>usuario estándar</u>.
- El <u>sistema</u> no constituye una <u>plataforma</u> científica de <u>validación</u>
  colaborativa.
- El <u>sistema</u> no garantiza una <u>identificación</u> definitiva cuando no se
  <u>alcance</u> el <u>nivel de confianza</u> establecido.
- El <u>sistema</u> no presenta como <u>identificación confirmada</u> una <u>especie</u> que
  no <u>alcance</u> el <u>nivel de confianza</u> correspondiente.
- El <u>sistema</u> no identifica como confirmadas <u>especies</u> que se encuentren
  fuera de los <u>datos</u> o <u>modelos</u> disponibles para la <u>región</u> seleccionada.

---

### 2. <u>Usuarios</u> y su contexto

BIOMA contempla dos tipos principales de <u>usuario</u>: el **<u>usuario estándar</u>**
y el **<u>usuario avanzado</u>**.

| <u>Usuario</u> | Qué hace hoy sin el <u>sistema</u> | Qué espera del <u>sistema</u> |
| --- | --- | --- |
| **<u>Usuario estándar</u> — excursionista, turista o <u>persona</u> interesada en la naturaleza** | Observa el organismo, registra o recuerda sus características, las compara con referencias disponibles, descarta posibles <u>especies</u> hasta obtener una <u>identificación</u> probable y, cuando es necesario, busca <u>validación</u> de una <u>persona</u> con mayor <u>conocimiento</u>. | Facilidad de uso y <u>acceso</u> rápido al <u>reconocimiento</u> mediante la <u>cámara</u>, con una <u>experiencia</u> similar a Shazam: apuntar y obtener una <u>identificación</u> sin requerir conocimientos especializados. Espera una <u>respuesta</u> rápida acompañada de <u>fotografías</u>, características visuales y <u>datos</u> que le permitan corroborar que la <u>especie</u> identificada corresponde con lo observado. |
| **<u>Usuario avanzado</u> — estudiantes, científicos, investigadores o entusiastas con conocimientos de <u>flora</u> y <u>fauna</u>** | Realiza <u>observaciones</u> y compara las características del organismo con referencias y <u>conocimiento</u> especializado para determinar una <u>identificación</u>. Posteriormente puede registrar y organizar manualmente sus <u>observaciones</u> para utilizarlas en <u>documentación</u>, investigación o trabajo de campo. | <u>Acceso</u> a <u>información</u> detallada y técnica de la <u>especie</u> identificada, como <u>nombre científico</u>, taxonomía, <u>nivel de confianza</u>, características distintivas y <u>especies</u> similares. Espera poder acceder preliminarmente a bases de <u>datos</u> y <u>modelos</u> en fase beta con mayor cobertura regional, además de registrar, organizar y documentar <u>observaciones</u> que puedan utilizarse como apoyo para estudios biológicos, monitoreo de <u>especies</u> o trabajo de campo. |

**Conflictos identificados entre <u>usuarios</u>:**

Existe un conflicto entre las prioridades del <u>usuario estándar</u> y las del
<u>usuario avanzado</u>.

El **<u>usuario estándar</u>** prioriza la rapidez y simplicidad del <u>sistema</u> y
espera identificar una <u>especie</u> casi inmediatamente después de apuntar la
<u>cámara</u> o proporcionar una <u>imagen</u>. La <u>interacción</u> debe requerir pocos
conocimientos especializados y permitir interpretar fácilmente el
<u>resultado</u>.

El **<u>usuario avanzado</u>**, en <u>cambio</u>, prioriza la <u>calidad</u>, <u>precisión</u> y
profundidad de la <u>identificación</u>. Puede aceptar un mayor <u>tiempo</u> de
<u>procesamiento</u> a <u>cambio</u> de analizar una mayor cantidad de <u>especies</u>,
obtener un <u>nivel de confianza</u> más fiable y disponer de <u>información</u>
técnica adicional que le permita contrastar y validar los <u>resultados</u>.

Este conflicto deberá considerarse durante la <u>definición</u> de los
<u>requisitos</u> del <u>sistema</u> para evitar que la búsqueda de mayor profundidad
de <u>información</u> perjudique la facilidad de uso esperada por el <u>usuario</u>
estándar o que la simplificación de la <u>experiencia</u> limite la <u>información</u>
requerida por los <u>usuarios avanzados</u>.

---

### 3. <u>Requisitos</u> funcionales

#### 3.1 Resumen

| ID | <u>Nombre</u> | <u>Prioridad</u> | <u>Origen</u> |
| --- | --- | --- | --- |
| RF-001 | Identificar <u>especies</u> mediante una <u>imagen</u> | Imprescindible | <u>Documento</u> de <u>requisitos</u> inicial |
| RF-002 | Consultar <u>información</u> de una <u>especie</u> | Imprescindible | <u>Documento</u> de <u>requisitos</u> inicial y entrevista de elicitación |
| RF-003 | Mostrar el <u>nivel de confianza</u> | Imprescindible | <u>Documento</u> de <u>requisitos</u> inicial y entrevista de elicitación |
| RF-004 | Registrar <u>identificaciones confirmadas</u> | Importante | <u>Documento</u> de <u>requisitos</u> inicial y entrevista de elicitación |
| RF-005 | Notificar una <u>especie</u> no reconocida | Imprescindible | <u>Documento</u> de <u>requisitos</u> inicial |
| RF-006 | Consultar <u>especies visualmente similares</u> | Importante | Visión del <u>producto</u> |
| RF-007 | Registrar <u>observaciones</u> avanzadas | Importante | Visión del <u>producto</u> |
| RF-008 | Identificar <u>especies</u> de <u>importancia médica</u> sin <u>conexión</u> | Imprescindible | Visión del <u>producto</u> y entrevista de elicitación |
| RF-009 | Descargar <u>datos regionales</u> para uso offline | Importante | Derivado de RF-008 |
| RF-010 | Notificar una <u>identificación de baja confianza</u> | Imprescindible | Entrevista de elicitación y especificación |
| RF-011 | Mostrar una posible <u>identificación</u> | Importante | Entrevista de elicitación |
| RF-012 | Solicitar una nueva <u>captura</u> por <u>calidad</u> insuficiente | Importante | Visión del <u>producto</u> y entrevista de elicitación |
| RF-013 | Capturar una <u>imagen</u> para <u>identificación</u> | Imprescindible | Derivado de CU-01 y <u>observación</u> docente |
| RF-014 | Consultar el <u>historial</u> de <u>identificaciones</u> | Importante | Derivado de CU-02 y <u>revisión</u> de la dupla |
| RF-015 | Autenticar <u>usuarios</u> y administrar <u>sesiones</u> | Importante | Propuesta para resolver referencias a <u>cuentas</u>; pendiente de validar <u>alcance</u> |

#### 3.2 Fichas

##### RF-001 · Identificar <u>especies</u> mediante una <u>imagen</u>

| Campo | Contenido |
| --- | --- |
| **<u>Descripción</u>** | El <u>sistema</u> identifica la <u>especie</u> de <u>flora</u> o <u>fauna</u> presente en una <u>imagen</u> capturada mediante la <u>cámara</u> del <u>dispositivo</u> móvil. |
| **<u>Origen</u>** | <u>Documento</u> de <u>requisitos</u> inicial. |
| **<u>Prioridad</u>** | Imprescindible |
| **<u>Criterio de aceptación</u>** | Al proporcionar una <u>imagen</u> de una <u>especie</u> incluida en el <u>modelo</u> disponible, el <u>sistema</u> procesa la <u>imagen</u> y genera un <u>resultado</u> de <u>identificación</u>. |
| **Relacionado con** | RF-002, RF-003, RF-005, RF-006, RF-010, RF-011, RF-012, RNF-CON-001, RNF-CON-002, RNF-CON-003, RNF-REN-001 |

##### RF-002 · Consultar <u>información</u> de una <u>especie</u>

| Campo | Contenido |
| --- | --- |
| **<u>Descripción</u>** | El <u>sistema</u> muestra el <u>nombre común</u>, <u>nombre científico</u>, <u>región</u> y <u>nivel</u> de <u>riesgo</u> o <u>importancia médica</u> de la <u>especie</u> identificada. |
| **<u>Origen</u>** | <u>Documento</u> de <u>requisitos</u> inicial. La entrevista de elicitación confirmó el interés por consultar <u>información</u> descriptiva y de <u>importancia médica</u>. |
| **<u>Prioridad</u>** | Imprescindible |
| **<u>Criterio de aceptación</u>** | Al obtener una <u>identificación confirmada</u>, el <u>sistema</u> presenta el <u>nombre común</u>, <u>nombre científico</u>, <u>región</u> y <u>nivel</u> de <u>riesgo</u> o <u>importancia médica</u> registrados para la <u>especie</u>. |
| **Relacionado con** | RF-001, RF-003, RF-006 |

##### RF-003 · Mostrar el <u>nivel de confianza</u>

| Campo | Contenido |
| --- | --- |
| **<u>Descripción</u>** | El <u>sistema</u> muestra el <u>nivel de confianza</u> asociado a cada <u>resultado</u> de <u>identificación</u>. |
| **<u>Origen</u>** | <u>Documento</u> de <u>requisitos</u> inicial y entrevista de elicitación. El entrevistado indicó que conocer la certeza del <u>resultado</u> influye en la <u>confianza</u> para actuar sobre la <u>identificación</u>. |
| **<u>Prioridad</u>** | Imprescindible |
| **<u>Criterio de aceptación</u>** | Después de procesar una <u>imagen</u>, el <u>resultado</u> presenta el <u>porcentaje</u> de <u>confianza</u> asociado a la <u>identificación</u> obtenida. |
| **Relacionado con** | RF-001, RF-005, RF-010, RF-011 |

##### RF-004 · Registrar <u>identificaciones confirmadas</u>

| Campo | Contenido |
| --- | --- |
| **<u>Descripción</u>** | El <u>sistema</u> registra en el <u>historial</u> únicamente las <u>identificaciones</u> que alcanzan el <u>nivel de confianza</u> requerido para presentarse como confirmadas. |
| **<u>Origen</u>** | <u>Documento</u> de <u>requisitos</u> inicial. La entrevista de elicitación confirmó que conservar <u>información</u> de <u>identificaciones</u> anteriores aporta <u>valor</u> al <u>usuario</u>. La exclusión de <u>identificaciones</u> no confirmadas fue definida durante la especificación. |
| **<u>Prioridad</u>** | Importante |
| **<u>Criterio de aceptación</u>** | Cuando una <u>identificación</u> alcanza el <u>nivel de confianza</u> requerido para presentarse como confirmada, el <u>sistema</u> la registra en el <u>historial</u>. Si el <u>resultado</u> se presenta únicamente como posible <u>identificación</u> por no alcanzar el <u>nivel de confianza</u> requerido, el <u>sistema</u> no lo registra en el <u>historial</u>. |
| **Relacionado con** | RF-001, RF-003, RF-010, RF-011, RNF-SEG-001, RNF-ESC-001 |

##### RF-005 · Notificar una <u>especie</u> no reconocida

| Campo | Contenido |
| --- | --- |
| **<u>Descripción</u>** | El <u>sistema</u> notifica al <u>usuario</u> que la <u>especie</u> no pudo reconocerse cuando el <u>modelo</u> regional no ofrece una <u>identificación</u> válida. |
| **<u>Origen</u>** | <u>Documento</u> de <u>requisitos</u> inicial. |
| **<u>Prioridad</u>** | Imprescindible |
| **<u>Criterio de aceptación</u>** | Al analizar una <u>especie</u> que no pueda ser identificada mediante el <u>modelo</u> disponible, el <u>sistema</u> informa que no fue posible realizar la <u>identificación</u> y no presenta una <u>especie</u> como <u>resultado</u> confirmado. |
| **Relacionado con** | RF-001, RF-003, RF-010, RF-011 |

##### RF-006 · Consultar <u>especies visualmente similares</u>

| Campo | Contenido |
| --- | --- |
| **<u>Descripción</u>** | El <u>sistema</u> muestra <u>especies visualmente similares</u> presentes en la <u>región</u> de la <u>especie</u> identificada. |
| **<u>Origen</u>** | Visión del <u>producto</u>. |
| **<u>Prioridad</u>** | Importante |
| **<u>Criterio de aceptación</u>** | Al consultar el <u>resultado</u> de una <u>especie</u> que <u>cuenta</u> con <u>especies</u> similares registradas para la <u>región</u>, el <u>sistema</u> muestra dichas <u>especies</u> como referencias adicionales. |
| **Relacionado con** | RF-001, RF-002 |

##### RF-007 · Registrar <u>observaciones</u> avanzadas

| Campo | Contenido |
| --- | --- |
| **<u>Descripción</u>** | El <u>sistema</u> permite al <u>usuario avanzado</u> guardar una <u>observación</u> asociada a una <u>identificación</u>, con <u>especie</u> candidata o confirmada, <u>fecha</u>, <u>región</u> y notas opcionales, para <u>documentación</u> y <u>consulta</u> privada. La conservación de <u>fotografías</u> y <u>ubicación</u> exacta requiere <u>consentimiento</u> y <u>definición</u> posterior de <u>alcance</u>. |
| **<u>Origen</u>** | Visión del <u>producto</u>. |
| **<u>Prioridad</u>** | Importante |
| **<u>Criterio de aceptación</u>** | Después de que un <u>usuario avanzado</u> realiza una <u>identificación</u>, los <u>datos</u> asociados quedan registrados y disponibles para su <u>consulta</u> posterior. |
| **Relacionado con** | RF-001, RF-004, RNF-SEG-001 |

##### RF-008 · Identificar <u>especies</u> de <u>importancia médica</u> sin <u>conexión</u>

| Campo | Contenido |
| --- | --- |
| **<u>Descripción</u>** | El <u>sistema</u> identifica <u>especies</u> de <u>importancia médica</u> sin <u>conexión</u> a <u>Internet</u> cuando el <u>usuario</u> dispone previamente de los <u>datos</u> correspondientes a su <u>región</u>. |
| **<u>Origen</u>** | Visión del <u>producto</u> y entrevista de elicitación. El entrevistado identificó como relevante disponer offline de <u>información</u> relacionada con <u>especies</u> de <u>importancia médica</u>. |
| **<u>Prioridad</u>** | Imprescindible |
| **<u>Criterio de aceptación</u>** | Con el <u>dispositivo</u> sin <u>conexión</u> a <u>Internet</u> y con los <u>datos regionales</u> previamente disponibles, el <u>sistema</u> procesa una <u>imagen</u> correspondiente a una <u>especie</u> de <u>importancia médica</u> incluida en dichos <u>datos</u> y genera un <u>resultado</u> de <u>identificación</u>. |
| **Relacionado con** | RF-001, RF-003, RF-009, RF-010, RF-012, RNF-CON-003 |

##### RF-009 · Descargar <u>datos regionales</u> para uso offline

| Campo | Contenido |
| --- | --- |
| **<u>Descripción</u>** | El <u>sistema</u> permite al <u>usuario</u> descargar los <u>datos</u> de una <u>región</u> necesarios para realizar <u>identificaciones</u> offline de <u>especies</u> de <u>importancia médica</u>. |
| **<u>Origen</u>** | Derivado de RF-008 y de la Visión del <u>producto</u>. |
| **<u>Prioridad</u>** | Importante |
| **<u>Criterio de aceptación</u>** | Cuando el <u>usuario</u> selecciona una <u>región</u> disponible y solicita su <u>descarga</u> con <u>conexión</u> a <u>Internet</u>, el <u>sistema</u> almacena los <u>datos</u> necesarios y posteriormente los reconoce como disponibles para <u>identificación</u> offline. |
| **Relacionado con** | RF-008 |

##### RF-010 · Notificar una <u>identificación de baja confianza</u>

| Campo | Contenido |
| --- | --- |
| **<u>Descripción</u>** | El <u>sistema</u> informa al <u>usuario</u> cuando una <u>identificación</u> no alcanza el <u>nivel</u> mínimo de <u>confianza</u> requerido para presentarse como confirmada. |
| **<u>Origen</u>** | Entrevista de elicitación y especificación. La entrevista confirmó la <u>necesidad</u> de comunicar la <u>incertidumbre</u>; los umbrales fueron definidos posteriormente durante la especificación. |
| **<u>Prioridad</u>** | Imprescindible |
| **<u>Criterio de aceptación</u>** | Si una <u>identificación</u> general obtiene una <u>confianza</u> inferior al 90 %, o una <u>identificación</u> de <u>importancia médica</u> obtiene una <u>confianza</u> inferior al 99 %, el <u>sistema</u> informa que el <u>resultado</u> no alcanza la <u>confianza</u> requerida y no lo presenta como <u>identificación confirmada</u>. |
| **Relacionado con** | RF-001, RF-003, RF-005, RF-011, RNF-CON-002, RNF-CON-003 |

##### RF-011 · Mostrar una posible <u>identificación</u>

| Campo | Contenido |
| --- | --- |
| **<u>Descripción</u>** | El <u>sistema</u> muestra la <u>especie</u> con mayor <u>nivel de confianza</u> como posible <u>identificación</u> cuando el <u>resultado</u> no alcanza el <u>umbral</u> requerido para presentarse como confirmado. |
| **<u>Origen</u>** | Entrevista de elicitación. El entrevistado indicó que, ante una <u>identificación</u> incierta, espera conocer la mejor aproximación disponible sin ocultar la <u>incertidumbre</u>. |
| **<u>Prioridad</u>** | Importante |
| **<u>Criterio de aceptación</u>** | Cuando existe al menos una <u>especie</u> candidata pero ninguna alcanza el <u>umbral</u> correspondiente, el <u>sistema</u> muestra la candidata con mayor <u>confianza</u> identificándola explícitamente como posible <u>identificación</u> y muestra su <u>nivel de confianza</u>. |
| **Relacionado con** | RF-003, RF-005, RF-010 |

##### RF-012 · Solicitar una nueva <u>captura</u> por <u>calidad</u> insuficiente

| Campo | Contenido |
| --- | --- |
| **<u>Descripción</u>** | El <u>sistema</u> solicita una nueva <u>captura</u> cuando detecta que la <u>imagen</u> es inadecuada para la <u>identificación</u> y presenta una recomendación de mejora. |
| **<u>Origen</u>** | Visión del <u>producto</u>. La entrevista de elicitación reforzó este <u>requisito</u> al identificar <u>fotografías</u> con contraluz, poca iluminación o colores poco visibles como una dificultad del <u>proceso</u> actual. |
| **<u>Prioridad</u>** | Importante |
| **<u>Criterio de aceptación</u>** | Cuando una <u>imagen</u> no cumple las <u>condiciones</u> mínimas necesarias para realizar la <u>identificación</u>, el <u>sistema</u> no presenta una <u>especie</u> como <u>resultado</u>, solicita una nueva <u>captura</u> y muestra recomendaciones para mejorar la <u>imagen</u>. |
| **Relacionado con** | RF-001, RF-008, RF-010, RNF-CON-002, RNF-CON-003 |

---

#### 3.3 <u>Requisitos</u> incorporados en la <u>revisión</u> 1.2

##### RF-013 · Capturar una <u>imagen</u> para <u>identificación</u>

| Campo | Contenido |
| --- | --- |
| <u>Descripción</u> | El <u>sistema</u> permite capturar una <u>imagen</u> del organismo mediante la <u>cámara</u> del <u>dispositivo</u> móvil para utilizarla en el <u>proceso</u> de <u>identificación</u>. |
| <u>Origen</u> | Derivado del <u>flujo</u> del <u>prototipo</u> y de la <u>observación</u> docente sobre la separación de <u>casos de uso</u>. |
| <u>Prioridad</u> | Imprescindible |
| <u>Criterio de aceptación</u> | Con <u>permiso</u> de <u>cámara</u> concedido, al pulsar capturar, el <u>sistema</u> obtiene una <u>imagen</u> y permite continuar a la verificación de <u>calidad</u>; si se cancela, no inicia <u>identificación</u>. |
| Relacionado con | RF-001, RF-012, CU-06 |

##### RF-014 · Consultar el <u>historial</u> de <u>identificaciones</u>

| Campo | Contenido |
| --- | --- |
| <u>Descripción</u> | El <u>sistema</u> permite al <u>usuario</u> consultar la lista de sus <u>identificaciones confirmadas</u> previamente registradas. |
| <u>Origen</u> | <u>Observación</u> RD-004 de la dupla y CU-02 ya existente. |
| <u>Prioridad</u> | Importante |
| <u>Criterio de aceptación</u> | Al abrir <u>historial</u>, el <u>usuario</u> ve únicamente sus <u>identificaciones confirmadas</u>; si no existen, se muestra un <u>estado</u> vacío; no puede consultar <u>registros</u> privados de otro <u>usuario</u>. |
| Relacionado con | RF-004, RNF-SEG-001, CU-02 |

##### RF-015 · Autenticar <u>usuarios</u> y administrar <u>sesiones</u> (propuesta pendiente)

| Campo | Contenido |
| --- | --- |
| <u>Descripción</u> propuesta | El <u>sistema</u> autentica a <u>usuarios</u> que requieren acceder a <u>información</u> privada y permite cerrar la <u>sesión</u>. |
| <u>Origen</u> | RD-002 de la <u>revisión</u> de la dupla; requiere decisión de <u>alcance</u>. |
| <u>Prioridad</u> | Por definir |
| <u>Criterio de aceptación</u> propuesto | Con credenciales válidas se inicia <u>sesión</u>; con credenciales inválidas se rechaza; al cerrar <u>sesión</u> se impide acceder a <u>datos</u> privados sin <u>autenticación</u>. |
| Relacionado con | RNF-SEG-001, RF-007, RF-014 |

**Decisión pendiente:** definir si BIOMA requiere <u>cuentas</u> en su primera <u>versión</u> o si utilizará identidad local para el <u>historial</u>. RF-015 no se considera aprobado hasta resolver esta decisión.

---

### 4. <u>Requisitos</u> no funcionales

#### 4.1 Resumen

| ID | <u>Atributo</u> | <u>Nombre</u> | <u>Prioridad</u> | <u>Origen</u> |
| --- | --- | --- | --- | --- |
| RNF-CON-001 | <u>Confiabilidad</u> | <u>Calidad</u> de <u>datos</u> de referencia | Imprescindible | Derivado del tipo de <u>sistema</u> |
| RNF-CON-002 | <u>Confiabilidad</u> | <u>Precisión</u> general de <u>identificación</u> | Imprescindible | Derivado del tipo de <u>sistema</u> y especificación |
| RNF-CON-003 | <u>Confiabilidad</u> | <u>Precisión</u> en <u>especies</u> de <u>importancia médica</u> | Imprescindible | Entrevista de elicitación y especificación |
| RNF-REN-001 | <u>Rendimiento</u> | <u>Tiempo</u> de <u>identificación</u> | Imprescindible | <u>Documento</u> de <u>requisitos</u> inicial |
| RNF-SEG-001 | <u>Seguridad</u> | Protección de <u>datos</u> | Imprescindible | Derivado del tipo de <u>sistema</u> |
| RNF-ESC-001 | <u>Escalabilidad</u> | <u>Capacidad</u> del <u>historial</u> | Importante | <u>Documento</u> de <u>requisitos</u> inicial y especificación |

#### 4.2 Fichas

##### RNF-CON-001 · <u>Calidad</u> de <u>datos</u> de referencia

| Campo | Contenido |
| --- | --- |
| **<u>Atributo</u> de <u>calidad</u>** | <u>Confiabilidad</u> |
| **<u>Descripción</u>** | Los <u>datos</u> utilizados como referencia por el <u>sistema</u> corresponden a <u>especies</u> identificadas y clasificadas antes de su incorporación al conjunto de <u>datos</u> disponible. |
| **<u>Métrica</u>** | El 100 % de las <u>especies</u> incorporadas al conjunto de <u>datos</u> <u>cuenta</u> con una <u>identificación</u> y <u>clasificación</u> asociada. |
| **<u>Origen</u>** | Derivado del tipo de <u>sistema</u>: la <u>identificación</u> depende de <u>datos</u> representativos y correctamente clasificados. |
| **<u>Prioridad</u>** | Imprescindible |
| **Por qué importa** | <u>Datos</u> incorrectamente clasificados pueden provocar <u>identificaciones</u> erróneas y reducir la <u>confiabilidad</u> de los <u>resultados</u>. |
| **Afecta a** | RF-001, RF-002, RF-003, RF-005, RF-006, RF-008, RF-010, RF-011 |

##### RNF-CON-002 · <u>Precisión</u> general de <u>identificación</u>

| Campo | Contenido |
| --- | --- |
| **<u>Atributo</u> de <u>calidad</u>** | <u>Confiabilidad</u> |
| **<u>Descripción</u>** | El <u>modelo</u> alcanza una <u>precisión</u> mínima del 90 % en la <u>identificación</u> general de <u>especies</u> incluidas en el <u>modelo</u> disponible. |
| **<u>Métrica</u>** | Al menos el 90 % de las <u>identificaciones</u> realizadas sobre un conjunto de <u>imágenes</u> de <u>prueba</u> previamente clasificadas de <u>especies</u> generales debe coincidir con la <u>especie</u> correcta. |
| **<u>Origen</u>** | Derivado del tipo de <u>sistema</u>. El <u>umbral</u> mínimo del 90 % fue establecido durante la especificación de <u>requisitos</u>. |
| **<u>Prioridad</u>** | Imprescindible |
| **Por qué importa** | Una <u>precisión</u> insuficiente reduce la <u>confiabilidad</u> del <u>sistema</u> y puede proporcionar <u>información</u> incorrecta sobre las <u>especies</u> observadas. |
| **Afecta a** | RF-001, RF-003, RF-005, RF-010, RF-011 |

##### RNF-CON-003 · <u>Precisión</u> en <u>especies</u> de <u>importancia médica</u>

| Campo | Contenido |
| --- | --- |
| **<u>Atributo</u> de <u>calidad</u>** | <u>Confiabilidad</u> |
| **<u>Descripción</u>** | El <u>modelo</u> alcanza una <u>precisión</u> mínima del 99 % en la <u>identificación</u> de <u>especies</u> clasificadas como de <u>importancia médica</u> e incluidas en el <u>modelo</u> disponible. |
| **<u>Métrica</u>** | Al menos el 99 % de las <u>identificaciones</u> realizadas sobre un conjunto de <u>imágenes</u> de <u>prueba</u> previamente clasificadas de <u>especies</u> de <u>importancia médica</u> debe coincidir con la <u>especie</u> correcta. |
| **<u>Origen</u>** | Entrevista de elicitación y especificación. La entrevista estableció la <u>necesidad</u> de una certeza mayor para <u>especies</u> de <u>importancia médica</u> y el <u>umbral</u> del 99 % fue definido posteriormente durante la especificación. |
| **<u>Prioridad</u>** | Imprescindible |
| **Por qué importa** | Una <u>identificación</u> incorrecta de una <u>especie</u> de <u>importancia médica</u> puede llevar al <u>usuario</u> a interpretar incorrectamente el <u>riesgo</u> asociado con el organismo observado. |
| **Afecta a** | RF-001, RF-002, RF-003, RF-005, RF-008, RF-010, RF-011 |

##### RNF-REN-001 · <u>Tiempo</u> de <u>identificación</u>

| Campo | Contenido |
| --- | --- |
| **<u>Atributo</u> de <u>calidad</u>** | <u>Rendimiento</u> |
| **<u>Descripción</u>** | El <u>sistema</u> presenta el <u>resultado</u> de una <u>identificación</u> en un <u>tiempo</u> máximo de 15 segundos desde que el <u>usuario</u> solicita la <u>identificación</u>. |
| **<u>Métrica</u>** | <u>Tiempo</u> transcurrido desde la <u>solicitud</u> de <u>identificación</u> hasta la <u>presentación</u> del <u>resultado</u>: máximo 15 segundos. |
| **<u>Origen</u>** | <u>Documento</u> de <u>requisitos</u> inicial. |
| **<u>Prioridad</u>** | Imprescindible |
| **Por qué importa** | Un <u>tiempo</u> de <u>procesamiento</u> elevado reduce la utilidad del <u>reconocimiento</u> durante <u>actividades</u> en campo. |
| **Afecta a** | RF-001, RF-002, RF-003, RF-005, RF-008, RF-010, RF-011 |

##### RNF-SEG-001 · Protección de <u>datos</u>

| Campo | Contenido |
| --- | --- |
| **<u>Atributo</u> de <u>calidad</u>** | <u>Seguridad</u> |
| **<u>Descripción</u>** | El <u>sistema</u> restringe el <u>acceso</u> a los <u>datos</u> privados asociados a una <u>identificación</u> al <u>usuario</u> propietario de dichos <u>datos</u>. |
| **<u>Métrica</u>** | En el 100 % de las <u>pruebas</u> de <u>acceso</u> realizadas con una <u>cuenta</u> diferente a la propietaria, el <u>sistema</u> impide consultar los <u>datos</u> privados asociados a la <u>identificación</u>. |
| **<u>Origen</u>** | Derivado del tipo de <u>sistema</u>: los <u>registros</u> pueden contener <u>información</u> asociada al <u>usuario</u> o a la <u>ubicación</u> donde se realizó una <u>observación</u>. |
| **<u>Prioridad</u>** | Imprescindible |
| **Por qué importa** | El <u>acceso</u> no autorizado puede comprometer la <u>privacidad</u> del <u>usuario</u> y revelar <u>información</u> sobre la <u>ubicación</u> de determinadas <u>especies</u>. |
| **Afecta a** | RF-004, RF-007 |

##### RNF-ESC-001 · <u>Capacidad</u> del <u>historial</u>

| Campo | Contenido |
| --- | --- |
| **<u>Atributo</u> de <u>calidad</u>** | <u>Escalabilidad</u> |
| **<u>Descripción</u>** | El <u>historial</u> de un <u>usuario estándar</u> conserva un máximo de 50 <u>identificaciones</u> y, al registrar una nueva <u>identificación</u> cuando se alcanza este <u>límite</u>, elimina la <u>identificación</u> más antigua. |
| **<u>Métrica</u>** | El <u>historial</u> mantiene un máximo de 50 <u>identificaciones</u> simultáneamente. Al registrar la <u>identificación</u> número 51, se elimina la <u>identificación</u> con mayor antigüedad y el <u>historial</u> permanece con 50 <u>registros</u>. |
| **<u>Origen</u>** | <u>Documento</u> de <u>requisitos</u> inicial. El comportamiento al alcanzar el <u>límite</u> fue definido durante la especificación de <u>requisitos</u>. |
| **<u>Prioridad</u>** | Importante |
| **Por qué importa** | Establecer un <u>límite</u> permite controlar la cantidad de <u>identificaciones</u> conservadas para un <u>usuario estándar</u> y define de manera predecible el comportamiento del <u>historial</u> cuando alcanza su <u>capacidad</u> máxima. |
| **Afecta a** | RF-004 |

---

### 5. <u>Casos de uso</u>

La <u>revisión</u> docente identificó que CU-01 reunía <u>captura</u>, <u>validación</u> de <u>imagen</u>, <u>identificación</u> y <u>consulta</u> del <u>resultado</u>. La <u>versión</u> 1.2 separa estas <u>responsabilidades</u> en <u>casos de uso</u> con un <u>objetivo</u> principal definido. Se conserva CU-01 como <u>identificación</u> para mantener la <u>trazabilidad</u> histórica. Los casos nuevos deben incorporarse también al <u>diagrama</u> editable de `docs/diagramas/casos-de-uso.drawio` y exportarse nuevamente a PNG; esta actualización documental no significa que el <u>archivo</u> gráfico ya se haya modificado.

#### 5.1 <u>Catálogo</u> revisado

| ID | <u>Caso de uso</u> | <u>Actor</u> principal | <u>Requisitos</u> |
| --- | --- | --- | --- |
| CU-01 | Identificar una <u>especie</u> a partir de una <u>imagen</u> válida | Estándar / avanzado | RF-001, RF-003, RF-005, RF-010, RF-011 |
| CU-02 | Consultar <u>historial</u> de <u>identificaciones</u> | Estándar / avanzado | RF-014 |
| CU-03 | Registrar <u>observación</u> avanzada | Avanzado | RF-007 |
| CU-04 | Identificar una <u>especie</u> de <u>importancia médica</u> sin <u>conexión</u> | Estándar / avanzado | RF-008, RF-003, RF-010 |
| CU-05 | Descargar <u>datos regionales</u> para uso offline | Estándar / avanzado | RF-009 |
| CU-06 | Capturar <u>imagen</u> de una <u>especie</u> | Estándar / avanzado | RF-013 |
| CU-07 | Verificar <u>calidad</u> de <u>imagen</u> capturada | Estándar / avanzado | RF-012 |
| CU-08 | Consultar <u>información</u> de una <u>especie</u> | Estándar / avanzado | RF-002, RF-006 |
| CU-09 | Registrar <u>identificación confirmada</u> | Estándar / avanzado | RF-004 |
| CU-10 | Consultar <u>nivel de confianza</u> de una <u>identificación</u> | Estándar / avanzado | RF-003 |

**Nota de modelado:** los CU-07 y CU-09 representan comportamientos automáticos iniciados dentro de un <u>objetivo</u> del <u>usuario</u>. En el <u>diagrama</u> UML se pueden representar como inclusiones (`<<include>>`) cuando proceda, sin presentarlos como acciones manuales independientes. CU-10 puede integrarse en CU-08 si se prefiere evitar un <u>caso de uso</u> sin <u>objetivo</u> autónomo.

#### 5.2 Fichas de <u>casos de uso</u>

##### CU-06 · Capturar <u>imagen</u> de una <u>especie</u>

| Campo | Contenido |
| --- | --- |
| <u>Actor</u> | <u>Usuario estándar</u> o avanzado |
| <u>Objetivo</u> | Proporcionar una <u>fotografía</u> para su análisis. |
| <u>Precondición</u> | La <u>aplicación</u> está abierta y tiene <u>permiso</u> para usar la <u>cámara</u>. |
| <u>Flujo</u> principal | 1. El <u>usuario</u> abre la <u>cámara</u>. 2. Enfoca el organismo. 3. <u>Captura</u> la <u>fotografía</u>. 4. El <u>sistema</u> entrega la <u>imagen</u> a la verificación de <u>calidad</u>. |
| Alternos | A1. Si se deniega el <u>permiso</u>, se solicita habilitarlo. A2. Si el <u>usuario</u> cancela, no se procesa ni registra ninguna <u>imagen</u>. |
| <u>Postcondición</u> | <u>Imagen</u> capturada disponible temporalmente para verificación. |
| <u>Requisitos</u> | RF-013 |

##### CU-07 · Verificar <u>calidad</u> de <u>imagen</u> capturada

| Campo | Contenido |
| --- | --- |
| <u>Actor</u> | <u>Usuario estándar</u> o avanzado (inicia la <u>captura</u>); <u>sistema</u> (ejecuta la verificación) |
| <u>Objetivo</u> | Determinar si la <u>imagen</u> puede utilizarse para <u>identificación</u>. |
| <u>Precondición</u> | Existe una <u>imagen</u> capturada. |
| <u>Flujo</u> principal | 1. El <u>sistema</u> evalúa <u>condiciones</u> mínimas de <u>calidad</u>. 2. La <u>imagen</u> resulta adecuada. 3. El <u>sistema</u> habilita la <u>identificación</u>. |
| Alternos | A1. Si la <u>imagen</u> es inadecuada, el <u>sistema</u> indica el problema y recomienda mejorar iluminación o enfoque; permite repetir la <u>captura</u> sin enviar la <u>imagen</u> al <u>reconocimiento</u>. |
| <u>Postcondición</u> | <u>Imagen</u> aceptada o nueva <u>captura</u> solicitada. |
| <u>Requisitos</u> | RF-012 |

##### CU-01 · Identificar una <u>especie</u> a partir de una <u>imagen</u> válida

| Campo | Contenido |
| --- | --- |
| <u>Actor</u> | <u>Usuario estándar</u> o avanzado |
| <u>Objetivo</u> | Obtener una <u>identificación</u> de la <u>especie</u> presente en una <u>imagen</u> válida. |
| <u>Precondición</u> | Existe una <u>imagen</u> validada y un <u>modelo</u> regional disponible. |
| <u>Flujo</u> principal | 1. El <u>usuario</u> solicita identificar la <u>imagen</u>. 2. El <u>sistema</u> procesa la <u>imagen</u> con el <u>modelo</u> disponible. 3. Obtiene una <u>especie</u> candidata y un <u>valor</u> de <u>confianza</u>. 4. Compara la <u>confianza</u> con el <u>umbral</u> correspondiente (90 % general; 99 % <u>importancia médica</u>). 5. Si cumple, presenta <u>identificación confirmada</u> y habilita la <u>consulta</u> de su <u>información</u>. |
| Alternos | A1. <u>Especie</u> fuera del <u>modelo</u>: notifica que no fue reconocida, sin confirmar ni registrar. A2. <u>Confianza</u> insuficiente: muestra <u>advertencia</u> y, si existe candidata, la presenta únicamente como posible <u>identificación</u> con <u>porcentaje</u>; no la registra como confirmada. A3. <u>Modelo</u> regional no disponible: informa que no puede procesarse la <u>solicitud</u>. |
| <u>Postcondición</u> | <u>Resultado</u> confirmado, posible o no reconocido; solo los confirmados son elegibles para <u>historial</u>. |
| <u>Requisitos</u> | RF-001, RF-003, RF-005, RF-010, RF-011, RNF-CON-002, RNF-CON-003, RNF-REN-001 |

##### CU-08 · Consultar <u>información</u> de una <u>especie</u>

| Campo | Contenido |
| --- | --- |
| <u>Actor</u> | <u>Usuario estándar</u> o avanzado |
| <u>Objetivo</u> | Conocer la <u>información</u> de la <u>especie</u> identificada. |
| <u>Precondición</u> | Existe un <u>resultado</u> o <u>especie</u> seleccionada con <u>información</u> disponible. |
| <u>Flujo</u> principal | 1. El <u>usuario</u> abre el detalle. 2. El <u>sistema</u> muestra <u>nombre común</u>, científico, <u>región</u> e <u>importancia médica</u>. 3. Muestra <u>especies</u> similares cuando están disponibles. |
| Alternos | A1. Sin <u>especies</u> similares: omite esa sección. A2. <u>Resultado</u> posible: conserva una <u>advertencia</u> visible de <u>incertidumbre</u>. |
| <u>Postcondición</u> | <u>Información</u> consultada sin alterar la <u>identificación</u>. |
| <u>Requisitos</u> | RF-002, RF-006, RF-003 |

##### CU-09 · Registrar <u>identificación confirmada</u>

| Campo | Contenido |
| --- | --- |
| <u>Actor</u> | <u>Usuario estándar</u> o avanzado (beneficiario); <u>sistema</u> (registra) |
| <u>Objetivo</u> | Conservar una <u>identificación confirmada</u> en el <u>historial</u>. |
| <u>Precondición</u> | La <u>identificación</u> alcanzó su <u>umbral</u> de <u>confianza</u>. |
| <u>Flujo</u> principal | 1. El <u>sistema</u> registra <u>especie</u>, <u>fecha</u>, <u>región</u> y <u>confianza</u>. 2. El <u>registro</u> queda asociado al <u>usuario</u>. |
| Alternos | A1. Si es <u>usuario estándar</u> y existen 50 <u>registros</u>, elimina el más antiguo antes de incorporar el nuevo. A2. Si el <u>resultado</u> no es confirmado, no lo registra. A3. Si falla el <u>almacenamiento</u>, informa el error sin afirmar que se guardó. |
| <u>Postcondición</u> | <u>Historial</u> actualizado o error comunicado. |
| <u>Requisitos</u> | RF-004, RNF-ESC-001, RNF-SEG-001 |

##### CU-02 · Consultar <u>historial</u> de <u>identificaciones</u>

| Campo | Contenido |
| --- | --- |
| <u>Actor</u> | <u>Usuario estándar</u> o avanzado |
| <u>Objetivo</u> | Recuperar las <u>identificaciones confirmadas</u> propias. |
| <u>Precondición</u> | <u>Usuario</u> identificado por el mecanismo de <u>acceso</u> definido para la <u>versión</u>. |
| <u>Flujo</u> principal | 1. Abre <u>historial</u>. 2. El <u>sistema</u> obtiene únicamente sus <u>registros</u>. 3. Muestra la lista y permite abrir un <u>registro</u>. |
| Alternos | A1. Sin <u>registros</u>: muestra <u>estado</u> vacío. A2. Sin <u>conexión</u> y sin <u>datos</u> locales: informa indisponibilidad. A3. <u>Acceso</u> a <u>registros</u> ajenos: rechaza la <u>solicitud</u>. |
| <u>Postcondición</u> | <u>Consulta</u> realizada sin modificar los <u>registros</u>. |
| <u>Requisitos</u> | RF-014, RNF-SEG-001 |

##### CU-03 · Registrar <u>observación</u> avanzada

| Campo | Contenido |
| --- | --- |
| <u>Actor</u> | <u>Usuario avanzado</u> |
| <u>Objetivo</u> | Documentar una <u>observación</u> de campo. |
| <u>Precondición</u> | <u>Usuario</u> con <u>perfil</u> avanzado y <u>especie</u> o <u>resultado</u> disponible. |
| <u>Flujo</u> principal | 1. Abre <u>registro</u> de <u>observación</u>. 2. Agrega notas opcionales. 3. Confirma guardar. 4. El <u>sistema</u> almacena los <u>datos</u> autorizados de forma privada. |
| Alternos | A1. Cancelación: no almacena. A2. <u>Datos</u> obligatorios faltantes: solicita completarlos. A3. <u>Usuario</u> sin <u>permisos</u>: rechaza la <u>operación</u>. |
| <u>Postcondición</u> | <u>Observación</u> privada almacenada o rechazo explicado. |
| <u>Requisitos</u> | RF-007, RNF-SEG-001 |

##### CU-04 · Identificar una <u>especie</u> de <u>importancia médica</u> sin <u>conexión</u>

| Campo | Contenido |
| --- | --- |
| <u>Actor</u> | <u>Usuario estándar</u> o avanzado |
| <u>Objetivo</u> | Identificar una <u>especie</u> de <u>importancia médica</u> sin <u>Internet</u>. |
| <u>Precondición</u> | Paquete regional y <u>recursos</u> de inferencia offline compatibles ya descargados. |
| <u>Flujo</u> principal | 1. El <u>usuario</u> solicita <u>identificación</u> offline con una <u>imagen</u> válida. 2. El <u>sistema</u> utiliza <u>recursos</u> locales. 3. Aplica el <u>umbral</u> de <u>confianza</u> del 99 %. 4. Muestra el <u>resultado</u> con su <u>nivel</u> de certeza. |
| Alternos | A1. Paquete no disponible: informa que debe descargarse con <u>Internet</u>. A2. <u>Confianza</u> inferior al 99 %: presenta solo posible <u>identificación</u> y <u>advertencia</u>. A3. <u>Especie</u> no incluida: informa que no fue reconocida. |
| <u>Postcondición</u> | <u>Resultado</u> disponible sin depender de inferencia en la nube. |
| <u>Requisitos</u> | RF-008, RF-003, RF-010, RF-011 |

##### CU-05 · Descargar <u>datos regionales</u> para uso offline

| Campo | Contenido |
| --- | --- |
| <u>Actor</u> | <u>Usuario estándar</u> o avanzado |
| <u>Objetivo</u> | Preparar <u>recursos</u> regionales para <u>identificación</u> sin <u>Internet</u>. |
| <u>Precondición</u> | Existe <u>conexión</u> a <u>Internet</u> y un paquete regional publicado. |
| <u>Flujo</u> principal | 1. Selecciona <u>región</u>. 2. Solicita <u>descarga</u>. 3. El <u>sistema</u> <u>descarga</u> y verifica el paquete. 4. Confirma <u>disponibilidad</u> offline. |
| Alternos | A1. <u>Descarga</u> interrumpida: informa <u>fallo</u> y permite reintentar. A2. <u>Almacenamiento</u> insuficiente: informa espacio requerido. |
| <u>Postcondición</u> | Paquete regional verificado y disponible o error comunicado. |
| <u>Requisitos</u> | RF-009 |

#### 5.3 <u>Relaciones</u> recomendadas para actualizar el <u>diagrama</u> UML

- CU-01 `<<include>>` CU-07 únicamente si el <u>flujo</u> de <u>identificación</u> siempre realiza esa verificación; si CU-07 ya se ejecutó al capturar, evitar duplicarla.
- CU-01 puede desencadenar CU-09 al confirmar una <u>identificación</u>, como comportamiento automático condicionado, no como `<<include>>` incondicional.
- CU-08 puede iniciarse desde el <u>resultado</u> de CU-01; no es obligatorio incluirlo para que la <u>identificación</u> concluya.
- CU-04 reutiliza la lógica de <u>identificación</u> de CU-01 con <u>recursos</u> locales y <u>umbral</u> médico, sin exigir un segundo <u>flujo</u> de <u>captura</u> independiente.

---

### 6. <u>Trazabilidad</u>

La columna **<u>Estado</u> de <u>documentación</u>** indica que el <u>requisito</u> está especificado, no que se haya implementado o demostrado. Las referencias de <u>pantallas</u> corresponden al <u>prototipo</u> V1 previamente documentado; las nuevas <u>pantallas</u> o <u>cambios</u> del <u>diagrama</u> siguen pendientes de verificación.

| <u>Requisito</u> | <u>Caso de uso</u> | <u>Pantalla</u> V1 | <u>Estado</u> de <u>documentación</u> |
| --- | --- | --- | --- |
| RF-001 | CU-01, CU-04 | P04, P05 | Actualizado |
| RF-002 | CU-08 | P05 | Actualizado |
| RF-003 | CU-01, CU-04, CU-08, CU-10 | P05, A-02 | Actualizado |
| RF-004 | CU-09 | P05, P06 | Actualizado |
| RF-005 | CU-01, CU-04 | — | Actualizado; representación pendiente |
| RF-006 | CU-08 | P05 | Actualizado |
| RF-007 | CU-03 | — | Revisado; <u>alcance</u> de <u>datos</u> pendiente |
| RF-008 | CU-04 | — | Actualizado; representación pendiente |
| RF-009 | CU-05 | — | Actualizado; representación pendiente |
| RF-010 | CU-01, CU-04 | A-02 | Actualizado |
| RF-011 | CU-01, CU-04 | A-02 | Actualizado |
| RF-012 | CU-07 | A-01 | Actualizado |
| RF-013 | CU-06 | P02, P03 | Nuevo; representado en V1 |
| RF-014 | CU-02 | P06 | Nuevo; representado en V1 |
| RF-015 | Pendiente de <u>caso de uso</u> y decisión de <u>alcance</u> | — | Propuesto, no aprobado |
| RNF-CON-001 | CU-01, CU-04 | — | Pendiente de <u>prueba</u> |
| RNF-CON-002 | CU-01 | — | Pendiente de <u>prueba</u> |
| RNF-CON-003 | CU-01, CU-04 | — | Pendiente de <u>prueba</u> |
| RNF-REN-001 | CU-01, CU-04 | P04 | Pendiente de medición |
| RNF-SEG-001 | CU-02, CU-03, CU-09 | — | Pendiente de <u>prueba</u> |
| RNF-ESC-001 | CU-02, CU-09 | P06 | Pendiente de <u>prueba</u> |

---

---

## 2. Filtro de sustantivos y clases candidatas

Se aplican las cuatro razones de descarte vistas en clase: **atributo de otra clase**, **sinónimo**, **actor o sistema externo** y **término demasiado vago**. Se consideran también las responsabilidades propias de cada objeto.

| Clase candidata | Por qué permanece | Responsabilidad principal |
| --- | --- | --- |
| `Especie` | Tiene identidad y características propias dentro del catálogo. | Mantener la información taxonómica y de riesgo de la especie. |
| `Identificacion` | Representa un resultado concreto, distinto del catálogo de especies. | Conservar predicción, confianza y estado de confirmación. |
| `Usuario` | Participa en permisos, historial y tipos de experiencia. | Representar el perfil y las autorizaciones del usuario. |
| `Historial` | Agrupa identificaciones confirmadas con reglas de conservación. | Registrar y consultar identificaciones permitidas. |
| `Observacion` | Representa los datos adicionales aportados por usuarios avanzados. | Validar y conservar información complementaria. |
| `Region` | Identifica el ámbito geográfico y el catálogo aplicable. | Determinar la pertenencia regional de las especies. |
| `PaqueteRegional` | Tiene ciclo de vida de descarga y disponibilidad offline. | Administrar recursos regionales descargables. |
| `ResultadoInferencia` | Separa la salida del modelo de la identificación confirmada. | Representar especies candidatas y valores de confianza. |

**Resultado:** ocho clases candidatas. `ResultadoInferencia` y `PaqueteRegional` son decisiones de diseño propuestas; deberán validarse durante la elaboración del diagrama de clases.

## 3. ¿Qué sabe y qué hace cada clase?

| Clase | Qué sabe (atributos candidatos) | Qué hace (operaciones candidatas) |
| --- | --- | --- |
| `Especie` | ID, nombre común, nombre científico, región, importancia médica, nivel de riesgo. | `esDeImportanciaMedica()`, `obtenerFicha()`. |
| `Identificacion` | ID, especie candidata, confianza, fecha, estado, usuario asociado. | `validarConfianza()`, `confirmar()`, `esRegistrable()`. |
| `Usuario` | ID, tipo de perfil, permisos y datos de cuenta cuando apliquen. | `puedeRegistrarObservacion()`, `puedeConsultarRegistro()`. |
| `Historial` | Usuario propietario, identificaciones registradas, capacidad máxima. | `agregarConfirmada()`, `consultar()`, `aplicarLimite()`. |
| `Observacion` | ID, autor, especie relacionada, notas, fecha y datos complementarios. | `validarDatos()`, `actualizarContenido()`. |
| `Region` | ID, nombre, especies asociadas y ámbito geográfico. | `contieneEspecie()`, `listarEspecies()`. |
| `PaqueteRegional` | Región, versión, estado de descarga, recursos disponibles. | `descargar()`, `verificarDisponibilidad()`, `habilitarUsoOffline()`. |
| `ResultadoInferencia` | Especies candidatas, puntuaciones de confianza y origen de inferencia. | `obtenerMejorCandidato()`, `obtenerConfianza()`. |

**Nota de diseño:** `validarConfianza()` puede delegar en las estrategias de validación general y de importancia médica definidas previamente. Las operaciones propuestas no implican que el código ya exista. La autenticación de cuentas permanece pendiente de validación en RF-015.

## 4. Sustantivos descartados y justificación

| Sustantivo encontrado | Motivo del descarte | Justificación |
| --- | --- | --- |
| Cámara | Actor o sistema externo | Es hardware del dispositivo, no una entidad de dominio administrada por BIOMA. |
| Teléfono inteligente / dispositivo móvil | Actor o sistema externo | Plataforma física donde opera la aplicación. |
| Modelo de IA | Actor o sistema externo (respecto al dominio) | Se utiliza como servicio o componente técnico de inferencia, no como entidad principal del modelo de dominio. |
| Imagen / fotografía | Atributo de otra clase | Es entrada de la identificación; en el alcance estándar no se conserva como entidad independiente. |
| Porcentaje / nivel de confianza | Atributo de otra clase | Valor asociado al resultado de inferencia o a la identificación. |
| Nombre común / nombre científico | Atributo de otra clase | Son propiedades de `Especie`. |
| Fecha | Atributo de otra clase | Forma parte de `Identificacion` u `Observacion`. |
| Riesgo / importancia médica | Atributo de otra clase | Propiedad o clasificación de `Especie`, no objeto independiente en este alcance. |
| Identificación confirmada | Sinónimo o estado de otra clase | Es una `Identificacion` cuyo estado cumple el umbral requerido. |
| Registro de identificación | Sinónimo | Se representa mediante `Identificacion` incorporada a `Historial`. |
| Datos regionales | Sinónimo o agrupación | Se concretan en `PaqueteRegional` y su asociación con `Region`. |
| Información / datos | Término demasiado vago | No identifican una entidad con identidad y responsabilidad propias. |
| Sistema / plataforma | Término demasiado vago | Designan BIOMA en su conjunto, no una clase de dominio. |
| Resultado | Término demasiado vago | Se precisa como `ResultadoInferencia` o `Identificacion`, según la etapa. |
| Usuario estándar / usuario avanzado | Sinónimo o variante de otra clase | Son perfiles de `Usuario`; podrían especializarse si aparecen comportamientos realmente distintos. |
| Pantalla / interfaz | Fuera del modelo de dominio | Son elementos de presentación, no clases de negocio candidatas para este ejercicio. |
| Requisito / caso de uso / prototipo | Fuera del modelo de dominio | Son artefactos de análisis y documentación, no entidades operativas de BIOMA. |

**Criterio final:** un sustantivo descartado del **modelo de dominio** todavía puede existir como clase técnica, interfaz, DTO o componente de infraestructura. Este filtro únicamente identifica las clases candidatas para el diseño orientado a objetos del problema.

---

## 5. Diagrama de clases UML en Mermaid

El siguiente diagrama extiende los **ocho candidatos del punto 2** con atributos tipados, operaciones, visibilidad y relaciones con multiplicidad en ambos extremos. Las relaciones son **decisiones de diseño propuestas**, no evidencia de implementación.

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

### 5.1 Justificación de las relaciones

- **Composición (`*--`):** `Usuario` posee su `Historial`, y cada `Identificacion` contiene su `ResultadoInferencia`. Se propone que estos objetos dependientes no tengan ciclo de vida independiente del objeto contenedor.
- **Asociación (`-->`):** una identificación puede referirse a una especie del catálogo, pero la especie sigue existiendo si se elimina la identificación. De igual modo, una región y una especie pueden existir independientemente.
- **Multiplicidad:** se indica en ambos extremos de cada vínculo. El historial estándar admite hasta 50 identificaciones confirmadas, de acuerdo con RNF-ESC-001. Una identificación sin confirmación puede no tener una especie asociada como identificación confirmada.
- **Sin herencia ni agregación:** los perfiles de usuario se mantienen como atributo mientras no se justifique una especialización de comportamiento. Se prefiere asociación frente a agregación compartida, según la guía de clase.

### 5.2 Validación con un caso concreto (modelo de objetos)

Un usuario estándar de prueba, `usuario01`, realiza una identificación de una especie regional. El modelo permite crear su `Historial`, asociar la `Identificacion` a un `ResultadoInferencia`, referenciar la `Especie` y conservarla en el historial **solo si** cumple el umbral de confirmación. Si no lo cumple, la identificación permanece fuera del historial. Este escenario verifica conceptualmente las relaciones y no representa una prueba de software ejecutada.

**Referencia del diagrama independiente:** [`diagramaClases.md`](diagramaClases.md).
