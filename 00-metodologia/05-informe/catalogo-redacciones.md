# Catálogo de redacciones reutilizables

Bloques de texto base (Descripción / Impacto / Remediación) por tipo de vuln, para **no reescribir desde cero** y mantener coherencia entre informes. **Adáptalos siempre** al caso concreto: rellena `[endpoint]`, `[parámetro]`, etc., y ajusta el impacto a lo que realmente demostraste.

> Redacción orientada a cliente. El vector CVSS de referencia lo tienes en `../00-fundamentos/cvss-scoring.md`.

---

## SQL Injection

**Descripción:** El parámetro `[parámetro]` del endpoint `[endpoint]` no valida ni parametriza correctamente la entrada antes de incluirla en una consulta SQL, permitiendo a un atacante alterar la lógica de la consulta e interactuar directamente con la base de datos.

**Impacto:** Un atacante puede extraer información confidencial de la base de datos (credenciales, datos personales), y según la configuración, modificar datos o comprometer el servidor. Se demostró [lo que se logró: p.ej. la extracción de la tabla de usuarios].

**Remediación:** Utilizar consultas parametrizadas (prepared statements) o un ORM en todas las interacciones con la base de datos. Validar la entrada con listas blancas y aplicar el principio de mínimo privilegio a la cuenta de base de datos.

---

## Cross-Site Scripting (XSS)

**Descripción:** La aplicación refleja/almacena la entrada del usuario en `[endpoint]` sin sanitizarla ni codificarla adecuadamente, permitiendo la inyección y ejecución de código JavaScript en el navegador de otros usuarios.

**Impacto:** Un atacante puede ejecutar código en el contexto de la sesión de la víctima: robo de cookies/sesión, acciones en su nombre, redirección a sitios maliciosos o modificación del contenido mostrado.

**Remediación:** Codificar la salida según el contexto (HTML, atributo, JS, URL). Validar la entrada en servidor. Implementar una política de seguridad de contenido (CSP) y marcar las cookies de sesión como `HttpOnly`.

---

## Control de acceso roto / IDOR

**Descripción:** El endpoint `[endpoint]` permite acceder a recursos de otros usuarios manipulando el identificador `[parámetro]`, sin verificar que el usuario autenticado tenga permiso sobre ese recurso.

**Impacto:** Un usuario autenticado puede acceder a (o modificar) información de otros usuarios, vulnerando la confidencialidad e integridad de los datos. Se demostró el acceso a [recurso de otro usuario].

**Remediación:** Aplicar comprobaciones de autorización del lado del servidor en cada acceso a recursos, verificando la pertenencia/permiso del usuario. No confiar en identificadores predecibles ni en controles del lado del cliente.

---

## SSRF (Server-Side Request Forgery)

**Descripción:** El parámetro `[parámetro]` de `[endpoint]` permite que el servidor realice peticiones a URLs controladas por el atacante, sin restringir los destinos permitidos.

**Impacto:** Un atacante puede hacer que el servidor acceda a recursos internos no expuestos (servicios internos, metadatos del proveedor cloud), pudiendo llegar a obtener credenciales o pivotar hacia la infraestructura interna.

**Remediación:** Validar y restringir los destinos mediante lista blanca de dominios/IPs permitidos. Bloquear rangos internos y direcciones de metadatos. Deshabilitar redirecciones y protocolos no necesarios.

---

## Autenticación débil / fuerza bruta

**Descripción:** El mecanismo de autenticación en `[endpoint]` no implementa protección contra intentos automatizados (rate limiting, bloqueo, CAPTCHA), permitiendo ataques de fuerza bruta o credential stuffing.

**Impacto:** Un atacante puede probar grandes volúmenes de credenciales y comprometer cuentas con contraseñas débiles o reutilizadas.

**Remediación:** Implementar rate limiting y bloqueo temporal tras varios intentos fallidos, exigir contraseñas robustas, ofrecer MFA y monitorizar accesos anómalos.

---

## Exposición de información sensible

**Descripción:** La aplicación expone información sensible en `[ubicación]` (mensajes de error detallados, ficheros de configuración, datos internos) accesible sin autorización.

**Impacto:** La información revelada facilita a un atacante el conocimiento de la infraestructura y el diseño de ataques dirigidos.

**Remediación:** Deshabilitar mensajes de error detallados en producción, retirar ficheros y endpoints innecesarios, y revisar qué datos se devuelven al cliente.

---

## Configuración de seguridad deficiente / cabeceras

**Descripción:** La aplicación no implementa cabeceras de seguridad recomendadas (`[cabeceras: CSP, HSTS, X-Content-Type-Options...]`) y/o mantiene configuraciones por defecto inseguras.

**Impacto:** Aumenta la superficie de ataque y facilita la explotación de otras vulnerabilidades (clickjacking, downgrade, MIME sniffing). Riesgo generalmente bajo por sí solo.

**Remediación:** Aplicar las cabeceras de seguridad adecuadas, revisar y endurecer la configuración por defecto de servidor y framework.

---

## CSRF (Cross-Site Request Forgery)

**Descripción:** La acción `[acción]` en `[endpoint]` no valida un token anti-CSRF, permitiendo que un tercero fuerce peticiones en nombre de un usuario autenticado.

**Impacto:** Un atacante puede provocar acciones no deseadas en la cuenta de la víctima (cambios de datos, operaciones) sin su consentimiento.

**Remediación:** Implementar tokens anti-CSRF por sesión/petición, usar el atributo `SameSite` en las cookies y validar el origen de las peticiones que modifican estado.

---

## Cómo mantener este catálogo

- Cada vez que redactes un finding nuevo bueno, **abstráelo** y añádelo aquí.
- Mantén el mismo estilo de los tres bloques (Descripción / Impacto / Remediación).
- Enlaza cada tipo con su ficha técnica en `../../01-web/` y su cheatsheet de payloads en `../../04-cheatsheets/por-vuln/`.
