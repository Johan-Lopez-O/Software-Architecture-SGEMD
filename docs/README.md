# Arquitectura SGEMD - Documentación Viva

> **Índice General y Visión Global de Vistas**
> Este directorio contiene la documentación técnica y arquitectónica del Sistema de Gestión de Emprendimiento Minuto de Dios (SGEMD) reconstruido desde cero.

## Sincronía Topológica: Decisiones y Diseño

El diseño del sistema está fuertemente acoplado a las decisiones críticas del negocio para garantizar trazabilidad. A continuación, se enlazan las decisiones (ADRs) con sus representaciones topológicas (diagramas).

| Necesidad de Negocio | Decisión (ADR) | Diseño (PlantUML) |
| :--- | :--- | :--- |
| **Separación de roles y control global** | [ADR-0001: Monolito Modular](../adr/0001-patron-arquitectonico.md)<br>[ADR-0007: Node.js + React](../adr/0007-stack-tecnologico-principal.md) | [Diagrama C4 de Contexto](../diagrams/c4-contexto.puml) |
| **Trazabilidad estricta y control manual de agendas** | [ADR-0002: Motor PostgreSQL 17](../adr/0002-motor-de-persistencia.md)<br>[ADR-0004: Expediente Central](../adr/0004-expediente-central-emprendimiento.md)<br>[ADR-0005: Agendamiento Manual](../adr/0005-agendamiento-manual-cerrado.md) | [Diagrama de Secuencia de Agendamiento](../diagrams/secuencia-proceso-clave.puml) |
| **Seguridad de datos y validación de usuarios** | [ADR-0003: JWT + OTP 8 dígitos](../adr/0003-estrategia-seguridad-acceso.md)<br>[ADR-0006: Almacenamiento Local](../adr/0006-almacenamiento-local-evidencias.md) | (Reflejado en el flujo de validación del backend) |

## Sustentación Técnica

La presente arquitectura y su documentación viva han sido estructuradas para mitigar de raíz la deuda técnica heredada del proyecto SGEMD anterior:

1. **Eliminación de Datos Mock y Consultas Incompatibles:** Al consolidar el Expediente Central apoyado en transacciones ACID con PostgreSQL (ADR-0002), se asegura que el cálculo de métricas en los Dashboards se genere exclusivamente a partir de registros reales. Se descarta cualquier estructura vestigial que usaba información simulada o tablas huérfanas.
2. **Unificación del Modelo de Dominio:** El diagrama de secuencia expone cómo la trazabilidad (asesorías, adjuntos, seguimiento) queda anclada obligatoriamente a la entidad *Emprendimiento* y no al docente. Esto resuelve las múltiples implementaciones duplicadas de asignaciones del proyecto anterior.
3. **Onboarding de Asistentes de IA y Nuevos Desarrolladores:** Adoptar *Diagram-as-Code* (PlantUML) y *Architectural Decision Records* (ADRs) en texto plano (Markdown) permite que herramientas de inteligencia artificial y nuevos ingenieros lean el repositorio y entiendan inmediatamente el diseño sin requerir documentación externa desactualizada.

## Estructura

```text
.
├── adr/
│   ├── 0001-patron-arquitectonico.md
│   ├── 0002-motor-de-persistencia.md
│   ├── 0003-estrategia-seguridad-acceso.md
│   ├── 0004-expediente-central-emprendimiento.md
│   ├── 0005-agendamiento-manual-cerrado.md
│   ├── 0006-almacenamiento-local-evidencias.md
│   └── 0007-stack-tecnologico-principal.md
├── diagrams/
    ├── c4-contexto.puml
    └── secuencia-proceso-clave.puml
└── docs/
    └── README.md
```

## Visualizar los diagramas

Instala en VS Code las extensiones **PlantUML** y **Pumlify**. Pumlify se utiliza
para formatear el código; PlantUML se utiliza para abrir la vista previa.

1. Abre cualquiera de los archivos `.puml` dentro de `diagrams/`.
2. Usa `Shift + Alt + F` para formatear con Pumlify.
3. Usa `Alt + D` o el comando `PlantUML: Preview Current Diagram` para ver el diagrama.

Para los diagramas C4, la extensión PlantUML debe poder resolver la inclusión
`C4/C4_Context`, ya sea mediante el servidor PlantUML o mediante una instalación
local configurada en VS Code.