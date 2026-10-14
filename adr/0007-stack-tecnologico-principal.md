# ADR-0007: Selección de React y Node.js (Express) como Stack Tecnológico Principal

**Estado:** ACEPTADO (Interconectado con [ADR-0001](./0001-patron-arquitectonico.md))

## Contexto
El sistema SGEMD requiere una interfaz de usuario altamente interactiva que reduzca la fricción operativa, cumpliendo con la restricción no funcional de usabilidad extrema (máximo tres clics para acciones clave)[cite: 6, 9]. Adicionalmente, el sistema exige notificaciones en tiempo real (In-App) y debe procesar subidas de archivos pesados de hasta 500 MB[cite: 6, 7].

## Decisión
Se decide adoptar **React** para la construcción del frontend como una Single Page Application (SPA) y **Node.js (con Express)** para el desarrollo de la API REST del backend[cite: 3]. Esta separación de responsabilidades asegura un cliente de renderizado rápido y un servidor altamente eficiente en el manejo de I/O[cite: 3].

## Consecuencias
* **Positivas:**
  * **Concurrencia:** La naturaleza asíncrona de Node.js es ideal para manejar los web sockets necesarios para las notificaciones In-App sin bloquear el hilo principal[cite: 7].
  * **Usabilidad:** React permite gestionar el estado en el cliente, habilitando transiciones fluidas en los dashboards y formularios[cite: 3].
* **Negativas:**
  * Exige una configuración estricta de políticas CORS y manejo de tokens (JWT) para comunicar de forma segura las dos aplicaciones separadas[cite: 3].