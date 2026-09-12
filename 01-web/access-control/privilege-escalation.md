# Privilege Escalation (a nivel web)

- **WSTG:** `WSTG-AUTHZ-03`
- **OWASP Top 10:** `A01:2021 – Broken Access Control`
- **Alias:** escalada de privilegios horizontal/vertical

## Qué es

El usuario obtiene permisos que no le corresponden por fallos de control de acceso en la aplicación.

- **Horizontal:** accedes a recursos/acciones de **otro usuario del mismo nivel** (muy ligado a [idor.md](idor.md)).
- **Vertical:** subes a un **rol superior** (usuario → admin), accediendo a funciones administrativas.

## Cómo detectarla

- Mapea funciones por rol con **varias cuentas** (admin, usuario, sin autenticar).
- Prueba acceder a funciones de admin desde una cuenta normal:
  - Rutas directas: `/admin`, `/admin/users`, endpoints de gestión.
  - Cambiando método o parámetros: `role=admin`, `isAdmin=true`, `?debug=1`.
  - Reenviando peticiones de admin capturadas, pero con la sesión de usuario normal.
- **Forced browsing** a funciones no enlazadas para tu rol.
- **Mass assignment:** añadir campos no previstos (`"role":"admin"`) en un update de perfil.

## Cómo explotarla

1. Identifica una acción privilegiada.
2. Intenta invocarla con un rol insuficiente (control solo en el cliente/UI, no en servidor → vulnerable).
3. Confirma el efecto (creaste un usuario, cambiaste un rol, accediste a datos de gestión).

## Impacto

Acceso administrativo o a datos/acciones de otros → puede llevar a compromiso total de la aplicación. Alto/crítico.

## Cómo remediar

- Comprobar autorización **en servidor** en cada función y recurso, según el rol.
- Negar por defecto; no ocultar funciones solo en la UI.
- Controlar los campos aceptados (evitar mass assignment de `role`/permisos).

## Referencias

- OWASP WSTG `WSTG-AUTHZ-03` · CWE-269 · PortSwigger — Access control

## Enlaces internos

- Relacionada: [idor.md](idor.md) · Checklist: `../../00-metodologia/06-checklists/05-authorization.md`
- Redacción: `../../00-metodologia/05-informe/catalogo-redacciones.md`
