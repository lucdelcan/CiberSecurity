# CiberSecurity — Repositorio de conocimiento

Notas, metodología y recursos de pentesting con foco en hacking web.

## Estructura

| Carpeta | Contenido |
|---|---|
| `00-metodologia/` | El flujo de un pentest: recon → enumeración → explotación → post-explotación → informe. Incluye `checklists/` (WSTG/OWASP + propias). |
| `01-web/` | Una ficha por clase de vulnerabilidad web (injection, XSS, SSRF, XXE, auth, access-control, SSTI, deserialización, file-upload, request-smuggling, API, client-side). |
| `02-infra-redes/` | Lo que no es web puro: Active Directory, privesc Linux/Windows, pivoting, servicios. |
| `03-herramientas/` | Notas de uso por herramienta (Burp, Nmap, ffuf/gobuster, sqlmap, DAST) y `custom-scripts/`. |
| `04-cheatsheets/` | Acceso rápido en pleno engagement: payloads, reverse shells, comandos, wordlists. |
| `05-writeups/` | Aprendizaje documentado: HTB, CTF, bug bounty. |
| `06-certificaciones/` | Prep de certificaciones (OSCP). |
| `recursos/` | Enlaces, libros, papers, referencias. |

## Convenciones

- Las carpetas van numeradas para mantener el orden por flujo, no alfabético.
- Cada ficha de vulnerabilidad: qué es, cómo detectarla, cómo explotarla, cómo remediarla, referencias.
- Los `.gitkeep` mantienen las carpetas vacías versionadas; se pueden borrar al añadir contenido.

> **Nota:** los writeups de máquinas activas de HTB no deben publicarse. Si este repo pasa a ser público, revisa `05-writeups/htb/` (ya excluido en `.gitignore`).
