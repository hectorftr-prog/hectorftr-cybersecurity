# Aplicar filtros SQL para el análisis de eventos de seguridad

## Objetivo

Practicar el uso de filtros SQL para analizar registros de autenticación y segmentar información de empleados durante una investigación de seguridad.

El ejercicio simula el trabajo de un analista de ciberseguridad que necesita identificar eventos potencialmente sospechosos y obtener rápidamente subconjuntos concretos de información a partir de una base de datos.

Se utilizan los operadores:

* `AND`
* `OR`
* `NOT`
* `LIKE`
* `=`
* `>`
* El comodín `%`

---

## 1. Identificar intentos de inicio de sesión fallidos fuera del horario laboral

### Consulta

```sql
SELECT *
FROM log_in_attempts
WHERE login_time > '18:00'
  AND success = FALSE;
```

### Análisis

La consulta combina dos condiciones mediante `AND`:

1. El intento de inicio de sesión se produjo después de las 18:00.
2. El intento terminó en fallo.

El objetivo es reducir el volumen de registros y localizar eventos que podrían requerir una revisión adicional.

Un intento aislado no demuestra por sí mismo una intrusión, pero varios intentos fallidos fuera del horario habitual pueden constituir una señal que merece investigación.

---

## 2. Analizar intentos de inicio de sesión correspondientes a determinadas fechas

### Consulta

```sql
SELECT *
FROM log_in_attempts
WHERE login_date = '2022-05-09'
   OR login_date = '2022-05-08';
```

### Análisis

El operador `OR` permite recuperar los registros correspondientes a cualquiera de las dos fechas.

Este tipo de consulta resulta útil cuando se investiga un incidente y se necesita comparar la actividad registrada durante el día del evento con la actividad inmediatamente anterior.

---

## 3. Excluir conexiones procedentes de México

### Consulta

```sql
SELECT *
FROM log_in_attempts
WHERE NOT country LIKE 'MEX%';
```

### Análisis

`LIKE` permite realizar una coincidencia basada en patrones.

El patrón `MEX%` permite localizar valores que comienzan por `MEX`, mientras que `NOT` invierte la condición y excluye esos registros.

Esta técnica puede resultar útil cuando existen pequeñas diferencias en la forma en que los datos están almacenados.

**Importante:** en un entorno real, antes de utilizar este filtro habría que comprobar los valores existentes en la columna `country`, ya que no se debe asumir que todas las variantes comienzan por `MEX`.

---

## 4. Localizar empleados de Marketing situados en el edificio Este

### Consulta

```sql
SELECT *
FROM employees
WHERE department = 'Marketing'
  AND office LIKE 'East%';
```

### Análisis

Se combinan dos filtros mediante `AND`:

* El empleado pertenece al departamento de Marketing.
* La ubicación comienza por `East`.

El uso de `LIKE 'East%'` permite obtener diferentes oficinas cuya denominación comienza por ese texto.

Este tipo de segmentación puede utilizarse para planificar tareas de mantenimiento, actualización o revisión de equipos.

---

## 5. Localizar empleados de Finanzas o Ventas

### Consulta

```sql
SELECT *
FROM employees
WHERE department = 'Finance'
   OR department = 'Sales';
```

### Análisis

El operador `OR` permite obtener registros que cumplan cualquiera de las dos condiciones.

La consulta devuelve los empleados pertenecientes a Finanzas o a Ventas.

Una alternativa equivalente, y más escalable cuando aumenta el número de departamentos, sería:

```sql
SELECT *
FROM employees
WHERE department IN ('Finance', 'Sales');
```

---

## 6. Excluir al departamento de Tecnología de la Información

### Consulta

```sql
SELECT *
FROM employees
WHERE NOT department = 'Information Technology';
```

### Análisis

El operador `NOT` permite excluir los registros correspondientes al departamento de Information Technology.

También puede escribirse de forma equivalente:

```sql
SELECT *
FROM employees
WHERE department <> 'Information Technology';
```

La segunda forma resulta especialmente habitual para expresar una comparación de desigualdad.

---

# Relación con ciberseguridad

Aunque las consultas utilizadas son sencillas, representan una competencia fundamental para un analista de seguridad: **saber extraer información relevante de grandes conjuntos de datos**.

En un entorno real, técnicas similares pueden utilizarse para:

* Analizar registros de autenticación.
* Detectar intentos de acceso fallidos.
* Investigar actividad fuera del horario habitual.
* Filtrar eventos por fecha.
* Identificar actividad procedente de determinadas ubicaciones.
* Preparar información para una investigación de incidentes.
* Reducir el volumen de datos que posteriormente debe analizar un profesional o una herramienta SIEM.

El filtrado SQL constituye, por tanto, una habilidad complementaria a otras competencias de ciberseguridad como el análisis de logs, detección de amenazas y respuesta ante incidentes.

# Conclusión

Este laboratorio demuestra el uso práctico de operadores SQL para transformar una consulta general sobre una base de datos en búsquedas específicas orientadas al análisis de seguridad.

La práctica también muestra una idea fundamental del trabajo de un analista: **no basta con disponer de datos; hay que saber filtrarlos, contextualizarlos y convertirlos en información útil para una investigación.**

## Tecnologías y conceptos

* SQL
* Análisis de logs
* Autenticación
* Detección de eventos sospechosos
* `SELECT`
* `WHERE`
* `AND`
* `OR`
* `NOT`
* `LIKE`
* `IN`
* Operadores de comparación
* Análisis defensivo
