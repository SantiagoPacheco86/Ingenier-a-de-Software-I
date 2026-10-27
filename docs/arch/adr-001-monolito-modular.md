# ADR-001: Adoptar un monolito modular en lugar de microservicios para BIOMA

## Estado

Aceptada — 27 de octubre de 2026.

## Contexto

BIOMA es un sistema de identificación de especies mediante inteligencia artificial, ofrecido principalmente como SaaS a través de una aplicación móvil. El procesamiento principal de identificación se realizará en infraestructura en la nube, con capacidad offline limitada para especies de importancia médica.

El proyecto es desarrollado por una sola persona y actualmente se han definido cuatro módulos de negocio: Especies y regiones, Identificación y reconocimiento, Gestión de usuarios e Historial y observaciones.

Se evaluaron las arquitecturas de monolito, monolito modular y microservicios. Aunque los módulos tienen responsabilidades identificables, sus fronteras todavía pueden modificarse durante el desarrollo.

## Decisión

Se adopta una arquitectura de monolito modular para el backend de BIOMA, manteniendo los cuatro módulos organizados mediante interfaces y responsabilidades independientes, pero conservando un despliegue unificado de la lógica de negocio.

Los módulos deberán comunicarse mediante interfaces definidas, evitando acceder directamente a las estructuras internas de otros módulos.

Esta decisión es compatible con el modelo SaaS y permite utilizar un servicio especializado de inferencia de IA sin convertir todos los módulos de negocio en microservicios.

## Consecuencias

**Positivas:**

- Menor complejidad operativa para un proyecto desarrollado individualmente.
- Despliegue y mantenimiento centralizados del backend.
- Separación lógica de responsabilidades que facilita pruebas y modificaciones.
- Posibilidad de separar módulos en servicios independientes si el crecimiento del sistema lo requiere.

**Negativas y riesgos:**

- Los módulos de negocio no podrán desplegarse ni escalarse de manera completamente independiente.
- Un problema en el backend compartido podría afectar varias funcionalidades.
- Se requiere disciplina para evitar dependencias directas que rompan las fronteras entre módulos.

**Condición para reconsiderar la decisión:**

El primer candidato a separarse será Identificación y reconocimiento. Se reconsiderará su despliegue independiente si, durante periodos de alta demanda, el backend supera el 80 % de utilización de recursos computacionales y se producen incumplimientos de los tiempos de respuesta establecidos en los requisitos no funcionales.

Este umbral se propone como criterio inicial de evaluación y deberá validarse mediante pruebas de rendimiento.
