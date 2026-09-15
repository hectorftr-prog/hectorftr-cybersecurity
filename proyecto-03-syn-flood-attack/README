# Análisis de Incidente — Ataque SYN Flood

## Contexto

Ejercicio práctico del **Google Cybersecurity Professional Certificate** (curso "Connect and Protect: Networks and Network Security"). Una agencia de viajes reporta un problema de acceso a su sitio web: los usuarios reciben un error de "tiempo de espera de conexión agotado".

## Objetivo

Analizar el tráfico de red capturado para identificar el tipo de ataque, explicar su mecanismo técnico y su impacto en el servidor, y proponer medidas de mitigación.

## Metodología

Se analizaron los registros de tráfico de red (paquetes TCP), examinando el volumen y origen de las solicitudes, y su relación con el proceso de establecimiento de conexión TCP (three-way handshake).

## Hallazgos

Los registros mostraron un volumen anormalmente alto de solicitudes **TCP SYN** procedentes de una **única dirección IP**, sin los correspondientes paquetes ACK que completan el protocolo de enlace de tres vías (three-way handshake: SYN → SYN-ACK → ACK).

**Three-way handshake:**
1. **SYN** — el cliente solicita iniciar una conexión
2. **SYN-ACK** — el servidor confirma y solicita su propia sincronización
3. **ACK** — el cliente confirma, completando la conexión

Al no recibir nunca el ACK final, el servidor mantiene cada conexión como "semiabierta", reservando recursos que nunca se liberan. Con miles de solicitudes de este tipo, la tabla de conexiones del servidor se satura, impidiendo que atienda tráfico legítimo.

## Diagnóstico

**Tipo de ataque:** SYN flood — un ataque de **Denegación de Servicio (DoS)**, no DDoS, ya que el tráfico procedía de una única dirección IP en lugar de múltiples fuentes distribuidas.

## Consecuencias

Pérdida de ventas por indisponibilidad del sitio web, imposibilidad de que los empleados accedieran a información de productos para atender a clientes, y riesgo reputacional si el incidente se repite o se prolonga.

## Medidas de mitigación propuestas

- Implementar **SYN cookies** para evitar reservar recursos hasta verificar la conexión completa
- Configurar **rate limiting** por IP para detectar y limitar volúmenes de tráfico anómalos
- Desplegar un **WAF (Web Application Firewall)** o servicio de protección DDoS que filtre tráfico malicioso antes de que llegue al servidor

## Nota sobre IP spoofing

El escenario señala que el bloqueo de la IP atacante no sería una solución duradera, ya que un atacante puede falsificar (spoof) la dirección IP de origen en sus paquetes, evadiendo bloqueos basados únicamente en IP.

## Reflexión personal

Este ejercicio reforzó la importancia de distinguir con precisión entre tipos de ataque (DoS vs. DDoS) basándose en evidencia concreta del tráfico, y de entender el funcionamiento interno de protocolos como TCP para diagnosticar correctamente el impacto técnico de un incidente.
