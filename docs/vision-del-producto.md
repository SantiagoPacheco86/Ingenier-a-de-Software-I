# Visión del producto

> **Plantilla del curso · Ingeniería de Software I · SIS3407**
> Este documento es el primer entregable del semestre y la base de todo lo que viene después.
> Se entrega completo en la **semana 4** y se presenta ante el grupo.
>
> **Cómo usarla:** copia este archivo a tu repositorio como `docs/vision-del-producto.md`, borra las instrucciones en gris de cada apartado y escribe tu contenido en su lugar. Conserva los títulos.

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

*Instrucción: lo que escribes en "fuera del alcance" es lo que después evita que el proyecto crezca sin control. Sé específico: "reportes" no dice nada, "reportes de ventas mensuales exportables a PDF" sí.*

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

*Instrucción: para al menos una de las exclusiones, explica la razón. Puede ser tiempo, complejidad, o que no aporta al problema central.*

--- **No identifica especies fuera del modelo o base de datos regional instalada:** Queda fuera porque ampliar la cobertura requeriría incorporar y entrenar el sistema con una cantidad considerablemente mayor de especies. 
--- **No garantiza una identificación definitiva de la especie:** Queda fuera porque el resultado depende de factores como la calidad de la imagen, similitud entre especies y datos disponibles para el modelo.
--- **No constituye una plataforma científica de validación colaborativa:** Queda fuera porque requeriría implementar mecanismos adicionales de revisión por expertos, validación de registros y colaboración entre usuarios.

## 4. Tipo de sistema y restricciones

*Instrucción: identifica de qué tipo es tu sistema y qué te obliga a garantizar ese tipo. Un sistema de información y un sistema crítico no se diseñan igual.*

**Tipo de sistema:**

*(De información · Embebido · Crítico · Web y SaaS · De datos y análisis)*

**Por qué es de ese tipo:**

**Atributos de calidad que impone:**

| Atributo | Por qué importa en mi caso | Qué pasa si no se cumple |
|---|---|---|
| | | |
| | | |

**Reglas de negocio que ya identifiqué:**

*Instrucción: reglas que no son obvias desde fuera y que alguien que conoce el dominio tendría que explicarte. Si no encuentras ninguna, tu caso puede ser demasiado simple.*

1.
2.
3.

---

## 5. Ciclo de vida elegido

*Instrucción: este apartado se trabaja en la semana 3, después de ver los modelos de desarrollo. La justificación pesa más que la elección: no hay un modelo correcto, hay uno defendible para tu caso.*

**Modelo elegido:**

**Por qué le conviene a este proyecto:**

*Instrucción: argumenta con las características reales de tu caso. Estabilidad de los requisitos, disponibilidad del cliente, nivel de riesgo, tamaño del equipo, frecuencia de entregas esperada.*

### Alternativas descartadas

**Alternativa 1:**

*Por qué la descarté:*

**Alternativa 2:**

*Por qué la descarté:*

---

## Antes de entregar

Reviso que el documento cumpla lo siguiente:

- [ ] La descripción del apartado 1 se entiende sin ser del área
- [ ] Hay al menos dos tipos de usuario con necesidades distintas
- [ ] Identifiqué un conflicto real entre usuarios
- [ ] El alcance dice qué queda fuera, no solo qué queda dentro
- [ ] Las exclusiones son específicas, no genéricas
- [ ] Identifiqué el tipo de sistema y al menos dos atributos de calidad
- [ ] Anoté al menos tres reglas de negocio no obvias
- [ ] Justifiqué el ciclo de vida contra dos alternativas descartadas
- [ ] El documento está en mi repositorio y se puede leer desde el navegador
- [ ] Borré todas las instrucciones en cursiva de la plantilla
