# XSS Basado en DOM (DOM-based)

- **WSTG:** `WSTG-CLNT-01`
- **OWASP Top 10:** `A03:2021 – Injection`
- Ver índice: [xss.md](xss.md)

## Qué es

La vulnerabilidad está **en el JavaScript del cliente**, no en la respuesta del servidor. El código toma datos de una fuente controlable (`source`) y los escribe en un punto peligroso (`sink`) sin sanitizar, ejecutándose en el navegador. El servidor puede no ver nunca el payload (p. ej. si va en el fragmento `#`).

## Sources (de dónde sale el dato)

```
location, location.href, location.search, location.hash, document.URL,
document.referrer, window.name, postMessage, localStorage/sessionStorage
```

## Sinks (dónde acaba y se ejecuta)

```
innerHTML, outerHTML, insertAdjacentHTML, document.write, document.writeln,
eval, setTimeout/setInterval(string), Function, location/location.href,
element.src, jQuery: $(...), .html(), .append()
```

## Cómo detectarla

1. Revisa el JS del cliente buscando el flujo **source → sink** sin sanitización.
2. Prueba manualmente: pon un payload en un source (p. ej. el `#` de la URL) y mira si llega a un sink.
   - Ejemplo: `https://sitio/#<img src=x onerror=alert(1)>` si el hash se escribe con `innerHTML`.
3. Herramientas: DevTools (breakpoints en los sinks), y análisis estático del JS.

## Cómo explotarla

1. Controla el source (URL, hash, `postMessage`, `window.name`).
2. Ajusta el payload al sink (algunos ejecutan HTML, otros JS directo como `eval`).
3. Como el payload puede ir en el fragmento `#`, a menudo **no llega al servidor** → no lo ve un WAF ni queda en logs.

## Impacto

Igual que otros XSS (ejecución en la sesión de la víctima), pero con la particularidad de que ocurre íntegramente en cliente, lo que complica su detección server-side.

## Cómo remediar

- Evitar sinks peligrosos; usar APIs seguras (`textContent`, `setAttribute`).
- Sanitizar con **DOMPurify** antes de escribir en el DOM.
- Trusted Types (donde esté disponible) para bloquear sinks peligrosos.
- CSP como defensa en profundidad.

## Referencias

- OWASP WSTG `WSTG-CLNT-01` · CWE-79 · PortSwigger — DOM-based XSS
