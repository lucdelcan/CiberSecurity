# WSTG-AUTHN · Authentication

- [ ] `WSTG-AUTHN-01` **Credentials over Encrypted Channel** — Que las credenciales viajen por HTTPS, nunca en claro.
- [ ] `WSTG-AUTHN-02` **Default Credentials** — Probar credenciales por defecto (admin/admin, del fabricante).
- [ ] `WSTG-AUTHN-03` **Weak Lock Out** — Comprobar si hay bloqueo tras varios intentos fallidos (anti fuerza bruta).
- [ ] `WSTG-AUTHN-04` **Bypass Authentication** — Intentar saltarse el login (acceso directo a rutas, manipular parámetros).
- [ ] `WSTG-AUTHN-05` **Vulnerable Remember Password** — Revisar el "recuérdame": tokens/cookies persistentes inseguras.
- [ ] `WSTG-AUTHN-06` **Browser Cache Weaknesses** — Que datos sensibles no queden cacheados en el navegador.
- [ ] `WSTG-AUTHN-07` **Weak Password Policy** — Política de contraseñas débil (longitud, complejidad, reutilización).
- [ ] `WSTG-AUTHN-08` **Weak Security Question** — Preguntas de seguridad adivinables o con respuesta pública.
- [ ] `WSTG-AUTHN-09` **Weak Password Change/Reset** — Fallos en cambio/reset (tokens predecibles, sin verificar identidad).
- [ ] `WSTG-AUTHN-10` **Weaker Auth in Alternative Channel** — Que la app móvil/API no tenga autenticación más débil que la web.
