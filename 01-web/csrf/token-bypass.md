# CSRF — Bypass del token

Ver índice: [csrf.md](csrf.md). **Solo sobre objetivos autorizados.** Cuando hay token anti-CSRF pero está mal validado.

## Comprobaciones típicas que fallan

```
- Quitar el parámetro/cabecera del token  -> ¿sigue aceptando la acción?
- Enviar el token vacío  (csrf=)
- Usar el token de OTRA sesión / de otra cuenta  -> ¿lo ata a la sesión?
- Cambiar el método  POST -> GET   (si acepta ambos)
- El token solo se valida si está presente (se puede omitir el campo)
```

## El token no está atado al usuario

Si el token es válido "en general" pero no ligado a la sesión de quien lo usa, un atacante consigue un token propio y lo mete en la PoC de la víctima.

## Token en cookie duplicada (double-submit mal hecho)

Si la defensa compara un token de cookie con uno de parámetro y el atacante puede **fijar** la cookie (cookie injection / subdominio), controla ambos valores.

## Content-Type para evitar preflight

Con `text/plain` (o `application/x-www-form-urlencoded`) evitas el preflight CORS y puedes enviar la petición desde un formulario/fetch simple.

## Notas

- Prueba siempre primero "quitar el token" y "token de otra sesión": son los fallos más comunes.
- Si hay XSS, el token deja de proteger (se lee y se envía) → encadena.
