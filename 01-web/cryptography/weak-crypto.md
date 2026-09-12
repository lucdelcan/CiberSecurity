# Weak Cryptography

- **WSTG:** `WSTG-CRYP-*`
- **OWASP Top 10:** `A02:2021 – Cryptographic Failures`
- **Alias:** fallos criptográficos

## Qué es

Uso de criptografía débil o mal aplicada: protocolos/cifrados obsoletos, datos sensibles sin cifrar, o implementaciones vulnerables (padding oracle, ECB, claves embebidas).

## Vectores frecuentes

- **TLS débil:** versiones antiguas (SSLv3, TLS 1.0/1.1), suites inseguras, certificados inválidos.
- **Datos sensibles sin cifrar** en tránsito (HTTP) o en reposo.
- **Padding oracle:** descifrar/forjar datos aprovechando mensajes de error de padding.
- **Cifrado débil:** ECB (patrones visibles), claves/IV embebidos, hashing sin salt para contraseñas.

## Cómo detectarla

- Escanea TLS (protocolos y suites) y revisa certificados.
- Comprueba si datos sensibles viajan por canales sin cifrar.
- Analiza tokens/blobs cifrados: reutilización de patrones (ECB), maleabilidad, errores de padding.

## Impacto

Exposición de datos sensibles, suplantación, manipulación de datos cifrados.

## Cómo remediar

- TLS moderno (1.2+/1.3) con suites fuertes; HSTS.
- Cifrado autenticado (AES-GCM), IV aleatorios, gestión de claves adecuada.
- Hashing de contraseñas con algoritmos lentos y salt (bcrypt/argon2).

## Referencias

- OWASP WSTG `WSTG-CRYP-*` · CWE-327 / CWE-326

## Enlaces internos

- Checklist: `../../00-metodologia/06-checklists/09-cryptography.md`
- Redacción para informe: `../../00-metodologia/05-informe/catalogo-redacciones.md`
