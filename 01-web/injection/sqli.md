# SQL Injection (SQLi) — Índice

- **WSTG:** `WSTG-INPV-05`
- **OWASP Top 10:** `A03:2021 – Injection`
- **Alias:** SQLi, inyección SQL

## Qué es

Ocurre cuando la aplicación construye una consulta SQL concatenando entrada del usuario sin parametrizarla. El atacante rompe los límites del dato (típicamente con `'`) y escribe SQL que el motor interpreta como código, alterando la consulta e interactuando con la base de datos.

```php
$q = "SELECT * FROM users WHERE username = '" . $_GET['user'] . "'";
```

## Detección (común a todos los motores)

- `'` → ¿error o cambio? · `'` rompe y `''` repara → SQLi.
- Booleano: `' OR '1'='1` vs `' AND '1'='2`.
- Numérico: `1`, `1-0`, `1 OR 1=1`.
- Comentarios para truncar: `-- -`, `#`, `/* */`.

## Tipos (cómo recuperas la salida)

- **In-band:** *Union-based* y *Error-based* (ves la salida).
- **Blind:** *Boolean-based* y *Time-based* (la infieres).
- **Out-of-band (OOB):** exfiltras por un canal externo (DNS/HTTP).

## Fichas por motor

La sintaxis (comentarios, funciones, enumeración del esquema, retardo) cambia según el motor:

| Motor | Ficha |
|---|---|
| MySQL / MariaDB | [mysql.md](mysql.md) |
| Microsoft SQL Server | [mssql.md](mssql.md) |
| PostgreSQL | [postgresql.md](postgresql.md) |
| Oracle | [oracle.md](oracle.md) |
| NoSQL (MongoDB…) | [nosqli.md](nosqli.md) |

## Impacto

Acceso a toda la BD (credenciales, datos personales), modificación/borrado, bypass de autenticación y, según privilegios, lectura/escritura de ficheros o RCE. Suele ser crítico.

## Remediación (común)

- **Consultas parametrizadas / ORM** en todas las interacciones (defensa principal).
- Nunca concatenar entrada del usuario.
- Validación con listas blancas; **mínimo privilegio** de la cuenta de BD.
- Errores genéricos en producción; WAF solo como defensa en profundidad.

## Enlaces internos

- Payloads: `../../04-cheatsheets/por-vuln/sqli.md`
- Checklist: `../../00-metodologia/06-checklists/07-input-validation.md`
- Redacción para informe: `../../00-metodologia/05-informe/catalogo-redacciones.md`
- Referencias: OWASP WSTG `WSTG-INPV-05` · CWE-89 · PortSwigger — SQL injection
