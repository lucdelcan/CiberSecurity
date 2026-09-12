# Command Injection

- **WSTG:** `WSTG-INPV-12`
- **OWASP Top 10:** `A03:2021 – Injection`
- **Alias:** OS command injection, inyección de comandos

## Qué es

La aplicación pasa entrada del usuario a una llamada del sistema operativo (shell) sin sanitizarla. El atacante encadena comandos propios usando operadores del shell, consiguiendo ejecución de comandos (RCE) en el servidor.

## Cómo detectarla

- Inyecta operadores de encadenamiento en parámetros que puedan acabar en una llamada al SO (ping, conversores, exportadores):
  `;`, `&&`, `|`, `||`, `` ` ` ``, `$( )`, `%0a` (nueva línea).
- Confirma con un comando observable: `; id`, `| whoami`, o **out-of-band** si no ves salida: `; ping -c1 tu-ip`, `; curl http://tu-ip`.
- Blind: usa retardo (`; sleep 5`) o exfiltración por DNS/HTTP.

## Cómo explotarla

1. Determina el contexto (¿comillas?, ¿Windows o Linux?) y el operador que funciona.
2. Ejecuta algo inocuo para probar impacto (`id`, `hostname`).
3. Si hay filtros, evádelos: variables (`c$@at`), codificación, `$IFS` en lugar de espacios, comodines.
4. Escala a una reverse shell → ver `../../04-cheatsheets/por-fase/03-explotacion.md`.

## Impacto

Ejecución de comandos arbitrarios en el servidor con los privilegios del servicio web → compromiso total del host, pivote a la red interna. Crítico.

## Cómo remediar

- Evitar llamar al shell; usar APIs nativas del lenguaje.
- Si es inevitable, usar funciones que separan comando y argumentos (arrays), nunca concatenar.
- Lista blanca estricta de valores permitidos.
- Mínimo privilegio del servicio.

## Referencias

- OWASP WSTG `WSTG-INPV-12` · CWE-78
- PortSwigger — OS command injection

## Enlaces internos

- Checklist: `../../00-metodologia/06-checklists/07-input-validation.md`
- Redacción para informe: `../../00-metodologia/05-informe/catalogo-redacciones.md`
