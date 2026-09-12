# Enumeration

Ya sobre la aplicación: mapear la app por dentro. La diferencia con recon es que aquí trabajas contra la superficie ya identificada.

## Mi flujo

1. Mapeo de contenido: directorios, ficheros, vhosts.
2. Descubrimiento de endpoints y parámetros (incluye análisis de JS).
3. Identificación de APIs (REST/GraphQL) y su esquema.
4. Roles y flujos de autenticación/sesión.
5. Puntos de entrada de datos → candidatos a inyección.

## No dejarse sin mirar

- `robots.txt`, `sitemap.xml`, ficheros `.js`, comentarios en HTML.
- Cabeceras de respuesta y cookies (flags, tecnología).
- Endpoints de API y documentación (swagger/openapi).
- Parámetros ocultos y funciones no enlazadas desde la UI.
