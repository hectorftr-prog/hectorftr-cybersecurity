# Análisis de Incidente de Red — Caso Yummy Recipes

## Contexto

Ejercicio práctico del **Google Cybersecurity Professional Certificate** (curso "Connect and Protect: Networks and Network Security"). Los clientes de una empresa cliente reportaron no poder acceder a su sitio web (www.yummyrecipesforme.com), recibiendo el error "puerto de destino inalcanzable".

## Objetivo

Analizar el tráfico de red capturado con tcpdump para identificar qué protocolo y servicio se vieron afectados, determinar la causa raíz probable, y proponer una solución.

## Metodología

Se analizó el log de tcpdump, examinando las direcciones IP de origen/destino, protocolos (UDP, ICMP) y puertos implicados en la comunicación fallida.

## Hallazgos

El registro mostró que el cliente (192.51.100.15) envió una consulta DNS por **UDP** al servidor DNS (203.0.113.2), solicitando la resolución del dominio. En lugar de recibir la IP, el cliente recibió un mensaje de error **ICMP**: *"udp port 53 unreachable"*, repetido en tres intentos.

Esto confirma que el servicio DNS no estaba respondiendo en el puerto 53, impidiendo resolver la IP del dominio y bloqueando cualquier conexión posterior con el servidor web.

## Causa probable

El log no especifica la causa raíz exacta, pero el patrón del error sugiere que ningún servicio estaba escuchando en el puerto 53 del servidor DNS. Posibles causas:
- El servicio DNS estaba detenido
- Configuración incorrecta del servicio tras un cambio reciente
- Una regla de firewall bloqueando el tráfico UDP entrante en el puerto 53

## Solución propuesta

1. Verificar si el servicio DNS está en ejecución; reiniciarlo si está detenido
2. Revisar la configuración del servicio para confirmar que está vinculado correctamente al puerto 53
3. Comprobar las reglas de firewall para descartar bloqueo del tráfico UDP en el puerto 53
4. Repetir la prueba de resolución DNS para confirmar la solución antes de notificar a los clientes afectados

## Reflexión personal

Este ejercicio me permitió profundizar en cómo se diagnostican fallos de red analizando tráfico real, distinguiendo claramente entre los hechos confirmados por los datos y las hipótesis razonadas sobre la causa — una distinción clave en cualquier análisis de ciberseguridad.
