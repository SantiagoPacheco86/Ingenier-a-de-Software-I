# ADR-003: Compartir resultados con el selector nativo de Android y una imagen temporal

## Estado

**Propuesta** — 17 de noviembre de 2026. Depende de que se apruebe [SC-001](../cambios/sc-001-compartir-escaneos-en-redes.md). Origen: [AI-001](../cambios/ai-001-compartir-escaneos-en-redes.md).

## Contexto

SC-001 pide compartir en redes sociales la fotografía de un escaneo junto con el nombre de la especie, sin captura de pantalla manual y sin modificar el escaneo guardado. La especificación vigente establece que **BIOMA no almacena la imagen del usuario estándar** y que solo las identificaciones confirmadas entran al historial (RF-004).

Alternativas, según AI-001:

- **A.** Selector nativo de Android con un archivo temporal.
- **B.** Integración específica con Instagram y almacenamiento persistente de la foto.

## Decisión

Si SC-001 se aprueba, la aplicación genera una tarjeta con la foto de la sesión y el nombre de la especie. La guarda como **archivo temporal en la caché de la app, sin metadatos EXIF**, la expone con `FileProvider` y abre el selector nativo (`Intent.ACTION_SEND`). El archivo se elimina al salir de la pantalla de resultado. No se agregan contenedores al backend ni se persiste la foto.

## Consecuencias

**Positivas:**

- No cambia la política de no almacenar la imagen ni el backend.
- Cualquier aplicación instalada que acepte imágenes puede servir de destino.
- Esfuerzo acotado: unas 20 h en una plataforma, según AI-001.

**Negativas y riesgos:**

- **No se garantiza publicar como historia de Instagram.** Depende de lo que exponga la aplicación destino.
- No se puede compartir **después**: cuando se cierra la pantalla de resultado, la foto ya no existe.
- Hay que definir si se permite compartir resultados **no confirmados**. De permitirse, deben rotularse como «posible identificación» (RF-011).
