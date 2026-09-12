# 04 · Post-explotación

Qué hacer una vez conseguido acceso, **siempre dentro del alcance y las reglas del engagement**. El detalle técnico de escalada (Linux/Windows/AD) vive en `02-infra-redes/`; aquí va el *proceso y el criterio*.

Regla de oro del pentest: el objetivo es **demostrar impacto**, no "hacer estragos". Todo lo que hagas debe poder revertirse y documentarse.

---

## 1. Situational awareness (¿dónde estoy?)

Antes de nada, entiende el terreno:

- **Quién soy:** usuario, privilegios, grupos.
- **Dónde estoy:** hostname, sistema operativo, si es contenedor/VM.
- **Qué alcanza esta máquina:** red interna, otros hosts, servicios internos, credenciales.
- **Qué datos toca:** a qué información/funcionalidad da acceso este compromiso.

---

## 2. Recolección de evidencias

Lo primero, capturar la prueba del acceso (mínima suficiente):

- Salida de `id`/`whoami`, `hostname`, y una captura del acceso conseguido.
- Marca de tiempo de cuándo se obtuvo.
- La cadena que llevó hasta aquí (enlaza con `03-explotacion/`).

---

## 3. Escalada de privilegios (alto nivel)

- Enumera vías de escalada (automatizado + manual).
- Confirma que **escalar está en alcance** antes de hacerlo.
- El *cómo* concreto → `02-infra-redes/linux-privesc/` y `windows-privesc/`.

---

## 4. Movimiento lateral (si está en alcance)

- Solo si el engagement lo contempla explícitamente.
- Reutilización de credenciales, pivoting hacia la red interna (detalle en `02-infra-redes/pivoting/`).
- Cada salto, documentado.

---

## 5. Evaluar el impacto / acceso a datos

Aquí es donde el finding gana severidad:

- ¿A qué datos sensibles se llega? (muestra acotada, **no** volcado masivo).
- ¿Se pueden tocar otras cuentas/tenants?
- ¿Da pie a comprometer más infraestructura?

---

## 6. Persistencia y limpieza

- **Persistencia:** en un pentest normal **NO** se deja (nada de backdoors, cuentas ni servicios). Solo si el engagement de red team lo pide y está autorizado.
- **Limpieza:** elimina lo que subiste (webshells, binarios, ficheros temporales), deja la máquina como estaba.
- Anota todo lo creado/modificado para que quede constancia y se pueda revertir.

---

## Reglas (recordatorio)

- No exfiltrar datos reales. No borrar ni modificar.
- No persistir salvo autorización expresa.
- Registrar cada acción con marca de tiempo.
- Ante cualquier duda de alcance, **parar y preguntar**.

## Entregable de la fase

- Evidencia del acceso y del nivel de privilegio alcanzado.
- Impacto real documentado (a qué se llega desde aquí).
- Lista de artefactos subidos y su limpieza confirmada.

## Referencias

- MITRE ATT&CK (tácticas de post-explotación: Discovery, Privilege Escalation, Lateral Movement).
- `02-infra-redes/` para el detalle técnico. Ver `../00-fundamentos/`.
