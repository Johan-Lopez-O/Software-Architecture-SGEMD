# ADR-0005: Gobernanza Administrativa de Agenda sin Integraciones Externas

**Estado:** ACEPTADO

## Contexto
Durante el levantamiento de requisitos se propuso integrar los calendarios de los docentes (Google Calendar/Outlook) para automatizar los espacios. Sin embargo, la coordinación administrativa rechazó explícitamente esta automatización debido al riesgo de agendamiento fantasma por falta de actualización de disponibilidad de los docentes.

## Decisión
Se decide implementar un sistema de agendamiento cerrado y completamente manual. La plataforma web será la única fuente de verdad. El estudiante solicitará el espacio y este quedará en estado "Pendiente". Solo la Coordinadora, validando su panel, podrá cruzar los horarios y confirmar la asesoría, disparando una notificación en tiempo real.

## Consecuencias
* **Positivas:**
  * Otorga control total a la administración, alineándose exactamente con sus reglas de negocio operativas.
  * Elimina dependencias tecnológicas y costos de mantenimiento asociados a APIs de terceros (Google Workspace/Microsoft Graph).
* **Negativas:**
  * Mantiene una carga operativa manual sobre el Administrador, al obligarlo a confirmar cada cita.