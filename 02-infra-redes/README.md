# 02 · Infra & Redes

Lo que no es web puro: post-explotación a nivel de sistema, Active Directory, escalada local y movimiento por la red interna. Complementa a `01-web/` cuando un compromiso web da acceso al host o a la red.

## Cajones

| Carpeta | Contenido |
|---|---|
| `active-directory/` | Enumeración y ataques a AD (Kerberos, ACLs, relay, delegaciones). |
| `linux-privesc/` | Escalada de privilegios en Linux. |
| `windows-privesc/` | Escalada de privilegios en Windows. |
| `pivoting/` | Movimiento lateral, túneles y port forwarding. |
| `servicios/` | Ataque a servicios comunes (SMB, SNMP, SSH, RDP, bases de datos…). |

## Cómo se usa

- El *proceso* de alto nivel está en `../00-metodologia/04-post-explotacion/`; aquí va el **detalle técnico**.
- Comandos de reconocimiento post-acceso en `../04-cheatsheets/por-fase/04-post-explotacion.md`.
- Mismo formato de ficha que `01-web/` (copia `../01-web/_plantilla-vuln.md` adaptando).
