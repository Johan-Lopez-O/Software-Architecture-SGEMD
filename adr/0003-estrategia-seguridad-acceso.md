# ADR-0003: Autenticación sin estado (JWT) y Validación OTP en Backend

**Estado:** PROPUESTO (Interconectado con ADR-0001 y ADR-0002)

## Contexto
En la iteración pasada del proyecto, los mecanismos de autorización eran deficientes: los códigos de verificación de correo se exponían en las respuestas JSON y los roles no se validaban correctamente en los endpoints, permitiendo el acceso cruzado a información confidencial (como actas de compromiso y diagnósticos).

## Decisión
Se propone una estrategia de seguridad en tres capas:
1. Contraseñas hasheadas exclusivamente con Bcrypt (salt 10+).
2. Autenticación mediante JSON Web Tokens (JWT) con expiración de 8 horas.
3. Validación estricta de OTP (One Time Password) de 8 dígitos para el registro, donde el código se persiste temporalmente en PostgreSQL, se envía vía SMTP y se cruza internamente en el backend. En ningún caso se devolverá el código al cliente.

## Consecuencias
* **Positivas:**
  * Cierra las brechas de seguridad previas, cumpliendo con la autorización restringida por rol y alcance exigida.
  * Evita la manipulación del estado de verificación de correo desde el frontend.
* **Negativas:**
  * Incrementa la complejidad de la configuración del entorno de desarrollo al requerir credenciales válidas de un servidor SMTP.