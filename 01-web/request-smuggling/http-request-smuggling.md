# HTTP Request Smuggling

- **WSTG:** `WSTG-INPV-15`
- **OWASP Top 10:** `A05:2021 – Security Misconfiguration`
- **Alias:** desincronización HTTP, HTTP desync

## Qué es

Cuando una cadena front-end (proxy/CDN/balanceador) y el back-end interpretan de forma distinta dónde acaba una petición HTTP, un atacante puede "colar" parte de una petición al principio de la siguiente de otro usuario. Nace de discrepancias entre las cabeceras `Content-Length` (CL) y `Transfer-Encoding` (TE).

## Variantes

- **CL.TE:** el front-end usa `Content-Length`, el back-end usa `Transfer-Encoding`.
- **TE.CL:** al revés.
- **TE.TE:** ambos soportan TE pero uno se puede "ofuscar" para que lo ignore.
- **H2.CL / H2.TE:** downgrade de HTTP/2 a HTTP/1.1 con desincronización (request smuggling en HTTP/2).

## Cómo detectarla

- Envía peticiones con CL y TE a la vez y observa retrasos/respuestas anómalas (técnica de time-based con `TE` malformado).
- La extensión **HTTP Request Smuggler** (Burp) automatiza la detección de CL.TE/TE.CL/H2.
- Confirma con una petición que "envenene" la siguiente respuesta de forma controlada.

## Cómo explotarla

- **Robar peticiones de otros usuarios** (capturar su cookie/credenciales en un endpoint que refleje el cuerpo).
- **Bypass de controles del front-end** (llegar a rutas que el proxy bloquea).
- **Envenenar la cola de respuestas** → servir tu contenido a otros.
- Encadenar con cache poisoning o XSS.

## Impacto

Compromiso de peticiones/sesiones de otros usuarios, bypass de seguridad perimetral. Suele ser alto.

## Cómo remediar

- Normalizar y rechazar peticiones ambiguas (CL + TE juntas) en el front-end.
- Usar HTTP/2 de extremo a extremo sin downgrade a HTTP/1.1.
- Que front-end y back-end compartan la misma implementación/parsing.

## Referencias

- OWASP WSTG `WSTG-INPV-15` · CWE-444
- PortSwigger — HTTP request smuggling

## Enlaces internos

- Checklist: `../../00-metodologia/06-checklists/07-input-validation.md`
- Redacción: `../../00-metodologia/05-informe/catalogo-redacciones.md`
