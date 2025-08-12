## 1. 🌐 **Conexión Remota a una Máquina Linux mediante SSH**

### 🔹 ¿Qué es SSH?
**SSH (Secure Shell)** es un protocolo que permite conectarse de manera segura a una máquina remota. La conexión se establece mediante un cliente SSH (como `ssh` en Linux/macOS) y un servidor SSH instalado en la máquina objetivo.

### 🔹 Sintaxis y Ejemplo Práctico
- **Sintaxis básica:**  
  ```bash
  ssh [usuario]@[dirección_IP]
  ```
- **Ejemplo:**  
  ```bash
  ssh tryhackme@MACHINE_IP
  ```
  Reemplaza `MACHINE_IP` con la dirección IP de la máquina Linux objetivo.  
  - **Nota:** Al introducir la contraseña, **no se muestra visualmente** en la terminal, pero se procesa normalmente.

---

## 2. 🛠️ **Introducción a Banderas y Comandos Básicos**

### 🔹 Banderas (Flags/Switches)
Las banderas modifican el comportamiento de los comandos. Ejemplo con `ls`:
- **Comando base:**  
  ```bash
  ls
  ```
  Muestra archivos visibles en el directorio actual (ej.: `folder1`).
- **Banda `-a` (mostrar archivos ocultos):**  
  ```bash
  ls -a
  ```
  Muestra archivos ocultos (ej.: `.hiddenfolder`).

### 🔹 Uso de `--help` y Manuales
- **Ver opciones de un comando:**  
  ```bash
  ls --help
  ```
  Muestra una lista de banderas disponibles y ejemplos de uso.
- **Acceder al manual (`man`):**  
  ```bash
  man ls
  ```
  Proporciona documentación detallada del comando.

---

## 3. 🗂️ **Interacción con el Sistema de Archivos**

### 🔹 Comandos Clave y Ejemplos
| **Comando** | **Nombre**       | **Propósito**                      | **Ejemplo**                          |
|-------------|------------------|------------------------------------|--------------------------------------|
| `touch`     | Crear archivo    | Crea un archivo vacío              | `touch note`                         |
| `mkdir`     | Crear directorio | Crea una carpeta                   | `mkdir mydirectory`                  |
| `cp`        | Copiar           | Duplica archivos o carpetas        | `cp note note2`                      |
| `mv`        | Mover/Renombrar  | Mueve o renombra archivos/carpetas | `mv note2 note3`                     |
| `rm`        | Eliminar         | Borra archivos o carpetas          | `rm note` (archivo) o `rm -R` (carpeta) |
| `file`      | Determinar tipo  | Identifica el tipo de archivo      | `file note` (salida: `ASCII text`)   |

### 🔹 Ejemplos Prácticos
- **Crear y listar archivos:**  
  ```bash
  touch note
  ls
  # Salida: folder1 note
  ```
- **Copiar archivos:**  
  ```bash
  cp note note2
  ls
  # Salida: folder1 note note2
  ```
- **Mover/renombrar archivos:**  
  ```bash
  mv note2 note3
  ls
  # Salida: folder1 note note3
  ```

---

## 4. 🔐 **Permisos de Archivos y Usuarios**

### 🔹 Tipos de Permisos
- **Read (r):** Leer contenido.
- **Write (w):** Modificar contenido.
- **Execute (x):** Ejecutar (para scripts o directorios).

### 🔹 Visualización con `ls -l`
- **Ejemplo de salida:**  
  ```bash
  ls -lh
  # -rw-r--r-- 1 cmnatic cmnatic 0 Feb 19 10:37 file1
  ```
  - `-rw-r--r--`: Permisos para **propietario**, **grupo** y **otros**.
  - `cmnatic`: Propietario y grupo del archivo.

### 🔹 Usuarios y Grupos
- Los permisos se asignan a **usuarios** y **grupos**. Por ejemplo:
  - Un usuario puede tener permisos `rw` en un archivo.
  - Un grupo puede tener permisos `r` en el mismo archivo.

---

## 5. 👤 **Cambio de Usuarios con `su`**

### 🔹 Comando `su` (Switch User)
- **Cambiar a otro usuario:**  
  ```bash
  su user2
  # Se solicita la contraseña de user2.
  ```
- **Iniciar sesión como usuario:**  
  ```bash
  su -l user2
  # Carga el entorno de user2 (ej.: variables de entorno).
  ```

### 🔹 Ejemplo Práctico
```bash
tryhackme@linux2:~$ su -l user2
Password:
user2@linux2:~$ pwd
/home/user2
```

---

## 6. 📁 **Directorios Clave en Linux**

### 🔹 `/etc` (Configuration)
- Almacena archivos de configuración del sistema.
- **Archivos destacados:**
  - `/etc/passwd`: Usuarios del sistema.
  - `/etc/shadow`: Contraseñas encriptadas (SHA-512).
  - `/etc/sudoers`: Permisos de ejecución como `root`.

### 🔹 `/var` (Variable Data)
- Datos dinámicos generados por servicios (ej.: logs).
- **Subdirectorios comunes:**
  - `/var/log`: Logs del sistema.
  - `/var/tmp`: Archivos temporales.

### 🔹 `/root`
- **Carpeta personal del usuario `root`.**  
  ```bash
  root@linux2:~# ls
  myfile myfolder passwords.xlsx
  ```

### 🔹 `/tmp` (Temporal)
- **Usado para almacenamiento temporal.**  
  - Los archivos se eliminan al reiniciar el sistema.
  - Útil en pruebas de penetración para scripts temporales.
  ```bash
  root@linux2:/tmp# ls
  todelete trash.txt rubbish.bin
  ```

---

## 7. 🧪 **Práctica: Simulador de Red y Enumeración**

- **Tarea:** Enviar un paquete TCP desde `Computer1` a `Computer3` usando un simulador de red.
- **Herramienta recomendada:** Navegadores Chrome o Firefox.
- **Objetivo:** Comprender el enrutamiento de paquetes y la interacción entre routers, switches y firewalls.

---

## 8. 📌 **Conclusión**

Este documento aborda conceptos fundamentales para interactuar con sistemas Linux y redes:
- **SSH:** Conexión segura a máquinas remotas.
- **Comandos básicos:** Manipulación de archivos y directorios.
- **Permisos:** Control de acceso mediante usuarios y grupos.
- **Directorios clave:** Funcionalidad y uso de `/etc`, `/var`, `/root` y `/tmp`.