## 1. 📝 **Introducción a Editores de Texto en la Terminal**

### 🔹 ¿Por qué usar editores de texto en terminal?
Los editores de texto en línea de comandos son herramientas esenciales para crear, editar y manipular archivos sin necesidad de una interfaz gráfica. Esto es especialmente útil en entornos remotos o con limitaciones de recursos.

### 🔹 Nano
- **Nano** es un editor sencillo y amigable, ideal para usuarios que están comenzando con el manejo de sistemas Linux.
- **Sintaxis básica:**  
  ```bash
  nano [nombre_del_archivo]
  ```
- **Ejemplo práctico:**  
  ```bash
  tryhackme@linux3:/tmp# nano myfile
  ```

#### 🔸 Funcionalidades clave de Nano:
| Acción             | Atajo de teclado       |
|--------------------|------------------------|
| Salir              | `Ctrl + X`             |
| Guardar            | `Ctrl + O`             |
| Buscar             | `Ctrl + W`             |
| Cortar/Pegar       | `Ctrl + K`, `Ctrl + U` |
| Ir a una línea     | `Ctrl + _`             |

> ⚠️ **Nota:** Al salir, Nano pregunta si desea guardar los cambios realizados.

---

## 2. 🖥️ **VIM (Vi Improved)**

### 🔹 Ventajas de VIM
- Muy popular entre desarrolladores por su potente funcionalidad.
- Permite personalización extensa.
- Soporta resaltado de sintaxis.
- No depende de instalaciones adicionales.

> 💡 **Recomendación:** TryHackMe tiene un módulo dedicado a VIM para aprender más sobre sus avanzadas funciones.

---

## 3. 🌐 **Descargar Archivos desde Internet con `wget`**

### 🔹 Sintaxis básica de `wget`
```bash
wget [URL_del_recurso]
```

### 🔹 Ejemplo Práctico:
```bash
tryhackme@linux3:/tmp# wget https://assets.tryhackme.com/additional/linux-fundamentals/part3/myfile.txt
```

> ✅ Este comando descargará el archivo `myfile.txt` directamente en el directorio actual.

---

## 4. 🔁 **Transferencia de Archivos con `scp` (Secure Copy Protocol)**

### 🔹 Descripción
El comando `scp` permite transferir archivos de manera segura entre máquinas utilizando SSH. Es útil tanto para copiar archivos locales a servidores remotos como viceversa.

### 🔹 Sintaxis general:
```bash
scp [origen] [destino]
```

### 🔹 Ejemplos:

#### 🔸 Copiar un archivo local a un servidor remoto:
```bash
scp important.txt ubuntu@192.168.1.30:/home/ubuntu/transferred.txt
```

#### 🔸 Copiar un archivo desde un servidor remoto a local:
```bash
scp ubuntu@192.168.1.30:/home/ubuntu/documents.txt notes.txt
```

> 🔒 **Seguridad:** Se requiere autenticación mediante contraseña o clave SSH.

---

## 5. 📂 **Servir Archivos Localmente con Python HTTPServer**

### 🔹 Descripción
Python incluye un módulo llamado `http.server` que permite crear rápidamente un servidor web local para compartir archivos.

### 🔹 Iniciar el Servidor:
```bash
python3 -m http.server
```

> ⚙️ **Puerto predeterminado:** 8000. Puedes cambiarlo usando:
```bash
python3 -m http.server 8080
```

### 🔹 Descargar un archivo desde el servidor:
```bash
wget http://10.10.251.114:8000/file
```

> ⚠️ **Nota:** El servidor se ejecuta en segundo plano, por lo que debes abrir una nueva terminal para usar `wget`.

---

## 6. 🔄 **Gestión de Procesos en Linux**

### 🔹 Comandos Clave

#### 🔸 `ps` (Process Status)
Muestra información sobre los procesos en ejecución asociados al usuario actual.

```bash
tryhackme@linux3:~$ ps
  PID TTY          TIME CMD
  204 pts/0    00:00:00 bash
  205 pts/0    00:00:00 ps
```

#### 🔸 `ps aux`
Muestra todos los procesos del sistema, incluidos los del usuario root.

```bash
tryhackme@linux3:~$ ps aux
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.1  24752  2120 ?        Ss   09:00   0:00 /sbin/init
cmnatic   1337  0.5  0.2  45678  3456 pts/0    S+   09:05   0:01 python script.py
```

#### 🔸 `top`
Proporciona una vista dinámica de los procesos en tiempo real.

```bash
tryhackme@linux3:~$ top
```

---

## 7. 🛑 **Finalizar Procesos con `kill`**

### 🔹 Sintaxis:
```bash
kill [PID]
```

### 🔹 Tipos de señales:
| Señal      | Propósito                         |
|------------|----------------------------------|
| `SIGTERM`  | Finaliza el proceso permitiendo limpieza |
| `SIGKILL`  | Finaliza inmediatamente el proceso     |
| `SIGSTOP`  | Detiene temporalmente el proceso       |

> 🧪 **Ejemplo:**
```bash
kill 1337
```

---

## 8. 🔄 **Namespace y Gestión de Inicios de Procesos**

### 🔹 Conceptos Básicos
- Los **namespaces** son mecanismos que aíslan recursos del sistema (como CPU, memoria) entre diferentes procesos.
- El primer proceso iniciado al arrancar el sistema es `systemd`, encargado de gestionar otros procesos.

### 🔹 Iniciar un servicio al arranque con `systemctl`
```bash
sudo systemctl enable apache2
```

### 🔹 Controlar servicios:
```bash
sudo systemctl start apache2
sudo systemctl stop apache2
sudo systemctl restart apache2
```

---

## 9. 🕰️ **Automatización con Cronjobs**

### 🔹 Introducción
`cron` permite programar tareas recurrentes (ej.: respaldos diarios, reinicios automáticos).

### 🔹 Formato de una entrada en `crontab`:
```
MIN HOUR DOM MON DOW CMD
```

#### 🔸 Ejemplo:
```bash
0 */12 * * * cp -R /home/cmnatic/Documents /var/backups/
```

> 🧩 **Wildcard (`*`):** Se usa cuando no importa el valor de un campo. Por ejemplo, `* * * * *` significa "ejecutar cada minuto".

### 🔹 Editar crontab:
```bash
crontab -e
```

> ✅ Recomendado usar `nano` o `vim` para edición.

---

## 10. 📦 **Gestión de Paquetes con APT**

### 🔹 Repositorios e Instalación
- Ubuntu utiliza repositorios (`apt`) para gestionar software.
- Para instalar un paquete:
```bash
sudo apt install [nombre_del_paquete]
```

### 🔹 Ejemplo: Instalar Sublime Text
```bash
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
sudo add-apt-repository "deb https://download.sublimetext.com/ apt/stable/"
sudo apt update
sudo apt install sublime-text
```

> 🔐 **GPG Keys:** Garantizan la integridad del software instalado.

---

## 11. 📄 **Análisis de Logs en `/var/log`**

### 🔹 Ubicación de logs
Los logs se guardan en `/var/log`. Cada servicio tiene su propio archivo de registro.

### 🔹 Ejemplos de Logs Importantes:
| Servicio           | Archivo de log                        |
|--------------------|---------------------------------------|
| Apache Web Server  | `/var/log/apache2/access.log`         |
| Fail2ban           | `/var/log/fail2ban.log`               |
| UFW Firewall       | `/var/log/ufw.log`                    |

> 🧾 **Uso común:** Analizar logs para detectar intentos de intrusión o errores de rendimiento.

---

## 12. 🧱 **Conclusión**

Este documento aborda temas fundamentales para administrar sistemas Linux de forma eficiente:

1. ✅ Uso de editores de texto en terminal como **Nano** y **VIM**.
2. ✅ Descarga y transferencia segura de archivos con **`wget`** y **`scp`**.
3. ✅ Configuración de servidores web temporales con **Python HTTPServer**.
4. ✅ Gestión de procesos con **`ps`**, **`top`** y **`kill`**.
5. ✅ Automatización de tareas con **Cron**.
6. ✅ Instalación y gestión de paquetes con **APT**.
7. ✅ Análisis de logs para monitoreo y seguridad.

Estas habilidades son esenciales para estudiantes, profesionales y administradores de sistemas que deseen dominar el entorno Linux y optimizar su productividad.

---

¿Deseas que este resumen se exporte como un **documento PDF** o una **presentación Markdown**? ¡Solo dime! 🚀