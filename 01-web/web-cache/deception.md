# Web Cache Deception

Ver índice: [web-cache.md](web-cache.md). **Solo sobre objetivos autorizados.**

## Idea

Engañar a la caché para que **almacene una respuesta con datos privados** de una víctima, y luego recuperarla tú desde una URL pública/cacheada.

## Método

1. Muchas cachés guardan por **extensión estática** (`.css`, `.js`, `.jpg`) o por rutas "estáticas".
2. Pide una página dinámica y sensible de la víctima con un sufijo estático que el backend ignore pero la caché sí considere cacheable:
```
https://sitio/mi-cuenta            -> dinámico, privado
https://sitio/mi-cuenta/foo.css    -> backend sirve la cuenta; la caché lo guarda como "estático"
https://sitio/mi-cuenta%0Afoo.css
https://sitio/mi-cuenta;foo.css
```
3. Si la víctima (autenticada) visita ese enlace, su respuesta privada queda cacheada.
4. Tú accedes a la misma URL (sin sesión) y recuperas sus datos desde la caché.

## Requisitos

- El backend debe devolver el contenido dinámico pese al sufijo (path confusion).
- La caché debe decidir cachear por la extensión/patrón.

## Notas

- Depende de la discrepancia de interpretación de la ruta entre caché y backend.
- Reporta como fuga de datos sensibles (confidencialidad).
