# Open Redirect

- **WSTG:** `WSTG-CLNT-04`
- **OWASP Top 10:** `A01:2021 – Broken Access Control`
- **Alias:** redirección abierta

## Qué es

La aplicación redirige a una URL controlada por el usuario sin validarla. Se abusa para phishing (parece un enlace legítimo) o como pieza para escalar otras vulns (robo de tokens OAuth, bypass de filtros SSRF).

## Cómo detectarla

- Parámetros de redirección: `?redirect=`, `?next=`, `?url=`, `?returnTo=`, `?dest=`.
- Cambia el valor por `https://tu-dominio` y comprueba si redirige fuera.
- Bypass: `//evil.com`, `https:evil.com`, `/\evil.com`, `@evil.com`, codificación.

## Cómo explotarla

- **Phishing:** enviar un enlace del dominio confiable que acaba en tu página.
- **Robo de token:** si un flujo OAuth/SSO usa el parámetro como `redirect_uri`, puedes exfiltrar el código/token.
- Encadenado con otras vulns para saltar validaciones de destino.

## Impacto

Por sí solo suele ser bajo/medio (phishing); alto si permite robar tokens de autenticación en flujos OAuth.

## Cómo remediar

- Lista blanca de destinos permitidos; evitar redirecciones basadas en entrada del usuario.
- Usar rutas relativas o identificadores mapeados, no URLs completas.
- Validar el destino completo (esquema + host).

## Referencias

- OWASP WSTG `WSTG-CLNT-04` · CWE-601

## Enlaces internos

- Checklist: `../../00-metodologia/06-checklists/11-client-side.md`
- Redacción para informe: `../../00-metodologia/05-informe/catalogo-redacciones.md`
