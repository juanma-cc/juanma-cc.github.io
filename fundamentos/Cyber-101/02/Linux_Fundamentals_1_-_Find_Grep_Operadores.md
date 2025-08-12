## 1. 💡 Eficiencia con Linux

Linux destaca por su **eficiencia** una vez que el usuario se familiariza con sus comandos básicos. A medida que interactúas con sistemas como Ubuntu, los comandos esenciales se vuelven parte del hábito (muscle memory).

---

## 2. 🔍 Uso del Comando `find`

El comando `find` permite buscar archivos a través de todo el sistema sin necesidad de navegar manualmente con `cd` y `ls`.

### Ejemplo: Buscar un archivo específico
```bash
tryhackme@linux1:~$ find -name passwords.txt
./folder1/passwords.txt
```

### Ejemplo: Buscar todos los archivos `.txt`
```bash
tryhackme@linux1:~$ find -name *.txt
./folder1/passwords.txt
./Documents/todo.txt
```

📌 Resultados:
1. `passwords.txt` en `folder1`
2. `todo.txt` en `Documents`

---

## 3. 🔎 Introducción al Comando `grep`

El comando `grep` sirve para **buscar contenido dentro de archivos**. Es útil para filtrar información en logs o archivos grandes.

### Ejemplo: Contar líneas en un log
```bash
tryhackme@linux1:~$ wc -l access.log
244 access.log
```

### Ejemplo: Buscar una IP en el log
```bash
tryhackme@linux1:~$ grep "81.143.211.90" access.log
81.143.211.90 - - [25/Mar/2021:11:17 +0000] "GET / HTTP/1.1" 200 417 "-" "Mozilla/5.0 (Linux; Android 7.0; Moto G(4))"
```

---

## 4. ⚙️ Operadores en Linux

Los operadores permiten optimizar y encadenar comandos para hacer más eficiente el trabajo en terminal.

| Símbolo | Nombre | Descripción |
|--------|--------|-------------|
| `&`    | Background Operator | Ejecuta comandos en segundo plano. |
| `&&`   | Logical AND         | Encadena comandos, ejecutando el siguiente solo si el anterior fue exitoso. |
| `>`    | Redirect Output     | Redirige la salida de un comando, sobrescribiendo un archivo. |
| `>>`   | Append Output       | Redirige la salida, pero añade al final del archivo sin sobrescribir. |

---

### 4.1 ➕ Operador `&`

Ejecuta un comando en segundo plano, permitiendo continuar usando la terminal.

```bash
cp largefile.iso backup/ &
```

---

### 4.2 🔗 Operador `&&`

Encadena comandos condicionalmente:

```bash
command1 && command2
```

Solo se ejecuta `command2` si `command1` tiene éxito.

---

### 4.3 📥 Operador `>`

Redirige la salida de un comando a un archivo (lo sobrescribe si existe):

```bash
echo hey > welcome
cat welcome
# Salida: hey
```

---

### 4.4 📥➕ Operador `>>`

Añade la salida al final del archivo sin borrar contenido previo:

```bash
echo hello >> welcome
cat welcome
# Salida:
# hey
# hello
```