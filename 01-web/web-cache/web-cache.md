# Web Cache Attacks — Índice

- **WSTG:** relacionado con `WSTG-CONF` / `WSTG-INPV-17` (Host header)
- **OWASP Top 10:** `A05:2021 – Security Misconfiguration`
- **Alias:** cache poisoning, cache deception

## Concepto clave: la clave de caché

Una caché sirve una respuesta guardada a peticiones que considera "iguales" según su **cache key** (normalmente método + host + path + algunos parámetros). Todo lo que afecta la respuesta pero **no** entra en la clave ("unkeyed input") es la raíz de estos ataques.

## Fichas a fondo

| Tema | Ficha |
|---|---|
| Cache Poisoning | [poisoning.md](poisoning.md) |
| Cache Deception | [deception.md](deception.md) |

## Impacto

Poisoning: distribuir contenido malicioso (XSS, redirect) a todos los usuarios. Deception: robar datos sensibles cacheados de una víctima.

## Remediación (común)

- Configurar bien la clave de caché (incluir todo input que afecte la respuesta).
- No cachear contenido sensible/autenticado; `Cache-Control` correcto.
- Normalizar/validar `Host` y `X-Forwarded-*`.

## Enlaces internos

- Checklist: `../../00-metodologia/06-checklists/02-config-deploy.md`
- Redacción: `../../00-metodologia/05-informe/catalogo-redacciones.md`
- Referencias: CWE-524 · PortSwigger — Web cache poisoning / deception
