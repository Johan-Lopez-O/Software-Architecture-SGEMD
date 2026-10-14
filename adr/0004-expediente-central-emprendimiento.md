# ADR-0004: Trazabilidad Anclada Exclusivamente a la Entidad Emprendimiento

**Estado:** ACEPTADO (Interconectado con ADR-0002)

## Contexto
Un problema crítico identificado por la coordinación era la pérdida de la bitácora histórica cuando un estudiante rotaba de asesor. En el modelo anterior, los seguimientos y tareas dependían estructuralmente del usuario (docente), rompiendo la continuidad del acompañamiento.

## Decisión
Se decide aplicar el patrón de "Expediente Central". En el diseño de la base de datos (PostgreSQL), todas las entidades transaccionales de seguimiento (Asesorías, Diagnósticos, Tareas y Seguimientos) tendrán una restricción de clave foránea estricta y obligatoria hacia la entidad `Emprendimiento`, y no hacia el docente en curso.

## Consecuencias
* **Positivas:**
  * Garantiza la retención del contexto histórico: cualquier docente nuevo asignado visualizará instantáneamente todo el proceso acumulado.
  * Facilita la generación de reportes directivos centralizados por idea de negocio.
* **Negativas:**
  * Requiere lógica adicional en el backend para validar que el docente que intenta escribir en el expediente tenga una relación activa en la tabla pivote de `Asignaciones` con dicho emprendimiento.