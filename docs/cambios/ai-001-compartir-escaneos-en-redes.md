# AI-001: Análisis de impacto de SC-001 — Compartir escaneos en redes sociales

> Ingeniería de Software I · SIS3407  
> Sistema: BIOMA — Sistema de detección de flora y fauna local para senderistas  
> Tipo de mantenimiento: **perfectivo**  
> Estado del análisis: **propuesta, pendiente de aprobación y validación técnica**

---

## Solicitud que se analiza

**Referencia:** `doc/cambios/sc-001-compartir-escaneos-en-redes.md` (SC-001).  
**Solicitante:** Victor Flores, dupla de revisión.  
**Fecha de solicitud:** 12 de noviembre de 2026.  
**Prioridad sugerida:** baja.

La solicitud pide incorporar en la pantalla de resultado de un escaneo un botón para compartir en redes sociales la fotografía capturada y el nombre de la especie identificada, con posibilidad de elegir al menos una red social, por ejemplo Instagram. El usuario no debería tener que realizar una captura de pantalla manual. Compartir no debe borrar ni modificar el escaneo guardado en BIOMA.

## Traducción a términos del sistema

En BIOMA, la solicitud afecta al flujo **CU-01: Identificar una especie a partir de una imagen válida**, posterior a **CU-06: Capturar imagen de una especie**, y a la pantalla donde se presenta el resultado de `Identificacion` y la ficha de `Especie`.

Se propone incorporar un nuevo caso de uso, **CU-11: Compartir resultado de identificación**, y un requisito funcional, **RF-016: Compartir resultado de identificación en redes sociales**. Estas claves son **propuestas** y deben comprobarse contra la numeración vigente antes de incorporarlas.

El resultado compartible reuniría una referencia **temporal** a la imagen capturada, el `nombreComun` (y opcionalmente `nombreCientifico`) de `Especie` y el estado de `Identificacion`. La clase `ResultadoInferencia` ya proporciona la confianza y el origen de la inferencia, por lo que no necesita almacenar información de la red social.

Como decisión de diseño propuesta, se introduce un servicio de aplicación `CompartidorResultado`, con la operación `prepararContenido(identificacion, imagenTemporal)` y `compartir(contenido)`, y un objeto temporal `ContenidoCompartible`. No se agrega la fotografía al `Historial` ni se presupone que `Identificacion` deba conservarla permanentemente. El servicio delegaría la elección de la aplicación destino al mecanismo de compartir del sistema operativo. **La compatibilidad con historias de Instagram requiere verificación en los dispositivos y versiones objetivo; no se da por garantizada.**

La imagen solo estará disponible para compartir durante la sesión de resultado, salvo que se apruebe por separado un mecanismo de conservación. Para una identificación de baja confianza, el contenido deberá indicar explícitamente que es **posible** y no confirmada, si se decide permitir compartirla. Esta decisión debe validarse con el solicitante.

## Impacto directo

| Artefacto | Unidad | Qué hay que cambiar |
|---|---:|---|
| Requisito funcional RF-016 (propuesto) | 2 | Especificar el botón de compartir, datos incluidos, selección de destino, manejo de cancelación y prohibición de alterar registros existentes. Relacionarlo con RF-001, RF-002, RF-003 y RF-013. |
| Caso de uso CU-11 (propuesto) | 2 | Documentar actor, precondición (resultado e imagen temporal disponibles), flujo de preparación y envío al menú nativo, cancelación, ausencia de aplicaciones compatibles y postcondición sin cambios en el historial. |
| Diagrama de clases | 4 | Agregar `CompartidorResultado` y `ContenidoCompartible`, sus operaciones y asociaciones con `Identificacion` y `Especie`; representar la imagen como referencia temporal, no como dato persistente. |
| Diagrama de secuencia | 4 | Agregar la interacción Usuario → pantalla de resultado → CompartidorResultado → mecanismo de compartir del sistema operativo → aplicación elegida; incluir alternativas de cancelación, fallo y ausencia de destino. |

## Impacto indirecto

| Artefacto | Unidad | Por qué se ve afectado |
|---|---:|---|
| Registro de decisión arquitectónica (ADR) | 3 | **Impacto: sí.** Debe registrarse la decisión de usar el mecanismo nativo de compartir frente a una integración específica con Instagram, así como la política de imagen temporal. No se presupone un identificador ADR existente: asignarlo según el repositorio. |
| Diagrama de contenedores C4 | 3 | **Impacto limitado.** Si el C4 muestra dependencias externas del cliente móvil, debe indicarse la interacción con el servicio de compartir del sistema operativo. No se requiere nuevo contenedor backend ni servicio propio de redes sociales. Si el diagrama se limita a contenedores desplegables, documentar expresamente **sin cambio estructural**. |
| Máquina de estados | 4 | **Impacto: sí, si se modela el flujo de identificación.** Añadir estados o transiciones de `resultado mostrado → preparando contenido → selector externo → regreso/cancelación/error`, sin modificar el estado de confirmación de la identificación ni el historial. Si no existe máquina de estados en el repositorio, registrar la necesidad de crearla solo si la actividad lo exige. |

**Otros efectos indirectos que deben revisarse:**

- **Privacidad y almacenamiento (RNF-SEG-001):** el alcance actual indica que BIOMA no almacena la imagen del usuario estándar. Compartir requiere conservarla temporalmente hasta construir el contenido y transferirlo a otra aplicación, con consentimiento explícito del usuario. Evitar incorporar ubicación exacta o metadatos EXIF innecesarios.
- **RF-004, RF-014 y RNF-ESC-001:** compartir no debe confirmar una identificación, crear un registro adicional, eliminar identificaciones ni alterar el límite de 50 registros para el usuario estándar.
- **RF-010 y RF-011:** si se comparte una candidata de baja confianza, debe mostrarse como posible identificación para evitar presentar como certeza un resultado incierto. Para especies de importancia médica, debe respetarse el umbral del 99 % y las advertencias correspondientes.
- **Prototipo e interfaz:** incorporar botón, vista previa de contenido compartible, indicaciones de carga/error y comportamiento al regresar desde otra aplicación.
- **Pruebas de integración móvil:** verificar permisos, disponibilidad temporal de la imagen, formato de archivo, recepción del contenido en destinos reales y comportamiento al cancelar.

## Lo que queda sin tocar

- Los umbrales de confirmación de **90 % para especies generales** y **99 % para especies de importancia médica**, así como los requisitos de precisión del modelo.
- Los modelos de inferencia y el procesamiento de reconocimiento de flora y fauna.
- La clasificación y ficha de `Especie`, salvo su uso para componer el contenido visual.
- El límite de 50 identificaciones confirmadas del historial estándar y su política de eliminación del registro más antiguo.
- La funcionalidad de observaciones avanzadas (`Observacion`).
- Los paquetes regionales, la descarga de recursos y la inferencia offline; compartir podría estar disponible sin conexión para generar contenido local, pero la publicación final depende de la aplicación destino y de su conectividad.
- El backend y la base de datos, **si se adopta la alternativa de imagen temporal y compartir nativo**.

## Riesgos

| Riesgo | Probabilidad estimada | Consecuencia y mitigación |
|---|---|---|
| La foto deja de estar disponible cuando el usuario pulsa compartir | Media | Falla la generación del contenido. Mantener referencia temporal durante la pantalla de resultado y liberarla al terminar. |
| El destino elegido no admite el formato o la opción de historia | Media | El criterio de aceptación podría no cumplirse en ese destino. Probar aplicaciones y versiones concretas; ofrecer el selector nativo y comunicar limitaciones. |
| Exposición accidental de ubicación u otros metadatos de la fotografía | Media | Riesgo de privacidad. Generar una imagen derivada sin EXIF innecesario y requerir acción explícita de compartir. |
| Una identificación no confirmada se publica como si fuera definitiva | Media | Desinformación sobre especies, especialmente las de importancia médica. Bloquear el compartir de no confirmadas o rotular claramente la incertidumbre; validar la política. |
| Compartir modifica el historial por acoplamiento incorrecto | Baja | Incumplimiento del criterio de aceptación. Mantener el servicio independiente de `Historial` y probar invariantes antes y después. |
| No realizar el cambio | Alta (oportunidad perdida) | Los usuarios seguirán recurriendo a capturas manuales; no bloquea funciones esenciales. |

Las probabilidades son **juicios preliminares**, no resultados de pruebas ni estadísticas observadas.

## Alternativas consideradas

1. **Opción A — Compartir nativo con imagen temporal (recomendada).** La aplicación genera una tarjeta visual a partir de la foto de la sesión y el nombre de la especie, y abre el selector de compartir del sistema operativo. No requiere backend ni persistencia nueva. Su costo principal está en interfaz, preparación del archivo, compatibilidad móvil y pruebas. Queda pendiente confirmar si la aplicación destino permite publicarlo como historia.
2. **Opción B — Integración específica con Instagram y almacenamiento persistente.** Se implementa un flujo especializado para el destino y se conserva la fotografía para compartirla posteriormente. Ofrece mayor control sobre una experiencia concreta, pero exige revisar políticas, compatibilidad, permisos, privacidad, persistencia y mantenimiento ante cambios de terceros. Es más costosa y modifica el alcance de almacenamiento de BIOMA.

Se elige la **opción A**, condicionada a validar en los dispositivos objetivo el criterio de seleccionar al menos una red social compatible. No se promete una publicación automática ni acceso a funciones no expuestas por la aplicación destino.

## Estimación de esfuerzo

**Estimación para una primera implementación de la opción A en una plataforma móvil**, sin backend nuevo ni persistencia permanente:

| Concepto | Esfuerzo |
|---|---:|
| Cambios de diseño y documentación | 5 h |
| Implementación (botón, tarjeta, archivo temporal, selector nativo y manejo de errores) | 10 h |
| Pruebas (flujo normal, cancelación, privacidad, historial y destino compatible) | 5 h |
| **Total** | **20 h** |

**De dónde sale este número.** Es una estimación de ingeniería preliminar, desglosada por tareas pequeñas, no una medición histórica de BIOMA. Supone que ya existen la pantalla de resultado, el acceso temporal a la fotografía y los datos de especie; que el proyecto puede usar la función de compartir del sistema operativo; y que se implementa en **una sola plataforma**. No incluye integración oficial con una API social, autenticación en redes, publicación automática, almacenamiento de fotos, backend ni una segunda plataforma móvil. Si se requiere compatibilidad verificada con historias de Instagram o desarrollo en Android **e** iOS, habrá que ampliar la estimación después de una prueba técnica.

Como referencia de documentación, la plantilla asigna **12 unidades de impacto directo** y hasta **10 unidades de revisión indirecta**. Estas unidades sirven para comparar artefactos afectados; **no se suman como horas**.

## Recomendación

**Aceptar el cambio con alcance controlado y programarlo después de los requisitos imprescindibles.** La solicitud aporta valor a la experiencia y a la difusión orgánica de BIOMA, pero tiene prioridad baja y no resuelve una falla del reconocimiento. La implementación nativa y temporal permite satisfacer el objetivo principal sin alterar el historial ni introducir almacenamiento permanente de imágenes.

Antes de iniciar, confirmar con la dupla dos puntos: **(1)** si se exige específicamente publicar en historias de Instagram o basta con ofrecer al menos una red social desde el selector, y **(2)** si se permite compartir resultados de baja confianza, identificándolos explícitamente como posibles. Si el requisito exige integración directa con historias o conservar fotografías para compartir después, volver a estimar y aprobar ese alcance adicional.

---

*Este análisis describe impacto y esfuerzo previstos. No afirma que el cambio haya sido implementado o probado.*
