# CSRF — Bypass de SameSite

Ver índice: [csrf.md](csrf.md). **Solo sobre objetivos autorizados.**

## Contexto

`SameSite` en la cookie limita cuándo se envía en peticiones cross-site:

- **Strict:** nunca en cross-site (rompe CSRF, pero también navegación normal).
- **Lax:** se envía en navegaciones top-level por **GET** (no en POST cross-site, no en subrecursos).
- **None:** se envía siempre (requiere `Secure`).
- **Sin atributo:** muchos navegadores aplican Lax por defecto.

## Bypass de Lax

- **Acción por GET:** si un endpoint que cambia estado acepta GET, una navegación top-level (`window.location`, `<a>`, `<img>` a veces) envía la cookie Lax.
- **Ventana de "Lax+POST":** algunos navegadores han tratado cookies recién creadas como enviables por POST durante un breve tiempo (comportamiento cambiante; comprobar).
- **Método override:** endpoints que aceptan `_method=POST` en un GET.

## Bypass vía subdominio / same-site

`SameSite` es **site**, no origin: un subdominio (`sub.sitio.com`) es "same-site" respecto a `sitio.com`. Si controlas o comprometes un subdominio (XSS, subdomain takeover), las peticiones desde ahí no son cross-site → la cookie viaja.

## Gadgets client-side

Un **open redirect** o un **gadget** en el propio sitio que dispare la petición hace que salga desde el mismo site, saltándose SameSite.

## Notas

- Primero comprueba el valor real de `SameSite` y si la acción acepta GET.
- Documenta la cadena completa (p. ej. subdominio + acción GET) para justificar la explotabilidad.
