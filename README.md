# CiberSecurity

Base de conocimiento de pentesting con foco en **hacking web**: metodología, fichas por vulnerabilidad, cheatsheets, checklists y material de apoyo. Pensada para consultarse en pleno engagement y para crecer con el tiempo.

## Cómo navegar

Cada sección tiene su propio `README.md` que hace de índice. El flujo natural:

1. **Empieza por la metodología** (`00-metodologia/`) para saber *qué hacer y en qué orden*.
2. **Consulta la vuln concreta** en `01-web/` (o `02-infra-redes/`) para saber *cómo* atacarla.
3. **Copia el payload** desde `04-cheatsheets/`.
4. **Redacta el hallazgo** con `00-metodologia/05-informe/`.

## Mapa del repositorio

| Sección | Qué contiene |
|---|---|
| [`00-metodologia/`](00-metodologia/README.md) | El proceso de un pentest por fases: fundamentos → recon → enumeración → explotación → post-explotación → informe, más checklists WSTG. |
| [`01-web/`](01-web/README.md) | Fichas por clase de vulnerabilidad web. Cada cajón (injection, xss, ssrf…) tiene su índice. |
| [`02-infra-redes/`](02-infra-redes/README.md) | Lo que no es web puro: Active Directory, privesc Linux/Windows, pivoting, servicios. |
| [`03-herramientas/`](03-herramientas/README.md) | Notas de uso por herramienta (Burp, Nmap, ffuf, sqlmap, DAST). |
| [`04-cheatsheets/`](04-cheatsheets/README.md) | Payloads y comandos listos para pegar: por fase, por vuln y transversales. |
| [`05-writeups/`](05-writeups/README.md) | Aprendizaje documentado (CTF, bug bounty, labs). |
| [`recursos/`](recursos/README.md) | Enlaces, libros, papers y referencias. |

## Las cuatro piezas de cada vulnerabilidad

Todo está enlazado para trabajar una vuln de principio a fin:

1. **Ficha** (`01-web/<cajón>/`) — entiéndela.
2. **Checklist** (`00-metodologia/06-checklists/`) — no olvides probarla (mismo `WSTG-ID`).
3. **Cheatsheet** (`04-cheatsheets/por-vuln/`) — payloads para pegar.
4. **Redacción** (`00-metodologia/05-informe/catalogo-redacciones.md`) — cómo reportarla.

## Convenciones

- Se **numera** lo que tiene una secuencia (metodología); los catálogos (web, herramientas) van en alfabético.
- **Cajón = categoría** (carpeta), **fichero = vulnerabilidad concreta**. Vuln nueva → nuevo `.md` en su cajón.
- Cada ficha sigue `01-web/_plantilla-vuln.md`: qué es · detección · explotación · impacto · remediación · referencias.
- Los `.gitkeep` mantienen versionadas las carpetas aún vacías.

## Aviso legal

Todo el contenido es para uso en **entornos autorizados** (engagements con permiso, laboratorios propios). 