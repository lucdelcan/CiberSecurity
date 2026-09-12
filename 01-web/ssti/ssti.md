# Server-Side Template Injection (SSTI)

- **WSTG:** `WSTG-INPV-18`
- **OWASP Top 10:** `A03:2021 – Injection`
- **Alias:** SSTI

## Qué es

La aplicación inserta entrada del usuario directamente en una plantilla del lado servidor (Jinja2, Twig, Freemarker, Velocity...) que luego se renderiza. El atacante inyecta sintaxis del motor de plantillas, que se evalúa en el servidor, llegando con frecuencia a RCE.

## Cómo detectarla

- Inyecta una operación matemática en la sintaxis del motor: `${7*7}`, `{{7*7}}`, `#{7*7}`, `<%= 7*7 %>`.
- Si la respuesta devuelve `49`, hay evaluación server-side.
- Usa un árbol de decisión de payloads para identificar el motor concreto según qué sintaxis evalúa.

## Cómo explotarla

1. **Identifica el motor** (qué sintaxis evalúa y cuál da error).
2. Escala del "cálculo" a **acceso a objetos/clases** del lenguaje para llegar a ejecución de comandos (p. ej. en Jinja2, cadenas de `__class__`/`__subclasses__`).
3. Ejecuta comando inocuo para demostrar RCE.

## Impacto

Habitualmente ejecución remota de código en el servidor → compromiso total. Crítico.

## Cómo remediar

- No pasar entrada del usuario como parte de la plantilla; usarla solo como **datos** (contexto), nunca como fuente de la plantilla.
- Motores en modo sandbox (con cautela, se han saltado).
- Lista blanca/escape de la entrada; lógica de plantilla mínima.

## Referencias

- OWASP WSTG `WSTG-INPV-18` · CWE-1336
- PortSwigger — Server-side template injection

## Enlaces internos

- Checklist: `../../00-metodologia/06-checklists/07-input-validation.md`
- Redacción para informe: `../../00-metodologia/05-informe/catalogo-redacciones.md`
