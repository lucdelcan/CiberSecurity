# CiberSecurity — Repositorio de conocimiento

Notas, metodología y recursos de pentesting con foco en hacking web.

## Estructura

| Carpeta | Contenido |
|---|---|
| `00-metodologia/` | El flujo de un pentest (numerado por fase): recon → enumeración → explotación → post-explotación → informe, más `06-checklists/`. |
| `01-web/` | Una ficha por clase de vulnerabilidad web (injection, XSS, SSRF, XXE, auth, access-control, SSTI, deserialización, file-upload, request-smuggling, API, client-side). |
| `02-infra-redes/` | Lo que no es web puro: Active Directory, privesc Linux/Windows, pivoting, servicios. |
| `03-herramientas/` | Notas de uso por herramienta (Burp, Nmap, ffuf/gobuster, sqlmap, DAST) y `custom-scripts/`. |
| `04-cheatsheets/` | Acceso rápido en pleno engagement: payloads, reverse shells, comandos, wordlists. |
| `05-writeups/` | Aprendizaje documentado (vacía por ahora). |
| `recursos/` | Enlaces, libros, papers, referencias. |

## Convenciones

- Se numera lo que tiene una **secuencia** (metodología). Los catálogos (web, herramientas) van en alfabético.
- Cada ficha de vulnerabilidad: qué es, cómo detectarla, cómo explotarla, cómo remediarla, referencias.
- Los `.gitkeep` mantienen las carpetas vacías versionadas; se pueden borrar al añadir contenido.

> **Nota:** si este repo pasa a ser público, revisa que los writeups no incluyan contenido de plataformas con máquinas activas ni material con licencia/copyright de terceros.
