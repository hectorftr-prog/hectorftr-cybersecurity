# Evaluación y priorización de riesgos de seguridad

## Descripción de los factores de riesgo

La organización presenta una serie de factores que pueden aumentar su exposición a incidentes de seguridad. Entre ellos destacan el número de empleados, la existencia de personal remoto, la gestión de información financiera y de usuarios, la dependencia de terceros y su ubicación geográfica.

La presencia de empleados que trabajan de forma remota puede ampliar la superficie de ataque, especialmente frente a amenazas como el phishing, el robo de credenciales o el acceso no autorizado a recursos corporativos.

Además, la organización gestiona información financiera y datos asociados a usuarios, por lo que un incidente de seguridad podría afectar a la confidencialidad, integridad y disponibilidad de información sensible.

También debe considerarse la dependencia de proveedores y de la cadena de suministro. Una interrupción de servicios externos puede afectar a las operaciones de la organización incluso cuando sus propios sistemas no hayan sido comprometidos.

Por último, aunque el riesgo de incidentes físicos pueda ser menor que el de determinadas amenazas digitales, el acceso no autorizado o el robo de activos siguen siendo riesgos que deben contemplarse dentro del análisis general de seguridad.

---

## Metodología de evaluación

Para priorizar los riesgos se utiliza una matriz basada en dos variables:

* **Probabilidad:** posibilidad de que el riesgo llegue a materializarse.
* **Gravedad:** impacto potencial que tendría el incidente sobre la organización.

La puntuación se obtiene mediante:

**Riesgo = Probabilidad × Gravedad**

Se utiliza una escala de 1 a 3 para cada variable:

| Valor | Probabilidad | Gravedad |
| ----- | ------------ | -------- |
| **1** | Baja         | Baja     |
| **2** | Moderada     | Moderada |
| **3** | Alta         | Alta     |

La puntuación resultante permite establecer qué riesgos deberían recibir mayor atención y recursos.

---

## Registro y evaluación de riesgos

| Riesgo identificado                                                |     Probabilidad |         Gravedad | Puntuación | Justificación                                                                                                                                                                                                                                                                                                                       |
| ------------------------------------------------------------------ | ---------------: | ---------------: | ---------: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Compromiso del correo electrónico empresarial (BEC / phishing)** |     **3 - Alta** | **2 - Moderada** |      **6** | El correo electrónico constituye un vector habitual de ataques de ingeniería social. La existencia de empleados remotos puede incrementar las oportunidades de phishing y robo de credenciales. Un compromiso podría facilitar accesos no autorizados o fraudes, aunque el impacto concreto dependería de los controles existentes. |
| **Compromiso de la base de datos de usuarios**                     | **2 - Moderada** |     **3 - Alta** |      **6** | El acceso no autorizado a una base de datos que contiene información de usuarios podría comprometer datos confidenciales y afectar a la reputación y al cumplimiento de las obligaciones de protección de datos.                                                                                                                    |
| **Fuga de registros financieros**                                  | **2 - Moderada** |     **3 - Alta** |      **6** | La exposición de información financiera puede producir consecuencias económicas, legales y reputacionales importantes. Por ello, aunque la probabilidad se considere moderada, el impacto potencial es alto.                                                                                                                        |
| **Interrupción de la cadena de suministro**                        |     **1 - Baja** |     **3 - Alta** |      **3** | Una interrupción causada por un proveedor o por un acontecimiento que afecte a la cadena de suministro puede provocar problemas operativos importantes. Sin embargo, se considera menos probable que los ataques dirigidos directamente contra los sistemas o usuarios de la organización.                                          |
| **Robo o acceso físico no autorizado**                             |     **1 - Baja** | **2 - Moderada** |      **2** | El acceso físico no autorizado puede provocar pérdida o manipulación de equipos e información. Se considera menos probable que los principales riesgos digitales identificados, pero debe mantenerse dentro de las medidas generales de seguridad.                                                                                  |

---

# Priorización de los riesgos

La puntuación obtenida permite establecer tres niveles de prioridad:

### 🔴 Prioridad alta — Riesgo 6

#### 1. Compromiso del correo electrónico empresarial

El phishing y otras técnicas de ingeniería social pueden utilizarse para obtener credenciales, distribuir malware o conseguir que un empleado realice una acción no autorizada.

**Medidas recomendadas:**

* Implementar autenticación multifactor (MFA).
* Formar periódicamente a los empleados en detección de phishing.
* Aplicar políticas de contraseñas seguras.
* Supervisar los accesos y actividades anómalas.
* Establecer procedimientos para comunicar correos sospechosos.

#### 2. Compromiso de la base de datos de usuarios

La protección de las bases de datos debe centrarse en impedir accesos no autorizados y limitar el impacto de una posible intrusión.

**Medidas recomendadas:**

* Aplicar el principio de mínimo privilegio.
* Utilizar controles de acceso basados en roles.
* Cifrar información sensible.
* Supervisar los accesos a las bases de datos.
* Mantener sistemas y aplicaciones actualizados.
* Realizar copias de seguridad y comprobar periódicamente su recuperación.

#### 3. Fuga de registros financieros

La información financiera requiere controles destinados a proteger su confidencialidad e integridad.

**Medidas recomendadas:**

* Limitar el acceso únicamente al personal autorizado.
* Aplicar MFA a las cuentas con acceso a información sensible.
* Cifrar los datos tanto en almacenamiento como durante su transmisión.
* Registrar y monitorizar los accesos.
* Establecer procedimientos de respuesta ante incidentes.
* Revisar periódicamente los permisos de los usuarios.

---

### 🟠 Prioridad media — Riesgo 3

#### 4. Interrupción de la cadena de suministro

La organización debe considerar que un incidente en un proveedor puede afectar a sus propias operaciones.

**Medidas recomendadas:**

* Identificar proveedores críticos.
* Evaluar los riesgos asociados a terceros.
* Establecer planes de continuidad de negocio.
* Mantener procedimientos alternativos para servicios esenciales.
* Revisar periódicamente los requisitos de seguridad de los proveedores.

---

### 🟢 Prioridad baja — Riesgo 2

#### 5. Robo o acceso físico no autorizado

Aunque presenta una puntuación inferior, no debe ignorarse porque puede afectar directamente a los equipos y a la información almacenada en ellos.

**Medidas recomendadas:**

* Mantener controles de acceso físico.
* Restringir el acceso a zonas sensibles.
* Proteger físicamente los equipos.
* Utilizar mecanismos de bloqueo y autenticación.
* Revisar periódicamente las medidas de seguridad física.

---

# Matriz de priorización

|                               | **Gravedad 1 - Baja** | **Gravedad 2 - Moderada** | **Gravedad 3 - Alta**                            |
| ----------------------------- | --------------------- | ------------------------- | ------------------------------------------------ |
| **Probabilidad 3 - Alta**     | 3                     | 🔴 **6 - BEC**            | 9                                                |
| **Probabilidad 2 - Moderada** | 2                     | 4                         | 🔴 **6 - Base de datos / Registros financieros** |
| **Probabilidad 1 - Baja**     | 1                     | 🟢 **2 - Robo físico**    | 🟠 **3 - Cadena de suministro**                  |

---

# Conclusión

El análisis muestra que los riesgos relacionados con el **correo electrónico, las bases de datos de usuarios y la información financiera** deben recibir la mayor prioridad debido a la combinación de probabilidad e impacto potencial.

La estrategia de seguridad debería centrarse inicialmente en reducir la probabilidad de compromiso mediante controles de acceso, MFA, formación frente al phishing, gestión de privilegios y monitorización.

Al mismo tiempo, la organización debería mantener medidas de continuidad y protección frente a riesgos de terceros y amenazas físicas.

Este análisis demuestra la importancia de **identificar, evaluar y priorizar los riesgos antes de asignar recursos de seguridad**, permitiendo concentrar los esfuerzos en aquellas amenazas que pueden producir un mayor impacto sobre la organización.
