## 1. 🛠️ **Conceptos Básicos de Scripting en Bash**

### 🔹 ¿Qué es un Script en Bash?

Un **script en Bash** es un archivo de texto que contiene comandos de terminal y lógica programática, permitiendo automatizar tareas repetitivas o complejas en sistemas Linux. Los scripts son fundamentales para la administración de sistemas, análisis de datos y ciberseguridad.

---

## 2. 📜 **Estructura de un Script Bash**

### 🔹 Shebang (`#!/bin/bash`)

- **Propósito:** Especifica el intérprete que debe ejecutar el script (en este caso, Bash).
- **Ejemplo:**

  ```bash
  #!/bin/bash
  echo "Este es un script de ejemplo."
  ```

> ⚠️ **Nota:** Sin el shebang, el sistema podría usar otro intérprete (como `sh`), lo que puede causar errores.

---

## 3. 🔄 **Variables y Entrada del Usuario**

### 🔹 Declaración de Variables

- **Sintaxis:**

  ```bash
  variable="valor"
  ```

- **Ejemplo:**

  ```bash
  nombre="John"
  echo "Hola, $nombre"
  ```

### 🔹 Lectura de Entrada del Usuario

- **Comando `read`:**

  ```bash
  read -p "Ingrese su nombre: " nombre
  echo "Bienvenido, $nombre"
  ```

---

## 4. 🔁 **Bucles y Condicionales**

### 🔹 Bucle `for`

- **Ejemplo de bucle que itera 3 veces:**

  ```bash
  for i in {1..3}; do
    echo "Iteración $i"
  done
  ```

### 🔹 Condicionales `if-else`

- **Ejemplo de validación de nombre:**

  ```bash
  read -p "Ingrese su nombre: " nombre
  if [ "$nombre" = "Stewart" ]; then
    echo "Bienvenido Stewart! Aquí está el secreto: THM_Script"
  else
    echo "No está autorizado."
  fi
  ```

---

## 5. 🧩 **Comentarios en Scripts**

- **Propósito:** Documentar el código para facilitar su lectura y mantenimiento.
- **Sintaxis:**

  ```bash
  # Este es un comentario
  # Definiendo el intérprete
  #!/bin/bash
  # Pidiendo al usuario que ingrese su nombre
  read -p "Nombre: " nombre
  ```

---

## 6. 🔐 **Ejemplo Complejo: "The Locker Script"**

### 🔹 Descripción

Este script utiliza bucles, variables y condicionales para validar credenciales (nombre, empresa y PIN).

### 🔹 Código del Script

```bash
#!/bin/bash
for i in {1..3}; do
  if [ "$i" -eq 1 ]; then
    read -p "Usuario: " usuario
  elif [ "$i" -eq 2 ]; then
    read -p "Empresa: " empresa
  else
    read -p "PIN: " pin
  fi
done

if [ "$usuario" = "John" ] && [ "$empresa" = "Tryhackme" ] && [ "$pin" = "7385" ]; then
  echo "Autenticación exitosa. Acceso concedido."
else
  echo "Autenticación fallida. Acceso denegado."
fi
```

> 🧪 **Ejecución:**

  ```bash
  ./locker_script.sh
  Usuario: John
  Empresa: Tryhackme
  PIN: 7385
  Autenticación exitosa. Acceso concedido.
  ```

---

## 7. 🔍 **Uso de `grep` para Búsqueda de Texto**

### 🔹 Descripción

El comando `grep` permite buscar patrones o palabras dentro de archivos, útil para análisis de logs o documentos grandes.

### 🔹 Ejemplo

```bash
grep "THM" archivo.txt
```

> 🧾 **Resultado:** Muestra todas las líneas en `archivo.txt` que contienen la palabra "THM".
