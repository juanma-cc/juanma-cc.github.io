
## 1. 🖥️ La Carpeta `Windows` y Variables de Entorno

La carpeta `C:\Windows` contiene los archivos del sistema operativo Windows, aunque puede estar ubicada en cualquier unidad o directorio.

- ✅ Variable de entorno clave: `%windir%`
- 📘 Según Microsoft: *"Las variables de entorno almacenan información sobre el entorno del sistema operativo, como la ruta del sistema, número de procesadores y ubicaciones de carpetas temporales."*

---

## 2. 📂 La Carpeta `System32`

Es una de las carpetas más importantes dentro de `Windows`.

- 🔧 Contiene archivos críticos para el funcionamiento del sistema.
- ⚠️ ¡Precaución! Eliminar archivos aquí puede dejar el sistema inoperable.
- 🛠️ Muchas herramientas usadas en sistemas Windows están ubicadas en esta carpeta.

---

## 3. 👤 Tipos de Cuentas de Usuario

En Windows local existen dos tipos principales de usuarios:

| Tipo de Cuenta | Permisos |
|----------------|----------|
| **Administrador** | Puede hacer cambios en el sistema: crear usuarios, modificar configuraciones, etc. |
| **Usuario Estándar** | Solo puede modificar sus propios archivos y no realizar cambios globales. |

### 📍 Cómo Verificar Usuarios Existentes

1. Abrir el **Menú Inicio**
2. Escribir **"Otro usuario"**
3. Acceder a **Configuración > Otros usuarios**

Solo los Administradores pueden ver y usar la opción **"Agregar otra persona a este equipo"**.

---

## 4. 🧾 Perfiles de Usuario

Al crear un nuevo usuario, Windows genera automáticamente su perfil en:

```
C:\Users\<NombreDeUsuario>
```

Ejemplo:

```bash
C:\Users\Max
```

El perfil se crea al primer inicio de sesión del usuario. Durante este proceso, aparece el mensaje **"User Profile Service"** en pantalla.

### 📁 Carpetas Comunes en un Perfil de Usuario

- Desktop
- Documents
- Downloads
- Music
- Pictures

---

## 5. 👥 Gestión Local de Usuarios y Grupos (`lusrmgr.msc`)

Acceso rápido mediante **Ejecutar (Run)**:

```bash
lusrmgr.msc
```

Este panel permite gestionar:
- **Usuarios**
- **Grupos**

Los usuarios heredan permisos según los grupos a los que pertenecen. Un usuario puede pertenecer a múltiples grupos.

---

## 6. ⚙️ Utilidad de Configuración del Sistema (`MSConfig`)

Herramienta avanzada para diagnosticar problemas de arranque.

### 📍 Cómo Abrirla

- Menú Inicio → Ejecutar → `msconfig`

### 📋 Pestañas Principales

1. **General**: Modo de inicio (Normal, Diagnóstico o Selectivo)
2. **Arranque (Boot)**: Opciones de carga del SO
3. **Servicios (Services)**: Lista de servicios del sistema
4. **Inicio (Startup)**: Elementos que inician con el sistema
5. **Herramientas (Tools)**: Herramientas adicionales del sistema

> ⚠️ Requiere permisos de administrador para ejecutarse.

---

## 7. 🧰 Computer Management (`compmgmt.msc`)

Herramienta centralizada para gestionar componentes del sistema.

### 🧩 Secciones Principales

- **Herramientas del Sistema**
  - Programador de Tareas (Task Scheduler)
  - Visor de Eventos (Event Viewer)
  - Carpetas Compartidas (Shared Folders)
  - Usuarios y Grupos Locales (Local Users and Groups)
  - Monitor de Rendimiento (Performance Monitor)
  - Administrador de Dispositivos (Device Manager)

- **Almacenamiento (Storage)**
  - Administración de Discos (Disk Management)

- **Servicios y Aplicaciones**
  - Servicios del sistema
  - WMI Control

---

## 8. 📝 Introducción al Símbolo del Sistema (`cmd`)

Interfaz de línea de comandos para interactuar con el sistema.

### 🔍 Comandos Básicos

```cmd
hostname        :: Muestra el nombre del equipo
whoami          :: Muestra el nombre del usuario actual
ipconfig        :: Muestra información de red
ipconfig /?
cls             :: Limpia la pantalla
netstat         :: Muestra conexiones de red activas
```

### 💡 Ayuda de Comandos

Usa `/?` para ver ayuda:

```cmd
ipconfig /?
```

Para comandos `net`, usa:

```cmd
net help
net help user
```

---

## 9. 📚 Recursos Adicionales

- 📄 [Documentación Oficial de MSConfig](https://docs.microsoft.com/)
- 📁 [Lista Completa de Comandos CMD](https://ss64.com/nt/)
- 🛡️ [WMIC vs PowerShell](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.management/get-service?view=powershell-7.3)
