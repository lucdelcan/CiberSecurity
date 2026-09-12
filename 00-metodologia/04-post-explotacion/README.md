# Post-explotación

Qué hacer una vez conseguido acceso, **siempre dentro del alcance y las reglas del engagement**.

## Mi flujo

1. Recolección de evidencias (capturas, IDs, pruebas mínimas suficientes).
2. Evaluar alcance del compromiso: a qué datos/funciones da acceso.
3. Escalada de privilegios (a alto nivel; el detalle técnico va en `02-infra-redes/`).
4. Movimiento lateral, si está en alcance.
5. Limpieza: no dejar artefactos, no persistir.

## Reglas (pentest real)

- No exfiltrar datos reales de clientes/usuarios.
- No dejar persistencia ni cuentas backdoor.
- Documentar toda acción para poder revertirla y reportarla.
