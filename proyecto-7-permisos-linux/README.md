# 🔐 Auditoría y Gestión de Permisos en Linux

## Caso práctico de seguridad | Research Team

---

## 📋 Contexto

Este proyecto documenta una auditoría básica de permisos en un entorno Linux basada en un escenario práctico de seguridad.

En una empresa ficticia, un equipo de investigación (`research team`) trabaja con archivos de proyecto, documentación confidencial y directorios restringidos. Durante la revisión se identificaron configuraciones de permisos que no respetaban adecuadamente el **Principio de Mínimo Privilegio (PoLP)**.

El objetivo de la auditoría es identificar permisos excesivos, evaluar el riesgo asociado y aplicar medidas de remediación mediante herramientas estándar de Linux.

---

# 🎯 Objetivo

Evaluar y corregir permisos de archivos y directorios utilizando la línea de comandos de Linux para:

- Identificar permisos excesivos.
- Reducir accesos no autorizados.
- Aplicar el Principio de Mínimo Privilegio.
- Proteger archivos confidenciales.
- Restringir el acceso a directorios sensibles.
- Verificar los cambios realizados después de la remediación.

---

# 🛠️ Herramientas utilizadas

### Sistema operativo

Linux

### Línea de comandos (CLI)

Utilizada para inspeccionar archivos, directorios y permisos.

### `ls -la`

Utilizado para visualizar:

- Archivos normales.
- Archivos ocultos.
- Directorios.
- Propietarios.
- Grupos.
- Permisos configurados.

### `chmod`

Utilizado para modificar permisos de:

- Usuario propietario.
- Grupo.
- Otros usuarios.

---

# 🧠 Conceptos de seguridad aplicados

## Principle of Least Privilege (PoLP)

El Principio de Mínimo Privilegio establece que los usuarios, grupos y procesos deben disponer únicamente de los permisos necesarios para realizar sus funciones.

La aplicación de este principio ayuda a reducir:

- Modificaciones no autorizadas.
- Exposición de información confidencial.
- Accesos innecesarios.
- Impacto potencial de cuentas comprometidas.

---

## Linux Discretionary Access Control (DAC)

Linux utiliza un modelo de control de acceso basado en permisos asociados a:

- Propietario.
- Grupo.
- Otros usuarios.

Los permisos básicos son:

| Permiso | Valor | Descripción |
|---|---:|---|
| `r` | 4 | Lectura |
| `w` | 2 | Escritura |
| `x` | 1 | Ejecución o acceso a directorios |

Los permisos pueden representarse mediante:

### Notación simbólica

```text
rwx
```

### Notación octal

```text
700
640
440
755
```

---

# 🔍 Fase 1 — Inspección inicial

La primera fase consiste en identificar los permisos actuales de los recursos.

Comando utilizado:

```bash
ls -la
```

Este comando permite visualizar tanto archivos normales como archivos ocultos.

Ejemplo:

```text
-rw-rw-rw- project_k.txt
-rw-r----- project_x.txt
drwxr-x--- drafts/
```

---

# ⚠️ Hallazgos de seguridad

Durante la revisión se identificaron configuraciones que requerían atención.

---

## 🔴 Hallazgo 1 — Permisos de escritura excesivos

### Archivo

```text
project_k.txt
```

### Riesgo

El archivo permitía permisos de escritura excesivos para usuarios que no necesitaban modificarlo.

Esto puede aumentar el riesgo de:

- Modificación accidental.
- Alteración no autorizada.
- Manipulación de información.
- Pérdida de integridad del contenido.

### Remediación

Se eliminó el permiso de escritura para la categoría `others`.

```bash
chmod o-w project_k.txt
```

### Resultado esperado

Los usuarios fuera del propietario y grupo autorizado ya no pueden modificar el archivo.

---

# 🔴 Hallazgo 2 — Archivo confidencial con permisos excesivos

### Archivo

```text
project_x.txt
```

Este archivo contiene información que requiere acceso restringido.

### Objetivo

Permitir únicamente lectura al:

- Propietario.
- Grupo autorizado.

Y eliminar cualquier acceso para:

- Otros usuarios.

### Remediación

```bash
chmod 440 project_x.txt
```

### Resultado

```text
-r--r----- project_x.txt
```

### Explicación

| Categoría | Permisos |
|---|---|
| Propietario | Lectura |
| Grupo | Lectura |
| Otros | Sin acceso |

### Nota técnica

El permiso `440` **no convierte un archivo en inmutable**.

`chmod` controla permisos de acceso, pero no impide necesariamente todas las modificaciones posibles por usuarios privilegiados o procesos con permisos elevados.

Para implementar controles adicionales de inmutabilidad en sistemas Linux compatibles pueden utilizarse mecanismos específicos como atributos de archivo.

---

# 📁 Hallazgo 3 — Directorio con acceso excesivo

### Directorio

```text
drafts/
```

Los directorios requieren especial atención porque sus permisos controlan:

- Visualización de contenido.
- Acceso a archivos internos.
- Creación de archivos.
- Eliminación de archivos.
- Navegación dentro del directorio.

---

## Permisos en directorios

En un directorio, los permisos tienen un comportamiento específico.

| Permiso | Función |
|---|---|
| `r` | Permite listar el contenido |
| `w` | Permite crear, modificar o eliminar entradas |
| `x` | Permite acceder o atravesar el directorio |

---

## Remediación

Para restringir el acceso únicamente al propietario:

```bash
chmod 700 drafts
```

### Resultado

```text
drwx------ drafts
```

### Explicación

| Categoría | Permisos |
|---|---|
| Propietario | Lectura, escritura y acceso |
| Grupo | Sin acceso |
| Otros | Sin acceso |

---

# 👁️ Fase 2 — Comprobación de archivos ocultos

Los archivos ocultos en Linux comienzan normalmente con un punto (`.`).

Ejemplo:

```text
.config
.hidden_file
```

Para identificarlos se utilizó:

```bash
ls -la
```

---

## Riesgo de seguridad

Los archivos ocultos pueden contener:

- Configuraciones.
- Datos temporales.
- Información de aplicaciones.
- Archivos sensibles.
- Scripts.

Por este motivo, una auditoría de permisos no debe limitarse únicamente a los archivos visibles.

---

# 🔐 Fase 3 — Verificación posterior

Después de aplicar los cambios se debe volver a comprobar la configuración.

Comando:

```bash
ls -la
```

El objetivo es confirmar que los permisos configurados coinciden con la política de acceso prevista.

---

# 📊 Resumen de remediaciones

| Recurso | Problema | Acción | Resultado |
|---|---|---|---|
| `project_k.txt` | Escritura excesiva | `chmod o-w` | Se elimina escritura para otros |
| `project_x.txt` | Acceso excesivo | `chmod 440` | Lectura limitada a propietario y grupo |
| `drafts/` | Directorio demasiado accesible | `chmod 700` | Acceso limitado al propietario |

---

# 🛡️ Recomendaciones de seguridad

## Prioridad alta

### 1. Revisar permisos excesivos

Evitar permisos innecesarios de escritura, especialmente para:

```text
others
```

El acceso de escritura debe concederse únicamente cuando exista una necesidad operativa.

---

### 2. Proteger información confidencial

Los archivos sensibles deben utilizar permisos restrictivos acordes a:

- Clasificación de la información.
- Necesidad de acceso.
- Usuarios autorizados.
- Grupos de trabajo.

---

### 3. Restringir directorios sensibles

Los directorios que contienen información confidencial deben limitar el acceso a los usuarios y grupos necesarios.

---

## Prioridad media

### 4. Realizar auditorías periódicas

Los permisos pueden cambiar con el tiempo debido a:

- Nuevos usuarios.
- Cambios en grupos.
- Instalación de aplicaciones.
- Scripts.
- Automatizaciones.
- Cambios manuales.

Se recomienda revisar periódicamente:

```bash
ls -la
```

Y analizar recursos especialmente sensibles.

---

### 5. Aplicar permisos por defecto adecuados

El uso de políticas adecuadas de permisos por defecto puede reducir la creación de archivos con permisos demasiado permisivos.

Es recomendable revisar configuraciones como:

```text
umask
```

De acuerdo con los requisitos del entorno.

---

### 6. Automatizar controles cuando sea necesario

En entornos corporativos puede ser útil automatizar la detección de configuraciones incorrectas mediante:

- Scripts.
- Auditorías programadas.
- Herramientas de configuración.
- Monitorización de cambios.
- Sistemas de gestión de configuración.

---

# 🔄 Metodología aplicada

El proceso seguido en esta auditoría fue:

```text
IDENTIFICAR
    ↓
ANALIZAR
    ↓
EVALUAR EL RIESGO
    ↓
APLICAR REMEDIACIÓN
    ↓
VERIFICAR RESULTADOS
    ↓
DOCUMENTAR
```

---

# 🧩 Escenario de riesgo

Un permiso incorrecto puede parecer un problema menor.

Por ejemplo:

```text
-rw-rw-rw-
```

Sin embargo, si el archivo contiene información importante, múltiples usuarios pueden tener capacidad para modificarlo.

Aplicando permisos más restrictivos:

```text
-rw-r-----
```

O:

```text
-r--r-----
```

Se reduce la superficie de exposición.

La configuración adecuada depende siempre del contexto operativo y de quién necesita realmente acceder al recurso.

---

# 🧠 Aprendizajes obtenidos

Este proyecto permitió reforzar conocimientos sobre:

- Permisos Linux.
- Notación simbólica.
- Notación octal.
- Propietario de archivos.
- Grupos.
- Otros usuarios.
- Archivos ocultos.
- Directorios.
- Control de acceso.
- Principle of Least Privilege.
- Security Hardening.
- Auditoría básica de permisos.
- Remediación de configuraciones inseguras.

---

# ⚠️ Limitaciones

Este ejercicio se centra en permisos tradicionales de Linux mediante DAC.

Una auditoría de seguridad completa en un entorno empresarial también debería considerar:

- ACLs.
- Gestión de usuarios y grupos.
- Privilegios `sudo`.
- SELinux o AppArmor cuando estén implementados.
- Propiedad de archivos.
- Servicios en ejecución.
- Procesos.
- Logs.
- Monitorización de cambios.
- Políticas corporativas.
- Gestión de identidades y accesos (IAM).

---

# 🚀 Próximas mejoras

Como evolución de este proyecto se podrían implementar:

### 🔹 Auditoría automatizada

Crear un script Bash que identifique:

- Archivos con permisos `777`.
- Directorios excesivamente abiertos.
- Archivos world-writable.
- Archivos sensibles con permisos incorrectos.

---

### 🔹 Registro de resultados

Generar informes de auditoría mediante:

```bash
ls -la
find
stat
```

---

### 🔹 Monitorización

Detectar cambios en archivos sensibles mediante herramientas de monitorización y auditoría.

---

### 🔹 Laboratorio empresarial

Implementar un entorno virtual con:

```text
Linux Server
        │
        ├── Usuarios
        ├── Grupos
        ├── Archivos confidenciales
        ├── Directorios compartidos
        ├── Logs
        └── Políticas de acceso
```

Para simular una infraestructura corporativa y realizar auditorías de seguridad más completas.

---

# 💼 Perspectiva profesional

La gestión de permisos no es únicamente una configuración técnica.

En un entorno empresarial, los controles de acceso forman parte de una estrategia más amplia de seguridad orientada a:

- Reducir riesgos.
- Limitar accesos innecesarios.
- Proteger información.
- Mantener la responsabilidad sobre los recursos.
- Minimizar el impacto de errores o cuentas comprometidas.

La combinación de conocimientos técnicos de Linux y una visión orientada a procesos, riesgos y control operativo es especialmente relevante para entornos de:

- Security Operations.
- IT Support.
- System Administration.
- Identity and Access Management.
- Governance, Risk and Compliance.
- Cybersecurity Operations.

---

# 🏁 Conclusión

La auditoría de permisos en Linux demuestra cómo una configuración aparentemente simple puede afectar directamente a la seguridad de un sistema.

Aplicando el **Principio de Mínimo Privilegio**, se pueden reducir accesos innecesarios y limitar la capacidad de modificación de recursos sensibles.

El proceso realizado en este proyecto ha consistido en:

```text
✔ Identificar permisos existentes
✔ Detectar configuraciones excesivas
✔ Evaluar riesgos
✔ Aplicar remediaciones
✔ Verificar los cambios
✔ Documentar recomendaciones
```

Este proyecto forma parte de mi portfolio práctico de ciberseguridad y de mi formación en administración de sistemas, seguridad Linux y gestión de controles de acceso.

---

## 🛠️ Tecnologías y herramientas

```text
Linux
Bash
CLI
chmod
ls
Security Auditing
Access Control
Principle of Least Privilege
```

---

**Proyecto desarrollado como parte de mi formación práctica en ciberseguridad.**
