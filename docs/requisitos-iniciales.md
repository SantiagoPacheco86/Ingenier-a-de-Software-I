# Requisitos iniciales del sistema

**Sistema:** BIOMA — Sistema de detección de flora y fauna local para senderistas  
**Materia:** Ingeniería de Software I  
**CNR:** 92623  
**Instructor:** Lizeth Murrieta Zavala  
**Estudiante:** Santiago Pacheco Carrillo  

---

## 1. Propósito

Este documento contiene los requisitos iniciales definidos para BIOMA antes de la entrevista de elicitación y de las modificaciones posteriores realizadas en la especificación de requisitos.

---

## 2. Requisitos funcionales iniciales

### RF-001 · Identificación de especie

**Requisito original:**  
El sistema deberá procesar una imagen capturada mediante la cámara del dispositivo móvil y proporcionar la identificación de la especie de flora o fauna detectada.

**Origen inicial:** Visión del producto.

**Justificación del origen:** La identificación de especies de flora y fauna mediante la cámara constituye la funcionalidad central planteada desde la Visión de BIOMA.

---

### RF-002 · Información de la especie

**Requisito original:**  
El sistema deberá mostrar el nombre común, nombre científico, región y nivel de riesgo o importancia médica de la especie identificada.

**Origen inicial:** Visión del producto.

**Justificación del origen:** La Visión contemplaba la presentación de información asociada a la especie identificada como parte del alcance del sistema.

---

### RF-003 · Nivel de confianza

**Requisito original:**  
El sistema deberá mostrar el nivel de confianza de cada identificación.

**Origen inicial:** Visión del producto.

**Justificación del origen:** El nivel de confianza formaba parte de la información prevista para acompañar el resultado de identificación.

---

### RF-004 · Historial de identificaciones

**Requisito original:**  
El sistema deberá almacenar un historial de las especies identificadas.

**Origen inicial:** Visión del producto.

**Justificación del origen:** La conservación de un historial de especies identificadas ya se encontraba contemplada dentro del alcance inicial de BIOMA.

---

### RF-005 · Especie no reconocida

**Requisito original:**  
El sistema deberá indicar que no fue posible realizar la identificación cuando la especie no se encuentre dentro del modelo disponible.

**Origen inicial:** Visión del producto / regla de negocio inicial.

**Justificación del origen:** La Visión establecía que el sistema no debía forzar una identificación cuando la especie no pudiera reconocerse o no estuviera disponible dentro del modelo.

---

## 3. Requisitos no funcionales iniciales

### RNF-SEG-001 · Protección de información sensible

**Requisito original:**  
El sistema deberá almacenar cifradas las credenciales y demás información sensible de los usuarios.

**Atributo:** Seguridad

**Origen inicial:** Supuesto propio derivado del tipo de sistema.

**Justificación del origen:** El entregable inicial estableció la necesidad de proteger credenciales e información sensible, pero el documento de requisitos inicial no registra que este requisito haya sido confirmado por un usuario o cliente.

---

### RNF-REN-001 · Tiempo de identificación

**Requisito original:**  
El sistema deberá determinar el resultado de una identificación en un tiempo máximo de 15 segundos.

**Atributo:** Rendimiento

**Origen inicial:** Supuesto propio / criterio definido durante la especificación inicial.

**Justificación del origen:** El límite cuantitativo de 15 segundos aparece en el documento inicial, pero no se documenta allí una fuente externa o validación de usuario para ese valor.

---

### RNF-ESC-001 · Capacidad del historial

**Requisito original:**  
El historial de un usuario estándar deberá tener una capacidad máxima de 50 identificaciones.

**Atributo:** Escalabilidad / Capacidad

**Origen inicial:** Supuesto propio / criterio definido durante la especificación inicial.

**Justificación del origen:** El límite de 50 identificaciones fue establecido en los requisitos iniciales, pero el documento original no indica que el valor procediera de una entrevista o de una necesidad confirmada.

---

## 4. Resumen de origen

| ID | Requisito | Tipo | Origen inicial |
| --- | --- | --- | --- |
| RF-001 | Identificación de especie | Funcional | Visión del producto |
| RF-002 | Información de la especie | Funcional | Visión del producto |
| RF-003 | Nivel de confianza | Funcional | Visión del producto |
| RF-004 | Historial de identificaciones | Funcional | Visión del producto |
| RF-005 | Especie no reconocida | Funcional | Visión del producto / regla de negocio inicial |
| RNF-SEG-001 | Protección de información sensible | No funcional — Seguridad | Supuesto propio derivado del tipo de sistema |
| RNF-REN-001 | Tiempo de identificación | No funcional — Rendimiento | Supuesto propio / criterio de especificación inicial |
| RNF-ESC-001 | Capacidad del historial | No funcional — Escalabilidad / Capacidad | Supuesto propio / criterio de especificación inicial |

---

## 5. Nota de trazabilidad

Este documento representa el **estado inicial** de los requisitos y no sustituye la especificación vigente de BIOMA.

Los requisitos aquí registrados pueden haber sido posteriormente confirmados, modificados, ampliados o complementados a partir de la entrevista de elicitación, la revisión de la Visión del producto y el proceso formal de especificación. Sus identificadores se conservan para mantener la trazabilidad entre la definición inicial y las versiones posteriores.
