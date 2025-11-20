# Capítulo 12: Buenas Prácticas y Estilo de Código

La calidad del código no se mide solo por si funciona, sino por si es legible, mantenible y predecible. Este capítulo explora las buenas prácticas que distinguen a los desarrolladores profesionales.

### 12.1. Importancia del Estilo Consistente

El código se lee mucho más frecuentemente de lo que se escribe. Un estilo consistente facilita la colaboración y reduce errores.

```javascript
// Inconsistente (difícil de leer)
let x=5; let y=10
if(x>y){console.log("x es mayor")}

// Consistente (fácil de leer)
let x = 5;
let y = 10;

if (x > y) {
    console.log("x es mayor");
}
```

***

### 12.2. Naming Conventions: camelCase

JavaScript usa **camelCase** como convención estándar:

```javascript
// ✓ Variables y funciones: camelCase
let nombreUsuario = "Juan";
let edadEnAños = 30;
function calcularPromedio(notas) { }
function obtenerDatosDelServidor() { }

// ✓ Constantes: UPPER_SNAKE_CASE
const MAX_INTENTOS = 3;
const URL_BASE = "https://api.ejemplo.com";

// ✓ Clases: PascalCase (estudiaremos en POO)
class Usuario { }
class CalculadoraAvanzada { }

// Evitar
let usuario_nombre;     // snake_case (Python style)
let NOMBRE;            // Confunde con constante
let n, x, a;           // Nombres crípticos
```

***

### 12.3. Comentarios: Explicar el Porqué

Los comentarios deben explicar **por qué** haces algo, no **qué** estás haciendo (el código ya lo dice).

```javascript
// Malo: Comenta lo obvio
let edad = 30;         // Establece edad a 30
edad = edad + 1;       // Incrementa edad en 1

// Bueno: Explica la intención
let edad = 30;         // Edad al iniciar sesión
edad = edad + 1;       // Cumpleaños detectado durante la sesión
```

#### **Tipos de comentarios**

```javascript
// Comentario de línea única para explicaciones breves

/* 
 * Comentario de múltiples líneas
 * para explicaciones más largas
 */

/**
 * Docstring para documentar funciones
 * @param {number} edad - La edad del usuario
 * @returns {boolean} true si es mayor de edad
 */
function esMayorDeEdad(edad) {
    return edad >= 18;
}
```

***

### 12.4. Indentación y Espaciado

```javascript
// ✓ 4 espacios por nivel de indentación
if (condicion) {
    let resultado = operacion();
    for (let i = 0; i < 10; i++) {
        resultado = resultado * 2;
    }
}

// ✓ Espacios alrededor de operadores
let suma = x + y;
let comparacion = x === y;

// ✓ Línea en blanco entre funciones y bloques lógicos
function primeraFuncion() {
    return 42;
}

function segundaFuncion() {
    return 43;
}
```

***

### 12.5. Evitar Antipatrones Comunes

#### **Antipatrón 1: Variables globales**

```javascript
// ✗ Evitar
var globalVariable = "Soy global";

function modificarGlobal() {
    globalVariable = "Modificada";
}

// ✓ Mejor: Encapsular en función
function crearPrograma() {
    let localVariable = "Soy local";
    
    function modificarLocal() {
        localVariable = "Modificada";
    }
    
    return { modificarLocal };
}
```

#### **Antipatrón 2: Uso de `eval()`**

```javascript
// ✗ Nunca hagas esto
let codigo = "console.log('Peligroso')";
eval(codigo);   // Seguridad y rendimiento comprometidos

// ✓ Alternativa: Funciones
let handlers = {
    accion1: () => console.log("Acción 1"),
    accion2: () => console.log("Acción 2")
};
handlers["accion1"]();
```

#### **Antipatrón 3: Condiciones complejas sin paréntesis**

```javascript
// ✗ Difícil de entender
if (a > b && c < d || e === f && g !== h) { }

// ✓ Mejor: Paréntesis para claridad
if ((a > b && c < d) || (e === f && g !== h)) { }

// ✓ O mejor aún: Extraer a función
if (cumplePrimesCondiciones() || cumpleSegundas()) { }
```

***

### 12.6. Herramientas: ESLint y Prettier

Estas herramientas automatizan el control de estilo:

```bash
# ESLint: Detecta problemas de código
npx eslint archivo.js

# Prettier: Formatea código automáticamente
npx prettier --write archivo.js
```

***

### 12.7. Principios SOLID Adaptados a JavaScript

#### **S: Single Responsibility**

Una función debe tener una única responsabilidad:

```javascript
// ✗ Hace demasiadas cosas
function procesarUsuario(datos) {
    // Validar
    if (!datos.nombre) return false;
    
    // Guardar en BD
    database.insert(datos);
    
    // Enviar email
    enviarEmail(datos.email);
    
    return true;
}

// ✓ Responsabilidades separadas
function validarDatos(datos) {
    return datos.nombre && datos.email;
}

function guardarUsuario(datos) {
    return database.insert(datos);
}

function notificarUsuario(email) {
    return enviarEmail(email);
}
```

#### **O: Open/Closed**

Abierto para extensión, cerrado para modificación:

```javascript
// ✗ Requiere modificar función existente
function calcularCosto(tipo, monto) {
    if (tipo === "a") return monto * 1.1;
    if (tipo === "b") return monto * 1.2;
    // Agregar nuevo tipo requiere modificar esta función
}

// ✓ Extensible sin modificar
const costos = {
    a: monto => monto * 1.1,
    b: monto => monto * 1.2,
    c: monto => monto * 1.3
};

function calcularCosto(tipo, monto) {
    return costos[tipo](monto);
}
```

***

### 12.8. Lectura de Código de Calidad

Aprender leyendo código bien escrito es invaluable:

* Proyectos open source en GitHub
* Código de librerías populares (lodash, axios)
* Repositorios didácticos en MDN Web Docs

***

### Resumen del Capítulo

Las buenas prácticas y el estilo consistente transforman código funcional en código profesional. Invertir tiempo en escribir código limpio ahora ahorra debugging y mantenimiento después.

#### **💡 Conceptos Clave:**

* **camelCase**: Convención estándar de nombres
* **Comentarios significativos**: Explica el "porqué"
* **Indentación consistente**: 4 espacios
* **Evitar antipatrones**: var, eval(), condiciones confusas
* **Herramientas de linting**: ESLint, Prettier
* **SOLID**: Principios de buen diseño
* **Lectura activa**: Aprender de código de calidad

#### **🤔 Preguntas de Reflexión:**

1. ¿Por qué es importante el estilo de código en un equipo?
2. ¿Cuál es la diferencia entre comentarios buenos y malos?
3. Da ejemplos de cuándo Single Responsibility mejora el código.
4. ¿Cómo te ayudan herramientas como ESLint a escribir mejor código?
5. Refactoriza código existente aplicando estos principios.

***
