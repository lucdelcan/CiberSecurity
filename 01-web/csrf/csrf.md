# Cross-Site Request Forgery (CSRF) — Índice

- **WSTG:** `WSTG-SESS-05`
- **OWASP Top 10:** `A01:2021 – Broken Access Control`
- **Alias:** CSRF, XSRF

## Qué es

Un sitio malicioso fuerza al navegador de una víctima autenticada a enviar una petición que cambia estado a la aplicación objetivo. Como el navegador adjunta las cookies automáticamente, la acción se ejecuta con la sesión de la víctima sin su consentimiento.

## PoC base

```html
<form action="https://sitio/cambiar-email" method="POST">
  <input type="hidden" name="email" value="atacante@evil.com">
</form>
<script>document.forms[0].submit()</script>
```

## Fichas a fondo

| Tema | Ficha |
|---|---|
| Saltarse la validación del token | [token-bypass.md](token-bypass.md) |
| Bypass de la protección SameSite | [samesite-bypass.md](samesite-bypass.md) |

## Impacto

Ejecución de acciones en nombre de la víctima: cambio de email/contraseña (→ toma de cuenta), operaciones, cambios de configuración.

## Remediación (común)

- Token anti-CSRF por sesión/petición, aleatorio y validado en servidor.
- Cookies `SameSite=Lax/Strict`.
- Reautenticación en acciones críticas; no usar GET para cambiar estado.

## Enlaces internos

- Payloads: `../../04-cheatsheets/por-vuln/csrf.md`
- Checklist: `../../00-metodologia/06-checklists/06-session.md`
- Redacción: `../../00-metodologia/05-informe/catalogo-redacciones.md`
- Referencias: `WSTG-SESS-05` · CWE-352 · PortSwigger — CSRF
