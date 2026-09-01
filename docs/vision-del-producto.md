# Visión del producto

> **Plantilla del curso · Ingeniería de Software I · SIS3407**

---

**Autor: Santiago Pacheco Carrillo**
**Fecha de la última versión: 17/08/2026**
**Repositorio: Ingenieria de Software I**

---

## 1. Descripción del sistema



**Nombre del sistema: Sistema de detección de flora y fauna local para senderistas.**

**Descripción: Un sistema basado en el entrenamiento de modelos de inteligencia artificial con bases de datos localizadas de flora y fauna para la detección y despliegue de información de estas a través del uso de la cámara de un teléfono inteligente.**\
**El sistema se orienta a senderistas que buscan identificar las especies de animales con las que se encuentran en sus rutas.**

---

## 2. Problema y usuarios


**El problema: Dificultad para identificar de manera rápida y accesible especies de flora y fauna propias de una región en zonas naturales.**

**Cómo se resuelve hoy sin el sistema: Observación del organismo → registro de características → comparación con referencias → descarte de especies → identificación probable → validación por experto**

**Usuarios del sistema:**

| Tipo de usuario | Qué necesita del sistema | Qué le preocupa |
|---|---|---|
|Usuario estándar — excursionista, turista o persona interesada en la naturaleza |Facilidad de uso y acceso rápido al reconocimiento mediante la cámara, con una experiencia similar a Shazam: apuntar y obtener una identificación sin conocimientos especializados |Que la identificación sea incorrecta o tarde demasiado. Necesita una respuesta rápida acompañada de fotografías y características visuales que le permitan corroborar que la especie identificada corresponde con lo que está observando |
|Usuario avanzado — estudiantes, científicos, investigadores o entusiastas con conocimientos de flora y fauna |Acceso a información detallada y técnica de la especie identificada: nombre científico, taxonomía, nivel de confianza, características distintivas y especies similares. Además, debe tener acceso preliminar a bases de datos y modelos en fase beta, con una cobertura considerablemente mayor de especies por región. El sistema debe permitirle registrar, organizar y documentar observaciones de flora y fauna de la zona, aprovechando las identificaciones realizadas para generar información útil para estudios biológicos, monitoreo de especies o trabajo de campo.|La precisión y confiabilidad de la identificación, especialmente ante especies visualmente similares. Le preocupa poder distinguir resultados confiables de identificaciones inciertas y contar con suficiente información para contrastarlos y validarlos. También le interesa que los registros generados sean suficientemente completos y estructurados para poder utilizarlos posteriormente como apoyo en documentación o investigación.|


**Un conflicto entre usuarios: El usuario estándar prioriza la rapidez y simplicidad, esperando identificar una especie casi inmediatamente al apuntar la cámara. En cambio, el usuario avanzado prioriza la calidad, precisión y profundidad del resultado, y puede aceptar un mayor tiempo de procesamiento a cambio de analizar más especies, obtener un nivel de confianza más fiable y acceder a información técnica adicional.**

## Semana 2 - Primer contacto con la dupla

**Huecos:**
> 1:Posible problema con la cantidad de especies y el peso del software.\
> 2:Posibilidad de utilizar la base de datos del software para apoyar a biólogos y documentar la vida silvestre de la zona.

---

## 3. Alcance

### Dentro del alcance

- Presentación de información de la especie identificada: nombre común, nombre científico, región, nivel de riesgo o importancia médica, nivel de confianza y especies visualmente similares presentes en la región.
- Identificación de especies mediante la cámara de un teléfono inteligente.
- Recopilación y almacenamiento de datos de las identificaciones realizadas por Usuarios Avanzados, con el propósito de apoyar la documentación de flora y fauna regional.
- Historial de especies identificadas por el usuario, incluyendo los datos asociados a cada identificación.
- Reconocimiento offline de especies de importancia médica, siempre que el usuario haya descargado previamente la base de datos o modelo correspondiente a su región.

### Explícitamente fuera del alcance

- No guarda la imagén utilizada para la detección (Usuario Estándar)
- No constituye una plataforma científica de validación colaborativa.
- No garantiza una identificación definitiva de la especie.
- No identifica especies fuera de las bases de datos/modelos utilizados para la región seleccionada

**Por qué queda fuera:**

--- **No identifica especies fuera del modelo o base de datos regional instalada:** 
Queda fuera porque ampliar la cobertura requeriría incorporar y entrenar el sistema con una cantidad considerablemente mayor de especies. 

--- **No garantiza una identificación definitiva de la especie:** 
Queda fuera porque el resultado depende de factores como la calidad de la imagen, similitud entre especies y datos disponibles para el modelo.

--- **No constituye una plataforma científica de validación colaborativa:** 
Queda fuera porque requeriría implementar mecanismos adicionales de revisión por expertos, validación de registros y colaboración entre usuarios.


## 4. Tipo de sistema y restricciones

**Tipo de sistema:**

De datos y análisis

**Por qué es de ese tipo:**

Porque a trevés de un modelo de inteligencia artificial entrenado con bases de datos seleccionadas, proporciona una conclusión/estimación a cerca de lo que se le alimenta.

**Atributos de calidad que impone:**

| Atributo | Por qué importa en mi caso | Qué pasa si no se cumple |
|---|---|---|
|Calidad de los datos |El modelo depende de imágenes y datos representativos y correctamente clasificados para aprender las características de cada especie |Datos incorrectos, insuficientes o poco representativos pueden provocar identificaciones erróneas y reducir la confiabilidad del modelo. |
|Precisión |Es necesario que el sistema diferencie correctamente entre especies, especialmente aquellas visualmente similares o de importancia médica. |Una identificación incorrecta puede desinformar al usuario y es especialmente relevante si se confunden especies peligrosas con especies inofensivas. |
|Tiempo de procesamiento |El usuario estándar espera obtener una identificación rápidamente después de apuntar la cámara o capturar una imagen. |Un procesamiento demasiado lento perjudica la experiencia del usuario y reduce la utilidad del reconocimiento en campo. |
|Privacidad |Las imágenes y registros pueden contener información asociada al usuario o a la ubicación donde se realizó una observación. |El almacenamiento o exposición no autorizada de estos datos puede comprometer la privacidad del usuario y la ubicación de determinadas especies. |

**Reglas de negocio que ya identifiqué:**

1. Si el porcentaje de confianza de la identificación es inferior al 90 %, el resultado no deberá presentarse como confiable.
2. Si la calidad de la fotografía no es suficiente para realizar una identificación adecuada, el sistema deberá solicitar al usuario un nuevo intento y proporcionar recomendaciones para mejorar la imagen.
3. Si la especie no se encuentra dentro de la base de datos o del modelo disponible, el sistema no deberá forzar una identificación y deberá indicar que no fue posible reconocerla.

---

## 5. Ciclo de vida elegido

**Modelo elegido: Ágil (Extreme Programming)**

**Por qué le conviene a este proyecto:**

Se utiliza un modelo Ágil con prácticas de Extreme Programming (XP) debido a que los requisitos del proyecto no son completamente estables y pueden evolucionar conforme se entrenen, prueben y ajusten los modelos de IA para el reconocimiento de flora y fauna. El desarrollo dependerá de ciclos constantes de entrenamiento, evaluación, ajuste o fine-tuning e integración de nuevas versiones del modelo.

La retroalimentación de los usuarios será frecuente y tendrá una participación importante en el desarrollo y evolución del sistema, permitiendo detectar problemas relacionados con la experiencia de uso, calidad de las identificaciones y nuevas necesidades.

El proyecto presenta riesgos técnicos y de producto, debido a posibles cambios en los modelos de reconocimiento, bases de datos, herramientas utilizadas y requisitos de hardware. Por ello, resulta conveniente realizar pruebas e integraciones frecuentes en lugar de esperar hasta una versión final.

Asimismo, al tratarse de un equipo de desarrollo pequeño, XP resulta adecuado por favorecer la comunicación directa, el desarrollo incremental y la adaptación rápida a los cambios. Finalmente, se espera realizar entregas frecuentes de versiones funcionales, incorporando progresivamente mejoras en la aplicación y nuevas versiones de los modelos de reconocimiento.

### Alternativas descartadas

**Alternativa 1: Prototipado**

*Por qué la descarté: Es una alternativa adecuada para el proyecto, especialmente para diseñar y validar la interfaz y la experiencia de usuario, por lo que se utilizará como complemento del modelo Ágil (XP). Sin embargo, se descarta como modelo principal porque el proyecto no se limita a validar una interfaz o descubrir requisitos mediante prototipos; también requiere desarrollar, entrenar, evaluar e integrar continuamente un modelo de reconocimiento de especies. Este proceso necesita múltiples iteraciones, pruebas y ajustes antes de obtener versiones suficientemente confiables para su integración. Por ello, Ágil (XP) proporciona un marco más adecuado para gestionar la evolución completa del sistema, mientras que el prototipado se utilizará principalmente para validar la experiencia de usuario.*

**Alternativa 2: Modelo V**

*Por qué la descarté: El Modelo V podría ser una alternativa, ya que establece etapas claras de desarrollo acompañadas de procesos de verificación y validación, lo cual es necesario y conveniente para comprobar la calidad del sistema. Sin embargo, se descarta como modelo principal porque el proyecto no cuenta con requisitos completamente estables y verificables desde el inicio. El desarrollo depende de la retroalimentación frecuente de los usuarios y de los resultados obtenidos durante las pruebas del modelo de reconocimiento, lo que puede provocar cambios en los requisitos y en la experiencia de uso. Esta necesidad de adaptación continua resulta más compatible con un enfoque Ágil (XP).*

---

## Antes de entregar

Reviso que el documento cumpla lo siguiente:

- [x] La descripción del apartado 1 se entiende sin ser del área
- [x] Hay al menos dos tipos de usuario con necesidades distintas
- [x] Identifiqué un conflicto real entre usuarios
- [x] El alcance dice qué queda fuera, no solo qué queda dentro
- [x] Las exclusiones son específicas, no genéricas
- [x] Identifiqué el tipo de sistema y al menos dos atributos de calidad
- [x] Anoté al menos tres reglas de negocio no obvias
- [x] Justifiqué el ciclo de vida contra dos alternativas descartadas
- [ ] El documento está en mi repositorio y se puede leer desde el navegador
- [ ] Borré todas las instrucciones en cursiva de la plantilla
