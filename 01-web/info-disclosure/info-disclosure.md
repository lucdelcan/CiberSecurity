# Information Disclosure

- **WSTG:** `WSTG-INFO-*`, `WSTG-ERR-*`
- **OWASP Top 10:** `A05:2021 – Security Misconfiguration`
- **Alias:** fuga de información, divulgación

## Qué es

La aplicación revela información que ayuda a un atacante: mensajes de error detallados, ficheros de configuración, código fuente, datos internos, versiones, o comentarios reveladores.

## Cómo detectarla

- Provoca errores y revisa si devuelven trazas, rutas o versiones.
- Busca ficheros expuestos: `.git/`, `.env`, backups (`.bak`, `.old`, `.zip`), `robots.txt`, `sitemap.xml`.
- Revisa código fuente/JS y comentarios HTML por claves, endpoints o rutas.
- Cabeceras que filtran tecnología y versiones.

## Cómo explotarla

- Encadenar la info para ataques dirigidos (versiones → exploits conocidos; `.git` → código fuente completo; `.env` → credenciales).

## Impacto

Habilita otros ataques; puede ser directo si expone credenciales o datos sensibles.

## Cómo remediar

- Errores genéricos en producción; sin trazas al usuario.
- Retirar ficheros y endpoints innecesarios; bloquear rutas sensibles (`.git`, backups).
- Minimizar cabeceras que revelan tecnología.

## Referencias

- OWASP WSTG `WSTG-INFO-*`, `WSTG-ERR-*` · CWE-200

## Enlaces internos

- Checklist: `../../00-metodologia/06-checklists/01-info-gathering.md`
- Redacción para informe: `../../00-metodologia/05-informe/catalogo-redacciones.md`
