# Cross-Site Request Forgery (CSRF)

- **WSTG:** `WSTG-SESS-05`
- **OWASP Top 10:** `A01:2021 – Broken Access Control`
- **Alias:** CSRF, XSRF

## Qué es

Un sitio malicioso fuerza al navegador de una víctima autenticada a enviar una petición que cambia estado a la aplicación objetivo. Como el navegador adjunta las cookies automáticamente, la acción se ejecuta con la sesión de la víctima sin su consentimiento.

## Cómo detectarla

- Acciones que cambian estado (cambiar email, contraseña, transferir): ¿validan un token anti-CSRF impredecible?
- Prueba a repetir la petición **sin** el token o con uno de otra sesión: si funciona, es vulnerable.
- Revisa `SameSite` de las cookies y si aceptan la acción por GET.

## Cómo explotarla

1. Construye una página con un formulario auto-enviado (o `<img>`/fetch) que reproduzca la petición sensible.
2. Consigue que la víctima autenticada la visite.
3. La acción se ejecuta en su cuenta.
- Bypass frecuentes: token no validado, token reutilizable, método cambiable (POST→GET), Content-Type permisivo.

## Impacto

Ejecución de acciones en nombre de la víctima: cambio de credenciales/email (→ toma de cuenta), operaciones, cambios de configuración.

## Cómo remediar

- Token anti-CSRF por sesión/petición, aleatorio y validado en servidor.
- Cookies con `SameSite=Lax/Strict`.
- Reautenticación o confirmación en acciones críticas.
- No usar GET para acciones que cambian estado.

## Referencias

- OWASP WSTG `WSTG-SESS-05` · CWE-352
- OWASP CSRF Prevention Cheat Sheet

## Enlaces internos

- Checklist: `../../00-metodologia/06-checklists/06-session.md`
- Redacción para informe: `../../00-metodologia/05-informe/catalogo-redacciones.md`
