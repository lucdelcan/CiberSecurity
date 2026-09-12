# CORS Misconfiguration

- **WSTG:** `WSTG-CLNT-07`
- **OWASP Top 10:** `A05:2021 – Security Misconfiguration`
- **Alias:** CORS mal configurado

## Qué es

Una política CORS demasiado permisiva permite que orígenes no confiables lean respuestas autenticadas de la aplicación, saltándose la Same-Origin Policy.

## Cómo detectarla

- Envía una petición con cabecera `Origin:` arbitraria y observa la respuesta:
  - ¿Refleja tu `Origin` en `Access-Control-Allow-Origin`?
  - ¿Devuelve `Access-Control-Allow-Credentials: true` junto con un origen reflejado o `null`?
- Prueba orígenes: reflejo del tuyo, `null`, subdominios, sufijos/prefijos que burlen una validación floja.

## Cómo explotarla

- Si refleja el origen **y** permite credenciales, una página maliciosa puede hacer peticiones autenticadas y **leer** la respuesta (datos privados, tokens).
- `ACAO: *` sin credenciales es menos grave (no lee datos autenticados) pero puede exponer datos sensibles no autenticados.

## Impacto

Robo de datos sensibles de usuarios autenticados desde un sitio controlado por el atacante.

## Cómo remediar

- Lista blanca estricta de orígenes; no reflejar el `Origin` sin validar.
- No combinar `Allow-Credentials: true` con orígenes dinámicos ni con `null`.
- Validar el origen completo, no por subcadenas.

## Referencias

- OWASP WSTG `WSTG-CLNT-07` · CWE-942
- PortSwigger — CORS

## Enlaces internos

- Checklist: `../../00-metodologia/06-checklists/11-client-side.md`
- Redacción para informe: `../../00-metodologia/05-informe/catalogo-redacciones.md`
