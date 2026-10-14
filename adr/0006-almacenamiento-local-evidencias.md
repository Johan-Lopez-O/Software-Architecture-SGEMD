# ADR-0006: Almacenamiento Local de Archivos Adjuntos con Borrado Físico

**Estado:** ACEPTADO

## Contexto
El sistema requiere el soporte para cargar y visualizar actas de confidencialidad y evidencias de avances en PDF/Excel (hasta 500 MB por archivo). Para el MVP, la integración inmediata con servicios de almacenamiento en la nube (como AWS S3) representa un sobrecosto y complejidad no justificada en esta fase inicial.

## Decisión
Se utilizará el sistema de archivos local del servidor mediante volúmenes de Docker para persistir los adjuntos. Se implementará una tabla centralizada `Adjuntos` en PostgreSQL que guardará la metadata y la ruta. Si un registro asociado (tarea o seguimiento) se elimina, el backend ejecutará un borrado en cascada que eliminará físicamente el archivo del servidor.

## Consecuencias
* **Positivas:**
  * Cumple con la restricción de presupuesto y simplifica la infraestructura del MVP.
  * El borrado físico automático previene la saturación del disco duro del servidor por archivos huérfanos.
* **Negativas:**
  * Dificulta la escalabilidad horizontal: si se añaden más nodos del backend en el futuro, se requerirá migrar forzosamente a un sistema de almacenamiento compartido en red o nube.