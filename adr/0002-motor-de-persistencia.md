# ADR-0002: Uso de PostgreSQL 17 como Motor Relacional Primario

**Estado:** ACEPTADO (Interconectado con ADR-0001)

## Contexto
El proyecto anterior presentaba esquemas desconectados, inconsistencias (ej. seguimientos huérfanos) y consultas SQL incompatibles. SGEMD requiere garantizar que ningún agendamiento se solape y que el historial de los proyectos mantenga una integridad referencial absoluta. Además, el formulario de caracterización produce respuestas dinámicas que deben ser tabuladas para el diagnóstico.

## Decisión
Se adopta PostgreSQL 17 como el único motor de base de datos relacional para el MVP, gestionado a través de un pool de conexiones nativo en Node.js (pg). Se integrará el uso de campos JSONB para almacenar las respuestas variables de la caracterización, combinando el rigor relacional con la flexibilidad documental.

## Consecuencias
* **Positivas:**
  * Cumple el requisito de aislamiento de transacciones (ACID) obligatorio para el módulo de agendamiento manual y prevención de duplicidad.
  * El soporte JSONB permite almacenar el formulario de valoración sin normalizar en exceso, facilitando el cálculo automático de métricas.
  * Soporta eficientemente las extracciones masivas de datos (Data Dumps en CSV/Excel) solicitadas por la administración como plan de contingencia.
* **Negativas:**
  * Exige un diseño de modelo físico extremadamente riguroso desde el día cero para evitar la deuda técnica del proyecto anterior.