## 1. 🌐 Introducción a Active Directory

**Active Directory (AD)** es una solución centralizada ofrecida por Microsoft que permite la gestión de usuarios, equipos y recursos en una red Windows. Su núcleo principal es el **Active Directory Domain Services (AD DS)**, que actúa como un directorio que contiene toda la información sobre los objetos existentes en la red, como usuarios, grupos, máquinas, impresoras y compartidos.

### ✅ Ventajas Principales:
- **Centralización de identidad**: Gestión única de usuarios y permisos.
- **Políticas de seguridad**: Aplicación uniforme de reglas de acceso y protección.
- **Escalabilidad**: Ideal para empresas con cientos o miles de usuarios y dispositivos.

> 💡 Ejemplo real: En universidades o escuelas, normalmente usamos una única cuenta para acceder a cualquier computadora del campus. Esto se debe a que todas las máquinas están conectadas al mismo Active Directory.

---

## 2. 👥 Tipos de Objetos en Active Directory

AD gestiona distintos tipos de objetos, algunos de los más importantes son:

### 2.1 Usuarios
- Representan personas o servicios que necesitan acceder a la red.
- Pueden ser:
  - **Usuarios Personales**: Empleados u otros usuarios humanos.
  - **Usuarios de Servicio**: Cuentas utilizadas por aplicaciones como IIS o SQL Server.

### 2.2 Equipos (Máquinas)
- Cada equipo que se une al dominio crea automáticamente un objeto de máquina en AD.
- Tienen credenciales propias (contraseña generada automáticamente).
- El nombre de las cuentas de máquina suele terminar con `$`, por ejemplo: `DC01$`.

### 2.3 Grupos de Seguridad
- Se usan para agrupar usuarios y máquinas con fines de asignación de permisos.
- Algunos grupos predefinidos son:
  - **Domain Admins**: Control total sobre el dominio.
  - **Server Operators**: Gestión de controladores de dominio.
  - **Backup Operators**: Acceso completo a archivos, útil para respaldos.
  - **Account Operators**: Crear/modificar cuentas de usuario.
  - **Domain Users**: Todos los usuarios normales del dominio.
  - **Domain Computers**: Todas las máquinas del dominio.
  - **Domain Controllers**: Todos los DCs del dominio.

---

## 3. 🗂️ Organizational Units (OUs)

Las OUs son contenedores que permiten organizar objetos (usuarios, máquinas, etc.) según roles o departamentos. Se usan principalmente para aplicar políticas de grupo (GPOs).

> ⚠️ Un usuario solo puede estar en **una sola OU** a la vez.

### Ejemplo de Estructura de OUs:
```
THM
├── IT
├── Sales
├── Marketing
└── Management
```

> 🔧 Para eliminar una OU no deseada (por ejemplo, un departamento cerrado), debes:
1. Abrir **Active Directory Users and Computers**.
2. Ir a **View > Advanced Features**.
3. Hacer clic derecho en la OU y seleccionar **Properties**.
4. Desmarcar **Protect object from accidental deletion**.
5. Confirmar eliminación.

---

## 4. 🛠️ Delegación de Privilegios

La delegación permite otorgar ciertos privilegios a usuarios sin darles acceso total al sistema.

### Ejemplo: Delegar Reseteo de Contraseñas

1. En **Active Directory Users and Computers**, hacer clic derecho en la OU deseada (ej. Sales).
2. Seleccionar **Delegate Control...**
3. Añadir el usuario (ej. Phillip).
4. Seleccionar **Reset Password** y confirmar.

#### PowerShell para resetear contraseñas:
```powershell
Set-ADAccountPassword sophie -Reset -NewPassword (Read-Host -AsSecureString -Prompt 'New Password') -Verbose
Set-ADUser -ChangePasswordAtLogon $true -Identity sophie -Verbose
```

---

## 5. 📁 Administración de Equipos

Los equipos también pueden ser gestionados dentro de AD. Por ejemplo, si se elimina una OU, también se eliminan todos sus objetos asociados (máquinas, usuarios, etc.).

---

## 6. 🧩 Group Policy Objects (GPOs)

Las GPOs permiten aplicar configuraciones específicas a usuarios o equipos dentro de una OU.

### Ejemplo de Uso:
- Bloquear el acceso al Panel de Control.
- Forzar actualizaciones automáticas.
- Configurar ajustes de seguridad.

---

## 7. 🔐 Métodos de Autenticación

### 7.1 Kerberos (Protocolo Moderno)

Kerberos es el protocolo predeterminado en versiones recientes de Windows. Funciona mediante **tickets de autenticación**.

#### Proceso Básico:
1. El usuario envía su nombre y un timestamp al Key Distribution Center (KDC).
2. KDC devuelve un Ticket Granting Ticket (TGT).
3. Con el TGT, el usuario obtiene tickets específicos para cada servicio.

> ✅ Ofrece mayor seguridad y eficiencia.

---

### 7.2 NetNTLM (Protocolo Legado)

NetNTLM utiliza un mecanismo de **challenge-response**.

#### Proceso:
1. El cliente solicita acceso.
2. El servidor genera un desafío.
3. El cliente responde usando su hash de contraseña.
4. El DC valida la respuesta.

> ⚠️ Considerado obsoleto, pero aún utilizado por compatibilidad.

---

## 8. 🌳 Árboles, Bosques y Confianzas

### 8.1 Árbol (Tree)
Un árbol es una extensión de un dominio principal, con subdominios que comparten el mismo espacio de nombres.

Ejemplo:
```
thm.local
├── uk.thm.local
└── us.thm.local
```

### 8.2 Bosque (Forest)
Un bosque es una colección de árboles con espacios de nombres diferentes.

Ejemplo:
```
thm.local
└── mhtinc.local
```

### 8.3 Confianza (Trust)
Una confianza permite que usuarios de un dominio accedan a recursos de otro dominio.

- **Confianza Unidireccional**: Si A confía en B, los usuarios de B pueden acceder a A.
- **Confianza Bidireccional**: Ambos dominios se confían mutuamente.

---

## 9. 🎯 Grupos Especiales

- **Enterprise Admins**: Tienen control total sobre todos los dominios del bosque.
- **Domain Admins**: Tienen control sobre su propio dominio.

---

## 10. 📌 Notas Importantes

- La creación de perfiles de usuario ocurre tras el primer inicio de sesión.
- Los usuarios estándar no ven opciones avanzadas como "Add someone else to this PC".
- Los comandos como `ipconfig`, `netstat` y `whoami` son útiles para diagnóstico de redes.
- PowerShell reemplaza a herramientas legadas como `WMIC`.

---

## 11. 📚 Recursos Adicionales

- [Documentación Oficial de Active Directory](https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/)
- [Lista de Comandos CMD](https://ss64.com/nt/)
- [Windows Event Logs](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/eventvwr)