# Capítulo 4: Entrada de Datos y Console

La interacción con el usuario es fundamental en cualquier programa. Este capítulo explora cómo obtener datos del usuario y utilizar la consola como herramienta de comunicación y depuración.

### 4.1. `prompt()`: Lectura desde Diálogo Modal

`prompt()` abre un diálogo modal que permite al usuario ingresar texto.

```javascript
let nombre = prompt("¿Cuál es tu nombre?");
console.log(nombre);

// Con valor por defecto
let edad = prompt("¿Cuántos años tienes?", "18");

// El usuario puede cancelar (retorna null)
let entrada = prompt("Introduce algo:");
if (entrada === null) {
    console.log("El usuario canceló");
} else {
    console.log("El usuario escribió:", entrada);
}
```

#### **Limitaciones de `prompt()`**

```javascript
// prompt() siempre retorna una cadena (o null si cancela)
let edad = prompt("Ingresa tu edad:");
console.log(typeof edad);           // "string"

// Convertir a número
let edadNumerica = Number(edad);
console.log(typeof edadNumerica);   // "number"

// O mejor, usar parseInt
let edadEntera = parseInt(edad);
```

#### **Validación con `prompt()`**

```javascript
function obtenerEdad() {
    let entrada = prompt("Ingresa tu edad:");
    
    // Si cancela
    if (entrada === null) {
        return null;
    }
    
    // Si es vacío
    if (entrada === "") {
        alert("Debes ingresar algo");
        return obtenerEdad();  // Pedir de nuevo
    }
    
    // Convertir y validar
    let edad = parseInt(entrada);
    if (isNaN(edad)) {
        alert("Debes ingresar un número");
        return obtenerEdad();  // Pedir de nuevo
    }
    
    return edad;
}
```

***

### 4.2. `confirm()`: Confirmación Binaria del Usuario

`confirm()` abre un diálogo con dos opciones: Aceptar (true) o Cancelar (false).

```javascript
let confirmacion = confirm("¿Estás seguro?");
console.log(confirmacion);          // true o false

// Uso común: confirmación de acciones
let eliminar = confirm("¿Eliminar este elemento?");
if (eliminar) {
    console.log("Elemento eliminado");
} else {
    console.log("Operación cancelada");
}
```

#### **Flujo de decisión con `confirm()`**

```javascript
let continuar = true;

if (!confirm("¿Deseas continuar?")) {
    continuar = false;
}

if (continuar) {
    console.log("Continuamos...");
} else {
    console.log("Operación cancelada");
}
```

***

### 4.3. `alert()`: Notificación al Usuario

`alert()` muestra un mensaje de alerta modal que el usuario debe confirmar.

```javascript
alert("¡Hola Mundo!");
alert("La operación se completó exitosamente");

// alert() no retorna nada útil (retorna undefined)
let resultado = alert("Presiona aceptar");
console.log(resultado);             // undefined
```

#### **Combinación de funciones de diálogo**

```javascript
function procesarUsuario() {
    let nombre = prompt("¿Tu nombre?");
    
    if (nombre === null || nombre === "") {
        alert("Debes ingresar un nombre");
        return;
    }
    
    let confirmado = confirm(`¿Es tu nombre realmente ${nombre}?`);
    
    if (confirmado) {
        alert(`¡Bienvenido, ${nombre}!`);
    } else {
        alert("Por favor, intenta de nuevo");
    }
}
```

#### **Limitaciones de `alert`/`prompt`/`confirm`**

* Bloquean la ejecución del programa (síncronos)
* Estilo visualmente anticuado
* No personalizables (se ven iguales en todos los navegadores)
* En producción, se prefieren interfaces HTML personalizadas

***

### 4.4. `console` como Herramienta de Depuración

La consola del navegador es tu mejor aliada para entender qué hace tu código.

```javascript
// Acceder a la consola: F12 o Ctrl+Shift+I (Windows/Linux) o Cmd+Option+I (Mac)
// Luego ir a la pestaña "Console"
```

***

### 4.5. `console.log()`, `console.warn()`, `console.error()`

#### **`console.log()`**

Muestra información general:

```javascript
console.log("Texto simple");
console.log(42);
console.log([1, 2, 3]);
console.log({ nombre: "Juan", edad: 30 });

// Múltiples argumentos
console.log("Usuario:", "Juan", "Edad:", 30);
```

#### **`console.warn()`**

Muestra advertencias (en amarillo):

```javascript
console.warn("Esta función está deprecada");
console.warn("Uso de memoria alto");
```

#### **`console.error()`**

Muestra errores (en rojo):

```javascript
console.error("Error fatal:");
console.error(new Error("Algo salió mal"));
```

***

### 4.6. Formateo de Mensajes en Consola

#### **Especificadores de formato**

```javascript
// %s: cadena
console.log("Hola %s", "Juan");       // Hola Juan

// %d o %i: número entero
console.log("Edad: %d años", 30);     // Edad: 30 años

// %f: número decimal
console.log("Pi: %f", 3.14);          // Pi: 3.140000

// %o: objeto
console.log("Usuario: %o", { nombre: "Juan" });
```

#### **Estilos CSS en consola**

```javascript
// Solo en navegadores, no en Node.js
console.log("%cTexto rojo y grande", "color: red; font-size: 20px;");
console.log("%cÉxito", "color: green; font-weight: bold;");
```

#### _**Template strings**_**&#x20;en consola**

```javascript
let nombre = "Juan";
let edad = 30;

console.log(`${nombre} tiene ${edad} años`);
console.log(`Usuario: ${nombre} (${typeof nombre})`);
```

***

### 4.7. `console.table()` y Otros Métodos Útiles

#### **`console.table()`**

Visualiza arrays y objetos como tabla:

```javascript
let usuarios = [
    { nombre: "Juan", edad: 30 },
    { nombre: "María", edad: 25 },
    { nombre: "Carlos", edad: 35 }
];

console.table(usuarios);
// Muestra en formato tabla

// Con objetos
let persona = { nombre: "Juan", edad: 30, ciudad: "Madrid" };
console.table(persona);
```

#### **`console.group()` y `console.groupEnd()`**

Agrupa mensajes relacionados:

```javascript
console.group("Información del Usuario");
console.log("Nombre: Juan");
console.log("Edad: 30");
console.log("Ciudad: Madrid");
console.groupEnd();

// Grupos anidados
console.group("Nivel 1");
    console.group("Nivel 2");
        console.log("Mensaje profundo");
    console.groupEnd();
console.groupEnd();
```

#### **`console.time()` y `console.timeEnd()`**

Mide el tiempo de ejecución:

```javascript
console.time("bucle");
for (let i = 0; i < 1000000; i++) {
    // operaciones
}
console.timeEnd("bucle");
// Output: bucle: 5.23ms (aproximado)
```

#### **`console.assert()`**

Muestra un error si la condición es falsa:

```javascript
let edad = 15;
console.assert(edad >= 18, "El usuario es menor de edad");
// Si edad < 18, muestra el mensaje de error

let resultado = 5;
console.assert(resultado === 10, "Resultado incorrecto");
```

#### **`console.count()`**

Cuenta cuántas veces se ejecuta:

```javascript
for (let i = 0; i < 5; i++) {
    console.count("iteración");
}
// iteración: 1
// iteración: 2
// iteración: 3
// iteración: 4
// iteración: 5
```

#### **`console.clear()`**

Limpia la consola:

```javascript
console.log("Texto que será borrado");
console.clear();
// La consola queda vacía
```

***

### 4.8. Buenas Prácticas con `console`

#### **No dejar `console.log()` en producción**

```javascript
// Desarrollo: OK
console.log("Debug:", datos);

// Producción: Eliminar o usar logger
if (process.env.NODE_ENV === "development") {
    console.log("Debug:", datos);
}
```

#### **Usar niveles apropiados**

```javascript
// Información general
console.log("Aplicación iniciada");

// Advertencias
console.warn("Deprecated: usa nueva API");

// Errores
console.error("Error de conexión");
```

#### **Estructurar output**

```javascript
// Malo: desordenado
console.log(a);
console.log(b);
console.log(c);

// Mejor: estructurado
console.group("Resultado");
    console.log("a:", a);
    console.log("b:", b);
    console.log("c:", c);
console.groupEnd();

// Mejor aún: usar table
console.table({ a, b, c });
```

***

### Resumen del Capítulo

Las funciones de entrada de datos (`prompt`, `confirm`, `alert`) y la consola son herramientas fundamentales para interactuar con el usuario y depurar código. Aunque en producción se prefieren interfaces HTML personalizadas, estas herramientas son excelentes para prototipado y aprendizaje.

#### **💡 Conceptos Clave:**

* **prompt()**: Obtiene texto del usuario (retorna string o null)
* **confirm()**: Confirmación binaria (true o false)
* **alert()**: Notificación modal (retorna undefined)
* **console.log()**: Mostrar información
* **console.warn(), console.error()**: Niveles de gravedad
* **console.table()**: Visualizar datos estructurados
* **console.time()**: Medir rendimiento
* **console.group()**: Organizar output

#### **🤔 Preguntas de Reflexión:**

1. ¿Por qué `prompt()` siempre retorna una cadena?
2. ¿Cuál es la diferencia entre `alert()` y `console.log()`?
3. ¿Cuándo usarías `confirm()` en lugar de una simple pregunta de sí/no?
4. Explica cómo debuggearías un bucle que no funciona correctamente.
5. Escribe una función que pida datos al usuario y los valide usando `prompt()`.
6. ¿Por qué las funciones `alert()`, `prompt()` y `confirm()` son problemáticas en producción?

***
