# Análisis de Incidente — Compromiso de Panel de Administración (Fuerza Bruta)

## Contexto

Ejercicio práctico del **Google Cybersecurity Professional Certificate** (curso "Connect and Protect: Networks and Network Security"). Un ex-empleado descontento comprometió el sitio web yummyrecipesforme.com mediante un ataque de fuerza bruta, insertando malware que redirigía a los visitantes a un sitio falso.

## Objetivo

Identificar los protocolos de red implicados en el incidente, documentar el evento de forma objetiva y detallada, y recomendar una medida de seguridad para prevenir ataques de fuerza bruta en el futuro.

## Protocolos identificados

El análisis del log de tcpdump identificó dos protocolos de la capa de aplicación del modelo TCP/IP:
- **DNS** — usado para resolver los dominios yummyrecipesforme.com y greatrecipesforme.com a sus direcciones IP
- **HTTP** (sin cifrado, no HTTPS) — usado para solicitar y cargar tanto la página legítima como la fraudulenta

## Documentación del incidente

Un ex-empleado obtuvo acceso no autorizado al panel de administración mediante un ataque de fuerza bruta, probando contraseñas por defecto conocidas hasta acertar. La cuenta nunca había cambiado su contraseña por defecto, y no existían controles para detectar o bloquear intentos repetidos de inicio de sesión.

Una vez dentro, el atacante insertó código JavaScript malicioso en el sitio, solicitando a los visitantes descargar un archivo. Tras el cambio, modificó la contraseña de administrador para bloquear el acceso al propietario legítimo.

Horas después, varios clientes reportaron al soporte que, tras descargar el archivo ofrecido por la web, eran redirigidos a otra dirección y sus equipos comenzaban a funcionar con lentitud. El propietario, incapaz de acceder al panel, contactó con el proveedor de hosting, iniciándose una investigación.

El equipo de ciberseguridad reprodujo el comportamiento en un entorno sandbox usando tcpdump, confirmando que el sitio redirigía a un dominio falso (greatrecipesforme.com) tras la descarga de un archivo con malware. Un analista senior confirmó el compromiso del código fuente y la inserción del script malicioso.

## Causa raíz

- Contraseña de administrador nunca cambiada del valor por defecto
- Ausencia de controles contra intentos repetidos de inicio de sesión (fuerza bruta)

## Recomendación

Implementar una **política de bloqueo de cuenta** tras un número limitado de intentos fallidos de inicio de sesión (por ejemplo, bloqueo tras 5 intentos durante un periodo determinado). Esta medida ataca directamente la causa raíz del incidente, eliminando la posibilidad de que un atacante pruebe contraseñas de forma ilimitada. Combinada con la exigencia de contraseñas robustas y no genéricas, reduce significativamente la viabilidad de ataques de fuerza bruta.

## Reflexión personal

Este ejercicio reforzó la importancia de separar la identificación técnica de protocolos (datos objetivos del log) de la documentación narrativa del incidente, así como de mantener un lenguaje neutro y basado en hechos al redactar informes de seguridad — una habilidad clave para la comunicación profesional en ciberseguridad.
