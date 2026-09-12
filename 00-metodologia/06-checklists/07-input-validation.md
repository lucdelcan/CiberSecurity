# WSTG-INPV · Input Validation

La categoría más grande. Las fichas técnicas de cada vuln van en `../../01-web/`.

- [ ] `WSTG-INPV-01` **Reflected XSS** — Inyectar JS que se refleja en la respuesta y se ejecuta en la víctima.
- [ ] `WSTG-INPV-02` **Stored XSS** — Inyectar JS que se almacena y se ejecuta a otros usuarios.
- [ ] `WSTG-INPV-03` **HTTP Verb Tampering** — Cambiar el método HTTP para saltarse restricciones.
- [ ] `WSTG-INPV-04` **HTTP Parameter Pollution** — Duplicar parámetros para confundir la lógica del servidor.
- [ ] `WSTG-INPV-05` **SQL Injection** — Inyectar SQL para manipular la consulta y acceder a la BD.
  - [ ] `05.1` Oracle · `05.2` MySQL · `05.3` SQL Server · `05.4` PostgreSQL · `05.5` MS Access
  - [ ] `05.6` NoSQL Injection · `05.7` ORM Injection · `05.8` Client-side
- [ ] `WSTG-INPV-06` **LDAP Injection** — Inyectar en consultas LDAP (bypass de login, extracción).
- [ ] `WSTG-INPV-07` **XML Injection** — Inyectar en XML; incluye XXE (leer ficheros, SSRF).
- [ ] `WSTG-INPV-08` **SSI Injection** — Inyectar directivas Server-Side Includes.
- [ ] `WSTG-INPV-09` **XPath Injection** — Inyectar en consultas XPath.
- [ ] `WSTG-INPV-10` **IMAP/SMTP Injection** — Inyectar comandos en servicios de correo.
- [ ] `WSTG-INPV-11` **Code Injection** — Inyectar código que ejecuta el servidor.
  - [ ] `11.1` Local File Inclusion (LFI) · `11.2` Remote File Inclusion (RFI)
- [ ] `WSTG-INPV-12` **Command Injection** — Ejecutar comandos del sistema operativo.
- [ ] `WSTG-INPV-13` **Format String** — Abusar de cadenas de formato mal tratadas.
- [ ] `WSTG-INPV-14` **Incubated Vulnerability** — Payload que se almacena y detona más tarde (persistente encadenado).
- [ ] `WSTG-INPV-15` **HTTP Splitting/Smuggling** — Desincronizar proxy y servidor con peticiones ambiguas.
- [ ] `WSTG-INPV-16` **HTTP Incoming Requests** — Monitorizar peticiones para detectar comportamientos anómalos.
- [ ] `WSTG-INPV-17` **Host Header Injection** — Abusar de la cabecera `Host` (cache poisoning, password reset).
- [ ] `WSTG-INPV-18` **SSTI** — Inyección en plantillas del servidor; suele llevar a RCE.
- [ ] `WSTG-INPV-19` **SSRF** — Forzar al servidor a hacer peticiones a destinos internos.
