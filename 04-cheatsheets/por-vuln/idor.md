# Cheatsheet · IDOR

Explicación en `../../01-web/access-control/idor.md`. **Solo sobre objetivos autorizados.**

## Qué manipular

```
/api/user/1001        ->  /api/user/1002
?id=1001              ->  ?id=1002
?uuid=...             (predecible o filtrado en otra respuesta)
Cookies / campos ocultos / JSON body con IDs
```

## Técnica (2 cuentas)

```
1. Con la cuenta A, captura la petición a un recurso propio.
2. Cámbiala al ID de la cuenta B y repite → ¿ves/modificas datos de B?
3. Prueba cambiar de método:  GET -> POST / PUT / DELETE
4. Prueba IDs por lotes para ver si son enumerables.
```

## Trucos

```
# IDs codificados
echo -n '1002' | base64
# parámetros duplicados / wrapping
id=1001&id=1002        {"id":1001,"id":1002}
# arrays
{"id":[1001,1002]}
```

## Automatización

```
# Burp Intruder / autorize / turbo intruder para enumerar IDs
# ffuf sobre el parámetro numérico
ffuf -w ids.txt -u "https://sitio/api/user/FUZZ" -H "Cookie: session=..." -mc 200
```
