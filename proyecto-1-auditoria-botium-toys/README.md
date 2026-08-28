# Auditoría de Seguridad — Caso Botium Toys

## Contexto

Ejercicio práctico del **Google Cybersecurity Professional Certificate** (curso "Play It Safe: Manage Security Risks"). Botium Toys es una empresa ficticia de venta de juguetes (física y online) que necesita una auditoría interna de TI para identificar riesgos y verificar cumplimiento normativo.

## Objetivo

Evaluar los activos y controles de seguridad existentes en Botium Toys, comparar la situación actual contra marcos de cumplimiento normativo (PCI DSS, GDPR, SOC), y proponer recomendaciones priorizadas por nivel de riesgo.

## Metodología

Se utilizó el marco **NIST CSF** (Cybersecurity Framework) como referencia, clasificando los hallazgos según:
- **Categoría de control**: administrativo, técnico o físico
- **Tipo de control**: preventivo, detectivo, correctivo o disuasorio

## Resultado de la evaluación de riesgo

**Puntuación de riesgo: 8/10** (alto), debido a la falta de controles críticos y a un cumplimiento normativo incompleto.

## Principales hallazgos

### ✅ Controles ya implementados
- Firewall configurado con reglas de seguridad
- Software antivirus activo y monitorizado
- Seguridad física adecuada (cerraduras, CCTV, detección de incendios)
- Plan de notificación de brechas de datos a clientes UE en 72h (GDPR)

### ❌ Controles ausentes o insuficientes
- Sin cifrado de datos de tarjetas de crédito (incumplimiento PCI DSS)
- Sin principio de mínimo privilegio ni separación de funciones
- Sin sistema de detección de intrusos (IDS)
- Sin plan de recuperación ante desastres ni copias de seguridad
- Sin sistema centralizado de gestión de contraseñas

## Recomendaciones (priorizadas por riesgo)

**Prioridad crítica:**
1. Implementar cifrado de datos de tarjetas y datos sensibles de clientes (PCI DSS)
2. Establecer políticas de mínimo privilegio y separación de funciones
3. Desarrollar un plan de recuperación ante desastres con copias de seguridad regulares

**Prioridad alta:**
4. Desplegar un sistema de detección de intrusos (IDS)
5. Implementar gestión centralizada de contraseñas y reforzar la política actual

**Prioridad media:**
6. Establecer un calendario formal de mantenimiento para sistemas legacy
7. Clasificar e inventariar correctamente todos los activos de datos

## Reflexión personal

Este ejercicio conecta directamente con mi experiencia previa en gestión de riesgo y cumplimiento normativo en banca y asesoría financiera: el proceso de auditar una situación contra un marco de referencia y priorizar recomendaciones de mitigación es una habilidad transferible que aplico ahora al ámbito de la ciberseguridad.
