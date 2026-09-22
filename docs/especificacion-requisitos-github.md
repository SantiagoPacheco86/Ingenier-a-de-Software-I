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

  -----------------------------------------------------------------------
  Usuario                 Qué hace hoy sin el     Qué espera del sistema
                          sistema                 
  ----------------------- ----------------------- -----------------------
  **Usuario estándar ---  Observa el organismo,   Facilidad de uso y
  excursionista, turista  registra o recuerda sus acceso rápido al
  o persona interesada en características, las    reconocimiento mediante
  la naturaleza**         compara con referencias la cámara, con una
                          disponibles, descarta   experiencia similar a
                          posibles especies hasta Shazam: apuntar y
                          obtener una             obtener una
                          identificación probable identificación sin
                          y, cuando es necesario, requerir conocimientos
                          busca validación de una especializados. Espera
                          persona con mayor       una respuesta rápida
                          conocimiento.           acompañada de
                                                  fotografías,
                                                  características
                                                  visuales y datos que le
                                                  permitan corroborar que
                                                  la especie identificada
                                                  corresponde con lo
                                                  observado.

  **Usuario avanzado ---  Realiza observaciones y Acceso a información
  estudiantes,            compara las             detallada y técnica de
  científicos,            características del     la especie
  investigadores o        organismo con           identificada, como
  entusiastas con         referencias y           nombre científico,
  conocimientos de flora  conocimiento            taxonomía, nivel de
  y fauna**               especializado para      confianza,
                          determinar una          características
                          identificación.         distintivas y especies
                          Posteriormente puede    similares. Espera poder
                          registrar y organizar   acceder preliminarmente
                          manualmente sus         a bases de datos y
                          observaciones para      modelos en fase beta
                          utilizarlas en          con mayor cobertura
                          documentación,          regional, además de
                          investigación o trabajo registrar, organizar y
                          de campo.               documentar
                                                  observaciones que
                                                  puedan utilizarse como
                                                  apoyo para estudios
                                                  biológicos, monitoreo
                                                  de especies o trabajo
                                                  de campo.
  -----------------------------------------------------------------------

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

------------------------------------------------------------------------

## 3. Requisitos funcionales

### 3.1 Resumen

  ID       Nombre   Prioridad   Origen
  -------- -------- ----------- --------
  RF-001                        
  RF-002                        
  RF-003                        

### 3.2 Fichas

------------------------------------------------------------------------

## 4. Requisitos no funcionales

### 4.1 Resumen

  ID            Atributo      Nombre   Prioridad   Origen
  ------------- ------------- -------- ----------- --------
  RNF-REN-001   Rendimiento                        
  RNF-SEG-001   Seguridad                          
  RNF-USA-001   Usabilidad                         

### 4.2 Fichas

------------------------------------------------------------------------

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
