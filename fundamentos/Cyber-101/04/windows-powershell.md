## 1. 🛠️ **¿Qué es PowerShell?**

### 🔹 Definición

**PowerShell** (acrónimo de *Powerful Shell*) es una solución de automatización de tareas y gestión de configuración desarrollada por Microsoft. Combina una **interfaz de línea de comandos**, un **lenguaje de scripting** y un **marco de configuración** basado en el entorno .NET. A diferencia de herramientas anteriores como `cmd.exe`, PowerShell es **orientado a objetos**, lo que permite manipular datos complejos y interactuar con componentes del sistema de manera más eficiente.

### 🔹 Historia

- **2006:** Lanzamiento de la primera versión de PowerShell, diseñada para superar las limitaciones de herramientas como `cmd.exe` y archivos `.bat`.
- **2016:** Lanzamiento de **PowerShell Core**, versión **open-source** compatible con **Windows, macOS y Linux**, ampliando su versatilidad.

> 💡 **Objetivo principal:** Automatizar tareas administrativas y gestionar sistemas con mayor profundidad y flexibilidad.

---

## 2. 🌐 **Conceptos Fundamentales de PowerShell**

### 🔹 Objetos y Cmdlets

- **Objetos:** Unidades fundamentales en PowerShell que contienen **propiedades** (datos) y **métodos** (acciones). Ejemplo:

  ```powershell
  $car = [PSCustomObject]@{
      Color = "Rojo"
      Modelo = "Ferrari"
      Metodo = { Write-Host "Acelerar" }
  }
  ```

- **Cmdlets:** Comandos específicos de PowerShell, siguiendo la convención **Verbo-Sustantivo** (ej.: `Get-Date`, `Set-Location`). Son orientados a objetos y no procesan texto plano.

> ⚙️ **Ejemplo de Cmdlet:**  

  ```powershell
  Get-Date
  # Devuelve un objeto DateTime con propiedades como Year, Month, Day, etc.
  ```

---

## 3. 🧪 **Comandos Básicos y Funcionalidades**

### 🔹 Consulta de Cmdlets

- **Listar todos los cmdlets:**

  ```powershell
  Get-Command
  ```

- **Filtrar por tipo (ej.: funciones):**

  ```powershell
  Get-Command -CommandType Function
  ```

### 🔹 Ayuda y Documentación

- **Obtener ayuda sobre un cmdlet:**

  ```powershell
  Get-Help Get-Date
  ```

-
- **Ver ejemplos de uso:**
-

  ```powershell
  Get-Help Get-Date -Examples
  ```

### 🔹 Aliases

- **Listar aliases (comandos abreviados):**

  ```powershell
  Get-Alias
  ```

  > Ejemplos: `dir` → `Get-ChildItem`, `cd` → `Set-Location`.

---

## 4. 🗂️ **Navegación y Manipulación del Sistema de Archivos**

### 🔹 Navegación

- **Listar contenido de un directorio:**

  ```powershell
  Get-ChildItem -Path C:\Users\captain
  ```

- **Cambio de directorio:**

  ```powershell
  Set-Location -Path ".\Documents"
  ```

### 🔹 Crear y Eliminar Elementos

- **Crear un directorio:**

  ```powershell
  New-Item -Path ".\captain-cabin\captain-wardrobe" -ItemType Directory
  ```

- **Eliminar un archivo:**

  ```powershell
  Remove-Item -Path ".\captain-cabin\captain-boots.txt"
  ```

### 🔹 Copiar y Mover

- **Copiar un archivo:**

  ```powershell
  Copy-Item -Path ".\captain-hat.txt" -Destination ".\captain-hat2.txt"
  ```

- **Mover un archivo:**

  ```powershell
  Move-Item -Path ".\captain-hat2.txt" -Destination ".\captain-hat3.txt"
  ```

### 🔹 Leer Contenido de un Archivo

- **Mostrar contenido de un archivo:**

  ```powershell
  Get-Content -Path ".\captain-hat.txt"
  ```

---

## 5. 🔄 **Tuberías, Filtros y Ordenamiento de Datos**

### 🔹 Tuberías (`|`)

- **Ordenar archivos por tamaño:**

  ```powershell
  Get-ChildItem | Sort-Object Length
  ```

- **Filtrar archivos `.txt`:**

  ```powershell
  Get-ChildItem | Where-Object { $_.Extension -eq ".txt" }
  ```

### 🔹 Operadores de Comparación

| Operador | Descripción             |
|----------|--------------------------|
| `-eq`    | Igual a                 |
| `-ne`    | Diferente a             |
| `-gt`    | Mayor que               |
| `-lt`    | Menor que               |
| `-like`  | Coincidencia con patrón |

> 🧩 **Ejemplo de filtro con patrón:**

  ```powershell
  Get-ChildItem | Where-Object { $_.Name -like "ship*" }
  ```

---

## 6. 🖥️ **Información del Sistema y Red**

### 🔹 Información del Sistema

- **Obtener detalles del sistema:**

  ```powershell
  Get-ComputerInfo
  ```

  > Incluye información de hardware, BIOS, sistema operativo, etc.

### 🔹 Usuarios y Permisos

- **Listar usuarios locales:**

  ```powershell
  Get-LocalUser
  ```

### 🔹 Configuración de Red

- **Ver configuración de IP:**

  ```powershell
  Get-NetIPConfiguration
  ```

- **Listar direcciones IP:**

  ```powershell
  Get-NetIPAddress
  ```

---

## 7. 🧭 **Análisis en Tiempo Real del Sistema**

### 🔹 Procesos Activos

- **Listar procesos:**

  ```powershell
  Get-Process
  ```

  > Muestra CPU, memoria y otros recursos usados por cada proceso.

### 🔹 Servicios

- **Ver estado de servicios:**

  ```powershell
  Get-Service
  ```

### 🔹 Conexiones de Red

- **Mostrar conexiones TCP:**

  ```powershell
  Get-NetTCPConnection
  ```

### 🔹 Hashes de Archivos

- **Generar hash SHA256:**

  ```powershell
  Get-FileHash -Path ".\ship-flag.txt"
  ```

---

## 8. 📜 **Scripting en PowerShell**

### 🔹 Automatización de Tareas

- **Ejemplo de script:**

  ```powershell
  # Script.ps1
  Write-Host "Iniciando análisis de logs..."
  Get-Content -Path "C:\logs\security.log" | Select-String -Pattern "error"
  ```

- **Ejecutar script localmente:**

  ```powershell
  Invoke-Command -FilePath "C:\scripts\test.ps1"
  ```

### 🔹 Ejecución Remota

- **Ejecutar comando en servidor remoto:**

  ```powershell
  Invoke-Command -ComputerName Server01 -ScriptBlock { Get-Culture }
  ```

---

## 9. 🛡️ **Aplicaciones en Seguridad Informática**

### 🔹 Blue Team

- **Análisis de logs y detección de IOC (Indicadores de Compromiso):**

  ```powershell
  Select-String -Path "C:\logs\security.log" -Pattern "malware"
  ```

### 🔹 Red Team

- **Enumeración y ejecución remota:**

  ```powershell
  Invoke-Command -ComputerName TargetPC -ScriptBlock { Get-NetUser }
  ```

### 🔹 Administración de Sistemas

- **Automatización de políticas de seguridad:**

  ```powershell
  Get-LocalUser | Where-Object { $_.Enabled -eq $false } | Disable-LocalUser
  ```

---

## 10. 📌 **Comandos**

## 📚 Tabla de Comandos Útiles de PowerShell

| Comando | Descripción | Ejemplos |
|--------|-------------|---------|
| `Get-Command` | Lista todos los cmdlets disponibles | `Get-Command -CommandType Function`, `Get-Command -Name Get-*Process`, `Get-Command -Module NetSecurity` |
| `Get-Help` | Muestra ayuda sobre un cmdlet | `Get-Help Get-Date`, `Get-Help Get-ChildItem -Full`, `Get-Help *network*` |
| `Get-Alias` | Muestra alias predefinidos | `Get-Alias -Definition Get-ChildItem`, `Get-Alias dir`, `Get-Alias -Name cd` |
| `Get-ChildItem` | Muestra contenido de un directorio | `Get-ChildItem C:\Windows`, `Get-ChildItem -Recurse`, `Get-ChildItem *.txt` |
| `Set-Location` | Cambia al directorio especificado | `Set-Location C:\Temp`, `cd ..`, `Set-Location $env:USERPROFILE` |
| `New-Item` | Crea archivos o directorios | `New-Item -Path .\nuevo.txt -ItemType File`, `New-Item -Path .\carpeta -ItemType Directory`, `New-Item -Path HKCU:\Software\TestKey -ItemType RegistryKey` |
| `Remove-Item` | Elimina archivos o carpetas | `Remove-Item archivo.txt`, `Remove-Item carpeta -Recurse`, `Remove-Item *.tmp -Force` |
| `Copy-Item` | Copia archivos o carpetas | `Copy-Item archivo.txt copia.txt`, `Copy-Item Carpeta1 Carpeta2`, `Copy-Item -Path .\*.log -Destination Backup\` |
| `Move-Item` | Mueve archivos o carpetas | `Move-Item archivo.txt documentos\`, `Move-Item .\logs\* .\backup\`, `Move-Item -LiteralPath "archivos antiguos" .\historial\` |
| `Get-Content` | Lee el contenido de un archivo | `Get-Content archivo.txt`, `Get-Content -Tail 5 archivo.txt`, `Get-Content -Encoding UTF8 archivo.txt` |
| `Out-File` | Guarda salida en un archivo | `Get-ChildItem > lista.txt`, `Get-Service \| Out-File servicios.txt`, `Get-WmiObject Win32_DiskDrive \| Out-File disco.txt` |
| `Sort-Object` | Ordena objetos (ej.: por tamaño) | `Get-ChildItem \| Sort-Object Length -Descending`, `Get-Process \| Sort-Object CPU`, `Get-NetTCPConnection \| Sort-Object LocalPort` |
| `Where-Object` | Filtra resultados | `Get-Process \| Where-Object { $_.CPU -gt 10 }`, `Get-ChildItem \| Where-Object Name -like "*temp*"`, `Get-EventLog -LogName System \| Where-Object EntryType -eq Error` |
| `Get-ComputerInfo` | Muestra información del sistema | `Get-ComputerInfo`, `Get-ComputerInfo -Property WindowsBuildLabEx`, `Get-ComputerInfo -Property Bios*` |
| `Get-LocalUser` | Lista usuarios locales | `Get-LocalUser`, `Get-LocalUser Administrador`, `Get-LocalUser \| Select-Object Name,Enabled` |
| `Get-NetIPConfiguration` | Muestra configuración de red | `Get-NetIPConfiguration`, `Get-NetIPConfiguration -InterfaceAlias Ethernet`, `Get-NetIPConfiguration -Detailed` |
| `Get-NetIPAddress` | Muestra direcciones IP asignadas | `Get-NetIPAddress`, `Get-NetIPAddress -AddressFamily IPv4`, `Get-NetIPAddress -InterfaceIndex 12` |
| `Get-Process` | Muestra procesos activos | `Get-Process`, `Get-Process chrome`, `Get-Process -Id 1234` |
| `Stop-Process` | Detiene un proceso | `Stop-Process -Name notepad`, `Stop-Process -Id 1234`, `Get-Process explorer \| Stop-Process` |
| `Get-Service` | Muestra servicios del sistema | `Get-Service`, `Get-Service -Name Spooler`, `Get-Service -Status Running` |
| `Start-Service / Stop-Service` | Inicia o detiene un servicio | `Start-Service -Name Spooler`, `Stop-Service -Name wuauserv`, `Get-Service dhcp \| Start-Service` |
| `Get-NetTCPConnection` | Muestra conexiones TCP activas | `Get-NetTCPConnection`, `Get-NetTCPConnection -State Established`, `Get-NetTCPConnection -LocalPort 80` |
| `Get-FileHash` | Genera hash SHA256 de un archivo | `Get-FileHash archivo.exe`, `Get-FileHash -Algorithm MD5 archivo.txt`, `Get-FileHash carpeta\* -Recurse` |
| `Invoke-Command` | Ejecuta scripts o bloques de código | `Invoke-Command -ScriptBlock { Get-Date }`, `Invoke-Command -FilePath script.ps1`, `Invoke-Command -ComputerName Servidor -ScriptBlock { Get-Process }` |
| `Select-String` | Busca patrones en texto o archivos | `Select-String -Pattern "error" -Path log.txt`, `Select-String -Pattern "@gmail.com" -Path *.txt`, `Get-Content archivo.txt \| Select-String "warning"` |
| `Get-Culture` | Muestra configuración regional actual | `Get-Culture`, `Get-Culture -ListAvailable`, `Get-Culture \| Select-Object DisplayName,LCID` |
| `Get-ExecutionPolicy` | Muestra política de ejecución de scripts | `Get-ExecutionPolicy`, `Get-ExecutionPolicy -List`, `Get-ExecutionPolicy -Scope CurrentUser` |
| `Set-ExecutionPolicy` | Cambia política de ejecución de scripts | `Set-ExecutionPolicy RemoteSigned`, `Set-ExecutionPolicy Bypass -Scope CurrentUser`, `Set-ExecutionPolicy Undefined -Scope LocalMachine` |
| `Test-Connection` | Hace ping a una dirección IP | `Test-Connection google.com`, `Test-Connection 192.168.1.1`, `Test-Connection -Count 3 8.8.8.8` |
| `Get-WmiObject` | Obtiene datos desde WMI (Windows) | `Get-WmiObject Win32_BIOS`, `Get-WmiObject Win32_LogicalDisk`, `Get-WmiObject -Query "SELECT * FROM Win32_StartupCommand"` |
| `Get-EventLog` | Accede a registros del sistema | `Get-EventLog -LogName Security`, `Get-EventLog -LogName Application -Newest 10`, `Get-EventLog -InstanceId 4625 -LogName Security` |
| `Get-NetFirewallRule` | Muestra reglas de firewall | `Get-NetFirewallRule`, `Get-NetFirewallRule -DisplayName "Remote Desktop"`, `Get-NetFirewallRule -Enabled True` |
