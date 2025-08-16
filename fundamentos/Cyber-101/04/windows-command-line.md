## 1. 🖥️ Introducción a la Línea de Comandos en Windows

La línea de comandos (`CMD`) es una herramienta fundamental para interactuar con el sistema operativo Windows desde una interfaz de texto. Aunque la GUI (interfaz gráfica) facilita muchas tareas, la terminal permite realizar operaciones avanzadas de forma rápida y precisa.

> 💡 La terminal puede accederse mediante:

- **Inicio → Ejecutar → cmd**
- **Teclas de atajo**: `Win + R` → `cmd`
- **Desde PowerShell**: `cmd`

---

## 2. 🌐 Información Básica del Sistema

Antes de ejecutar comandos, es útil conocer el entorno actual del sistema. El comando `set` muestra variables de entorno como la ruta del sistema, nombre de usuario, número de procesadores, etc.

### Ejemplo

```cmd
C:\> set
ALLUSERSPROFILE=C:\ProgramData
LOGNAME=strategos
NUMBER_OF_PROCESSORS=2
OS=Windows_NT
```

---

## 3. 📂 Navegación por el Sistema de Archivos

Los comandos básicos de navegación son fundamentales para explorar y manipular archivos y directorios.

### 3.1 `dir` – Listar Contenido de Directorio

Muestra los archivos y subdirectorios dentro de una carpeta.

#### Opciones útiles

- `/a`: Muestra archivos ocultos y de sistema.
- `/s`: Incluye subdirectorios recursivamente.

#### Ejemplo

```cmd
C:\example> dir
 Directory of C:\example
05/02/2024  07:36 AM    <DIR>          .
05/02/2024  07:36 AM    <DIR>          ..
05/02/2024  07:36 AM    <DIR>          backup_files
```

---

## 4. 🧱 Estructura de Directorios

El comando `tree` permite visualizar la estructura jerárquica de carpetas de manera gráfica.

#### Ejemplo

```cmd
C:\Users\strategos> tree
Folder PATH listing
Volume serial number is A8A4-C362
C:.
├───Desktop
├───Documents
├───Downloads
├───Favorites
├───Links
├───Music
├───Pictures
├───Saved Games
└───Videos
```

---

## 5. 🗑️ Eliminación de Directorios

El comando `rmdir` elimina directorios vacíos.

#### Ejemplo

```cmd
C:\example> rmdir backup_files
```

---

## 6. 📁 Copia y Movimiento de Archivos

CMD ofrece comandos para gestionar archivos de forma básica pero eficiente.

### 6.1 `copy` – Copiar Archivos

Copia un archivo de una ubicación a otra.

#### Ejemplo

```cmd
C:\example> copy test.txt test2.txt
1 file(s) copied.
```

### 6.2 `move` – Mover Archivos

Desplaza un archivo de un lugar a otro.

#### Ejemplo

```cmd
C:\example> move test2.txt ..
1 file(s) moved.
```

### 6.3 `del` / `erase` – Eliminar Archivos

Borra archivos especificados.

#### Ejemplo

```cmd
C:\example> erase test2.txt
```

---

## 7. ⚙️ Uso de Comodines (`*` y `?`)

Permiten trabajar con múltiples archivos usando patrones:

- `*` = Coincide con cualquier cantidad de caracteres.
- `?` = Coincide con un solo carácter.

#### Ejemplo

```cmd
copy *.txt C:\backup
```

---

## 8. 🕒 Gestión de Tareas y Procesos

CMD permite listar y filtrar procesos en ejecución.

### 8.1 `tasklist` – Ver Procesos Actuales

Lista todos los procesos activos en el sistema.

#### Ejemplo

```cmd
C:\> tasklist
Image Name                     PID Session Name        Session#    Mem Usage
========================= ======== ================ ========== ============
winlogon.exe                  516 Console                    1     11,144 K
services.exe                  584 Services                   0      7,492 K
lsass.exe                     592 Services                   0     16,108 K
svchost.exe                   704 Services                   0     23,432 K
```

### 8.2 Filtrar Procesos

Se pueden aplicar filtros para buscar específicamente un proceso.

#### Ejemplo

```cmd
C:\> tasklist /FI "imagename eq sshd.exe"
```

---

## 9. 🔍 Ayuda y Consulta de Comandos

Todos los comandos tienen ayuda integrada que se puede ver con el símbolo `/?`.

#### Ejemplo

```cmd
C:\> dir /?
```

---

## 10. 🔄 Visualización de Salida Página por Página

Para evitar que salidas muy largas desborden la pantalla, se puede usar el comando `more`.

### 10.1 Mostrar un Archivo Página por Página

```cmd
more file.txt
```

### 10.2 Mostrar Salida de Otro Comando

```cmd
driverquery | more
```

> ⏭ Para continuar viendo más contenido, presiona la tecla **Espacio**.  
> ✅ Para salir, presiona **Ctrl + C**.

---

## 11. 🌐 Solución de Problemas de Red

CMD incluye herramientas básicas para diagnosticar problemas de conectividad.

### 11.1 `ping` – Verificar Conectividad

Envía paquetes ICMP a un host remoto para verificar si está accesible.

#### Ejemplo

```cmd
C:\> ping example.com
Pinging example.com [93.184.215.14] with 32 bytes of data:
Reply from 93.184.215.14: bytes=32 time=78ms TTL=52
Reply from 93.184.215.14: bytes=32 time=78ms TTL=52
Reply from 93.184.215.14: bytes=32 time=78ms TTL=52
Reply from 93.184.215.14: bytes=32 time=78ms TTL=52
Ping statistics for 93.184.215.14:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 78ms, Maximum = 78ms, Average = 78ms
```

---

## 12. 🧹 Limpiar Pantalla

El comando `cls` limpia la ventana de la consola para mejorar la visibilidad.

#### Ejemplo

```cmd
C:\> cls
```

---

## 13. 📚 Recursos Adicionales

- [Lista de Comandos CMD](https://ss64.com/nt/)
- [Guía Oficial de Windows Command Prompt](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/windows-commands)
- [Documentación de Active Directory Users and Computers](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/lusrmgr.msc)
