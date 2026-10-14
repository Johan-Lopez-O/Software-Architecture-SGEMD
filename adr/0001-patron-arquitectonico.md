# ADR-0001: Selección de Monolito Modular sobre Microservicios para el MVP

**Estado:** ACEPTADO

## Contexto
El proyecto SGEMD está siendo reconstruido desde cero utilizando Node.js y React. El sistema debe gestionar tres roles (Administrador, Docente, Estudiante) y orquestar flujos de registro, diagnósticos automáticos y agendamiento. Aunque las responsabilidades están bien delimitadas, la carga transaccional esperada para el MVP en el Centro Progresa es manejable y el equipo de desarrollo requiere iteraciones rápidas sin la complejidad de gestionar infraestructura distribuida.

## Decisión
Se decide implementar una arquitectura de Monolito Modular. El backend operará como un único proceso de despliegue en Node.js, pero el código fuente estará estrictamente segmentado en módulos de dominio independientes (rutas, controladores, servicios) como Auth, Usuarios, Emprendimientos, Seguimiento y Asesorías.

## Consecuencias
* **Positivas:**
  * Minimiza la complejidad operativa y los costos de infraestructura mediante un despliegue simple con Docker Compose.
  * Facilita el mantenimiento de transacciones ACID en la base de datos al no requerir transacciones distribuidas (Sagas) para los cruces de agenda.
  * Permite una futura migración a microservicios si un módulo específico (ej. el motor de diagnósticos) demanda escalabilidad independiente.
* **Negativas:**
  * Un fallo fatal (panic) en un módulo puede comprometer la disponibilidad de toda la API.
  * La escalabilidad requerirá replicar todo el monolito en lugar de solo los cuellos de botella.