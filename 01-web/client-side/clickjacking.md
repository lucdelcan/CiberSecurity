# Clickjacking

- **WSTG:** `WSTG-CLNT-09`
- **OWASP Top 10:** `A05:2021 – Security Misconfiguration`
- **Alias:** UI redressing

## Qué es

El atacante enmarca la aplicación víctima en un `iframe` transparente sobre su propia página y engaña al usuario para que haga clics que en realidad actúan sobre la app legítima (con su sesión).

## Cómo detectarla

- Comprueba si la respuesta permite ser enmarcada: ausencia de `X-Frame-Options` o de `frame-ancestors` en la CSP.
- Monta una PoC con un `<iframe>` apuntando a la página y verifica que se renderiza.

## Cómo explotarla

- Superponer controles engañosos sobre acciones sensibles (cambiar config, aceptar permisos, transferir).
- Combinar con drag&drop o multi-paso para acciones más complejas.

## Impacto

Acciones no deseadas ejecutadas por la víctima con su sesión. Impacto según la acción enmarcada.

## Cómo remediar

- `Content-Security-Policy: frame-ancestors 'self'` (o lista blanca).
- `X-Frame-Options: DENY`/`SAMEORIGIN` como compatibilidad.
- Confirmaciones en acciones críticas.

## Referencias

- OWASP WSTG `WSTG-CLNT-09` · CWE-1021

## Enlaces internos

- Checklist: `../../00-metodologia/06-checklists/11-client-side.md`
- Redacción para informe: `../../00-metodologia/05-informe/catalogo-redacciones.md`
