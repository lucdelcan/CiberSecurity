# REST API Attacks

- **WSTG:** `WSTG-APIT` + categorías generales
- **OWASP:** OWASP API Security Top 10 (2023)
- **Alias:** ataques a APIs REST

## Qué es

Las APIs REST concentran los riesgos del OWASP API Top 10. Los más recurrentes son fallos de autorización a nivel de objeto y de función, que permiten acceder a datos o acciones de otros.

## Vectores clave (API Top 10)

- **BOLA** (Broken Object Level Authorization): IDOR en endpoints de API — el más común.
- **Broken Authentication:** tokens/JWT mal validados.
- **BOPLA:** exposición o asignación masiva de propiedades del objeto (mass assignment).
- **Unrestricted Resource Consumption:** falta de rate limiting → DoS/coste.
- **Broken Function Level Authorization:** acceder a funciones de admin cambiando método/ruta.

## Cómo detectarla

- Consigue la documentación/colección (swagger/openapi, Postman) — ver `../../00-metodologia/02-enumeration/`.
- Con dos cuentas/roles, prueba acceso cruzado a objetos (BOLA) y a funciones de mayor privilegio.
- Prueba métodos no documentados (PUT/DELETE), parámetros extra (mass assignment) y ausencia de rate limiting.

## Impacto

Acceso/modificación no autorizada de datos, escalada de privilegios, DoS.

## Cómo remediar

- Autorización a nivel de objeto y de función en **cada** endpoint.
- Validar y limitar los campos aceptados (evitar mass assignment).
- Rate limiting y cuotas.
- Autenticación robusta y esquema de API documentado y controlado.

## Referencias

- OWASP API Security Top 10 (2023) · CWE-285

## Enlaces internos

- Checklist: `../../00-metodologia/06-checklists/12-api.md`
- Redacción para informe: `../../00-metodologia/05-informe/catalogo-redacciones.md`
