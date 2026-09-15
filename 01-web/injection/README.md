# Injection

Familia de inyecciones: entrada del usuario que el backend interpreta como código/consulta.

> Cada ficha: qué es · cómo detectarla · cómo explotarla · impacto · remediación · referencias.

## Fichas

- [sqli.md](sqli.md) — **SQL Injection** — índice (detección, tipos, por motor)
- [mysql.md](mysql.md) — SQLi en MySQL/MariaDB
- [mssql.md](mssql.md) — SQLi en SQL Server
- [postgresql.md](postgresql.md) — SQLi en PostgreSQL
- [oracle.md](oracle.md) — SQLi en Oracle
- [nosqli.md](nosqli.md) — NoSQL Injection (MongoDB…)
- [command-injection.md](command-injection.md) — **Command Injection** — índice (RCE por el SO)
- [blind.md](blind.md) — Command injection ciega (OOB/time)
- [cmdi-bypass.md](cmdi-bypass.md) — Command injection — evasión de filtros
- [lfi-rfi.md](lfi-rfi.md) — **File Inclusion** — índice (LFI/RFI)
- [lfi.md](lfi.md) — LFI — lectura y bypass
- [rfi.md](rfi.md) — RFI — inclusión remota
- [lfi-to-rce.md](lfi-to-rce.md) — LFI → RCE
- [ldap.md](ldap.md) — LDAP Injection
- [xpath.md](xpath.md) — XPath Injection

## Relación con el resto del repo

- **Checklist:** `../../00-metodologia/06-checklists/07-input-validation.md`
- **Payloads:** `../../04-cheatsheets/por-vuln/`
- **Redacción para informe:** `../../00-metodologia/05-informe/catalogo-redacciones.md`
- **Nueva ficha:** copia `../_plantilla-vuln.md` en este cajón.
