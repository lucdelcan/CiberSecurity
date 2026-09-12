# WSTG-BUSL · Business Logic

La que no detecta un scanner: requiere entender el negocio de la app.

- [ ] `WSTG-BUSL-01` **Business Logic Data Validation** — Enviar valores imposibles/incoherentes según la lógica (cantidades negativas, etc.).
- [ ] `WSTG-BUSL-02` **Ability to Forge Requests** — Forjar peticiones que la interfaz no permite hacer.
- [ ] `WSTG-BUSL-03` **Integrity Checks** — Manipular datos que deberían ser inmutables (precios, roles decididos en cliente).
- [ ] `WSTG-BUSL-04` **Process Timing** — Abusar de los tiempos del proceso (race conditions, deducir info por tiempos).
- [ ] `WSTG-BUSL-05` **Function Usage Limits** — Usar una función más veces de lo permitido (cupones, votos, reintentos).
- [ ] `WSTG-BUSL-06` **Circumvention of Workflows** — Saltarse el orden obligatorio de pasos de un flujo.
- [ ] `WSTG-BUSL-07` **Defenses Against Misuse** — Ver si la app detecta y reacciona ante un uso abusivo.
- [ ] `WSTG-BUSL-08` **Upload of Unexpected File Types** — Subir tipos de fichero no previstos por la app.
- [ ] `WSTG-BUSL-09` **Upload of Malicious Files** — Subir ficheros maliciosos (webshell, malware).
