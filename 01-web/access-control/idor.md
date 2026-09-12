# IDOR (Insecure Direct Object Reference)

- **WSTG:** `WSTG-AUTHZ-04`
- **OWASP Top 10:** `A01:2021 – Broken Access Control`
- **Alias:** IDOR, referencia directa insegura a objetos

## Qué es

La aplicación expone una referencia a un objeto (un `id`, un nombre de fichero) y decide el acceso solo por esa referencia, sin verificar en el servidor que el usuario autenticado tenga permiso sobre ese objeto. Cambiando la referencia se accede a datos de otros.

## Cómo detectarla

- Endpoints con identificadores: `?id=`, `/user/1001`, `/invoice/523.pdf`, IDs en JSON o cookies.
- Con **dos cuentas** del mismo rol, intenta acceder a los recursos de una desde la otra cambiando el ID.
- Prueba IDs secuenciales, predecibles, o codificados (base64) que puedas manipular.

## Cómo explotarla

1. Captura una petición legítima a un recurso propio.
2. Cambia el identificador por el de otro usuario y repite.
3. Si obtienes datos ajenos (o puedes modificarlos), hay IDOR. Prueba también métodos (GET→POST/PUT/DELETE).

## Impacto

Acceso o modificación no autorizada de datos de otros usuarios: confidencialidad e integridad. Escala a masivo si los IDs son enumerables.

## Cómo remediar

- Comprobar autorización **en el servidor en cada acceso**, verificando pertenencia/permiso del usuario sobre el objeto.
- Usar referencias indirectas por sesión o IDs no predecibles (UUID) — como capa, no como única defensa.
- No confiar en controles del lado cliente.

## Referencias

- OWASP WSTG `WSTG-AUTHZ-04` · CWE-639
- PortSwigger — Access control (IDOR)

## Enlaces internos

- Checklist: `../../00-metodologia/06-checklists/05-authorization.md`
- Redacción para informe: `../../00-metodologia/05-informe/catalogo-redacciones.md`
