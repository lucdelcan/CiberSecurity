# XSS Almacenado (Stored)

- **WSTG:** `WSTG-INPV-02`
- **OWASP Top 10:** `A03:2021 – Injection`
- Ver índice: [xss.md](xss.md)

## Qué es

El payload se **guarda en el servidor** (comentario, nombre de perfil, mensaje, ticket, log visible en un panel) y se ejecuta **a todo usuario que vea ese contenido**, sin que tenga que hacer nada. Es el más grave: no requiere engañar a la víctima y puede afectar a muchos usuarios o a administradores.

## Cómo detectarla

1. Identifica todo campo cuya entrada se **almacena y luego se muestra**: perfiles, comentarios, mensajes, nombres de fichero, campos que ve un admin.
2. Inyecta un marcador único y localiza **dónde** se renderiza después (puede ser en otra página o en otro rol, p. ej. el panel de soporte).
3. Comprueba si se codifica al mostrarlo; si no, adapta el payload al contexto de salida.

Ojo a los **XSS "ciegos"** (blind): el payload se ejecuta en un panel interno que tú no ves. Usa un payload que llame a tu servidor (Burp Collaborator / callback) para detectarlos.

## Cómo explotarla

1. Almacena un payload adaptado al contexto donde se renderiza.
2. Espera a que lo cargue la víctima (o el administrador).
3. Impacto: robo de sesión de otros usuarios/admins, acciones masivas, propagación (XSS que se auto-replica = "gusano").

## Impacto

El mayor de los XSS: afecta a otros sin interacción y puede alcanzar a administradores → escalada hacia compromiso de la aplicación. Suele puntuar alto.

## Cómo remediar

- Codificar la salida **en cada lugar** donde se muestre el dato almacenado (incluidos paneles internos).
- Sanitizar en servidor el contenido rico (DOMPurify del lado servidor o equivalente) cuando se permita HTML.
- CSP y `HttpOnly`.

## Referencias

- OWASP WSTG `WSTG-INPV-02` · CWE-79 · PortSwigger — Stored XSS
