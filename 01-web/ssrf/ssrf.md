# Server-Side Request Forgery (SSRF)

- **WSTG:** `WSTG-INPV-19`
- **OWASP Top 10:** `A10:2021 – SSRF`
- **Alias:** SSRF

## Qué es

La aplicación hace una petición de red a una URL que controla el usuario, sin restringir el destino. El atacante consigue que **el servidor** haga peticiones en su nombre a recursos internos no expuestos.

## Cómo detectarla

- Parámetros que reciben URLs: webhooks, importadores, generadores de PDF/imágenes, previsualizadores, `?url=`, `?redirect=`, `?dest=`.
- Apunta a un servidor tuyo (Burp Collaborator / servidor propio) y observa si el servidor te contacta (out-of-band).
- Prueba destinos internos: `http://127.0.0.1`, `http://localhost`, IPs internas.

## Cómo explotarla

- **Acceso interno:** servicios en `localhost`, paneles internos, bases de datos.
- **Metadatos cloud:** `http://169.254.169.254/...` para robar credenciales de instancia (AWS/GCP/Azure).
- **Bypass de filtros:** IP en decimal/octal/hex, DNS rebinding, redirecciones, `[::]`, dominios que resuelven a interno.
- **Escaneo de puertos** internos por diferencia de respuesta/tiempo.

## Impacto

Acceso a recursos internos, robo de credenciales cloud (que suele llevar a compromiso de la infra), pivote a la red interna. A menudo alto/crítico.

## Cómo remediar

- Lista blanca de dominios/IPs de destino permitidos.
- Bloquear rangos internos y la IP de metadatos; resolver y validar tras la resolución DNS.
- Deshabilitar redirecciones y protocolos innecesarios (`file://`, `gopher://`).
- Respuestas y errores que no revelen el resultado interno.

## Referencias

- OWASP WSTG `WSTG-INPV-19` · CWE-918
- PortSwigger — SSRF

## Enlaces internos

- Checklist: `../../00-metodologia/06-checklists/07-input-validation.md`
- Redacción para informe: `../../00-metodologia/05-informe/catalogo-redacciones.md`
