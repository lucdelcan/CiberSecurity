# Web Cache Poisoning

Ver índice: [web-cache.md](web-cache.md). **Solo sobre objetivos autorizados.**

## Idea

Conseguir que la caché **almacene** una respuesta maliciosa que luego se sirve a otros usuarios. Se explota un input que influye en la respuesta pero **no** forma parte de la clave de caché (unkeyed).

## Método

1. **Identifica la caché** y los indicadores: `X-Cache: hit/miss`, `Age`, `Cache-Control`, cabeceras de CDN.
2. **Encuentra un unkeyed input** que afecte la respuesta: cabeceras como `X-Forwarded-Host`, `X-Forwarded-Scheme`, `X-Host`, `X-Forwarded-For`, parámetros ignorados por la clave.
3. **Comprueba el impacto:** ¿ese input se refleja en la respuesta (URL absoluta, `<script src>`, redirect)?
4. **Envenena:** manda la petición con el input malicioso hasta que la respuesta quede cacheada (`X-Cache: hit` para otros).

## Ejemplos de payload

```
GET /
X-Forwarded-Host: evil.com          # si la página construye URLs absolutas con ese valor
# -> se cachea un <script src="//evil.com/..."> servido a todos

X-Forwarded-Scheme: nothttps        # forzar redirect cacheado
```

## Cache key manipulation

Ajusta la petición para que **entre** en la clave que usarán las víctimas (mismo path/params) pero llevando el input no incluido en la clave.

## Notas

- Prueba también "cache key injection" y parámetros que la caché normaliza distinto que el backend.
- Confirma que el envenenamiento afecta a peticiones limpias (no solo a la tuya).
