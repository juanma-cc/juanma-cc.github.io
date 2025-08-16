# Modelos de Seguridad y Principios de Diseño

## 1. 🛡️ Modelos de Seguridad

Los modelos de seguridad son esquemas teóricos que definen cómo debe ser gestionada la información sensible dentro de un sistema. A continuación, se explican dos modelos clásicos:

---

## 2. 🔐 Modelo Bell-LaPadula

### 2.1 Propósito

El modelo **Bell-LaPadula** se centra en el control de acceso basado en niveles de clasificación o "seguridad". Su objetivo principal es prevenir la filtración de información sensible a usuarios con menor nivel de seguridad.

### 2.2 Propiedades Clave

| Propiedad | Descripción |
|----------|-------------|
| **Discretionary-Security Property** | Permite operaciones de lectura y escritura según una matriz de acceso. |
| **Simple Security Property** | Regla de "read down": Un sujeto solo puede leer objetos de igual o menor nivel de seguridad. |
| **Star Property** | Regla de "write up": Un sujeto solo puede escribir en objetos de igual o mayor nivel de seguridad. |

> ✅ **Resumen:** *Write Up / Read Down*

#### Ejemplo:

| Sujeto   | Objeto A   | Objeto B  |
| -------- | ---------- | --------- |
| Sujeto 1 | Write      | No access |
| Sujeto 2 | Read/Write | Read      |

Este modelo permite compartir información confidencial con usuarios de nivel superior (write up), pero no permite que los sujetos de nivel inferior lean datos sensibles (read down).

---

## 3. 🧾 Modelo Biba

### 3.1 Propósito
El modelo **Biba** se enfoca en garantizar la **integridad** de los datos. Define reglas que evitan que información no confiable afecte datos críticos.

### 3.2 Propiedades Clave

| Propiedad | Descripción |
|----------|-------------|
| **Simple Integrity Property** | *"No read down"*: Un sujeto de alto nivel de integridad no puede leer objetos de bajo nivel de integridad. |
| **Star Integrity Property** | *"No write up"*: Un sujeto de bajo nivel de integridad no puede escribir sobre objetos de alto nivel de integridad. |

> ✅ **Resumen:** *No read down / No write up*

---

## 4. ⚖️ Diferencias entre Bell-LaPadula y Biba

| Característica | Bell-LaPadula | Biba |
|----------------|---------------|------|
| Enfocarse en   | Confidencialidad | Integridad |
| Regla principal | Write up / Read down | No read down / No write up |
| Aplicabilidad | Control de acceso por nivel de seguridad | Prevención de corrupción de datos |
| Limitación     | No maneja bien el intercambio de archivos | No aborda directamente la confidencialidad |

---

## 5. 🛠️ Principios de Diseño de Sistemas Seguros

### 5.1 Encapsulación

- **Definición**: Ocultar detalles internos de un objeto o sistema, permitiendo interactuar con él solo a través de interfaces definidas.
- **Uso**: Impide manipulaciones no autorizadas o incorrectas de datos internos.
- **Ejemplo**: En programación orientada a objetos (OOP), si tienes un reloj (`clock`), se proporciona un método `increment()` en lugar de acceder directamente a la variable `seconds`.

```python
class Clock:
    def __init__(self):
        self._seconds = 0

    def increment(self):
        self._seconds += 1
```

> 🔒 Esto previene que se asignen valores inválidos a `_seconds`.

---

### 5.2 Minimización de la Superficie de Ataque

- **Definición**: Reducir al mínimo las interfaces o componentes expuestos al exterior para limitar puntos de entrada posibles para atacantes.
- **Objetivo**: Disminuir el número de vulnerabilidades potenciales.
- **Ejemplo**: 
  - Deshabilitar servicios innecesarios en un sistema Linux.
  - Eliminar funcionalidades redundantes en una aplicación web.

> ⚠️ Cada servicio o componente adicional representa un riesgo potencial.

---

### 5.3 Otros Principios Importantes

- **Principio del Menor Privilegio**: Los usuarios y procesos deben tener únicamente los permisos necesarios para realizar su tarea.
- **Diseño Abierto (Open Design)**: La seguridad no debe depender del secreto del diseño; debe estar en la clave utilizada.
- **Tolerancia a Fallos**: El sistema debe seguir funcionando correctamente incluso ante fallos o intentos de ataque.

---

## 6. 🧩 Aplicación Práctica

Estos principios y modelos no son abstractos, sino que tienen aplicaciones prácticas en el desarrollo y administración de sistemas seguros:

### Ejemplo Real:
- **Linux Hardening**:
  - Desactivar servicios no usados:  
    ```bash
    sudo systemctl disable apache2
    ```
  - Configurar políticas de acceso con SELinux o AppArmor.

- **Aplicaciones Web**:
  - Usar APIs bien definidas y validar todas las entradas del usuario.
  - Implementar autenticación y autorización robustas.

---

## 7. 🧭 Conclusión

Este documento ofrece una visión clara de cómo diseñar sistemas seguros mediante modelos teóricos como **Bell-LaPadula** y **Biba**, junto con principios fundamentales de seguridad como **encapsulación**, **menor privilegio** y **minimización de la superficie de ataque**.

Entender estos conceptos ayuda a construir sistemas más seguros y resilientes frente a amenazas modernas.

---

## 8. 📚 Recursos Adicionales

- [OWASP Top Ten](https://owasp.org/www-project-top-ten/)
- [Código abierto vs. Seguridad](https://www.ciphercloud.com/blog/open-design-vs-security-by-obscurity)
- [Guía de Hardening para Linux](https://wiki.archlinux.org/title/Security)
- [Modelos de Seguridad Informática](https://csrc.nist.gov/publications/detail/sp/800-181/final)