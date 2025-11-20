# Capítulo 7: Introducción a Funciones

Las funciones son bloques de código reutilizables que realizan una tarea específica. Son fundamentales para escribir código modular, legible y mantenible. En este capítulo, exploraremos cómo crear y usar funciones en JavaScript.

### 7.1. ¿Qué es una Función?

Una función es un conjunto de instrucciones agrupadas que se ejecutan como una unidad. Las funciones permiten **reutilizar código** sin reescribirlo constantemente.

```javascript
// Sin función: código repetido
console.log("Hola, Juan");
console.log("Hola, María");
console.log("Hola, Carlos");

// Con función: código reutilizable
function saludar(nombre) {
    console.log(`Hola, ${nombre}`);
}

saludar("Juan");                // Hola, Juan
saludar("María");               // Hola, María
saludar("Carlos");              // Hola, Carlos
```

***

### 7.2. Declaración de Funciones: _`function declaration`_  &#x20;

La forma clásica de declarar una función.

```javascript
function suma(a, b) {
    return a + b;
}

console.log(suma(3, 5));        // 8
```

#### **Parámetros y argumentos**

* **Parámetros**: Variables en la definición
* **Argumentos**: Valores pasados al llamar

```javascript
function multiplicar(x, y) {    // x, y son parámetros
    return x * y;
}

console.log(multiplicar(4, 5)); // 4, 5 son argumentos
```

#### **Valores por defecto**

```javascript
function saludar(nombre = "Visitante") {
    console.log(`Hola, ${nombre}`);
}

saludar();                      // Hola, Visitante
saludar("Ana");                 // Hola, Ana
```

#### **Hoisting de funciones**

Las _function declarations_ se elevan completamente, puedes llamarlas antes de declararlas.

```javascript
console.log(suma(2, 3));        // Funciona: 5

function suma(a, b) {
    return a + b;
}
```

***

### 7.3. _`Function Expressions`_: Funciones Anónimas

Asignar una función a una variable. La función no tiene hoisting.

```javascript
// Sin nombre (anónima)
const restar = function(a, b) {
    return a - b;
};

console.log(restar(10, 3));     // 7

// Con nombre (útil para recursión)
const factorial = function calcularFactorial(n) {
    if (n <= 1) return 1;
    return n * calcularFactorial(n - 1);
};
```

#### **No tiene hoisting**

```javascript
console.log(restar(5, 2));      // ReferenceError: Cannot access 'restar' before initialization

const restar = function(a, b) {
    return a - b;
};
```

***

### 7.4. _`Arrow Functions`_: Sintaxis Moderna (ES6+)

Las arrow functions proporcionan una sintaxis más concisa introducida en ES6.

```javascript
// Sintaxis básica
const sumar = (a, b) => {
    return a + b;
};

console.log(sumar(2, 3));       // 5

// Un parámetro: paréntesis opcionales
const doble = x => {
    return x * 2;
};

console.log(doble(5));          // 10

// Sin parámetros: paréntesis vacíos
const saludo = () => {
    console.log("¡Hola!");
};

saludo();
```

#### **Return implícito en una línea**

```javascript
const sumar = (a, b) => a + b;  // Return implícito
console.log(sumar(3, 4));       // 7

const doble = x => x * 2;
console.log(doble(5));          // 10

// Para retornar un objeto, usa paréntesis
const crearUsuario = nombre => ({ nombre, edad: 18 });
console.log(crearUsuario("Juan")); // { nombre: 'Juan', edad: 18 }
```

#### **`this` en&#x20;**_**arrow functions**_

Las arrow functions no tienen su propio `this`, heredan del contexto externo (importante en POO).

```javascript
const persona = {
    nombre: "Juan",
    saludar: function() {
        console.log(this.nombre); // "Juan"
    },
    saludarFlecha: () => {
        console.log(this.nombre); // undefined (this no se refiere a persona)
    }
};
```

***

### 7.5. Parámetros, Argumentos y Valores por Defecto

#### **Argumentos extras se ignoran**

```javascript
function sumar(a, b) {
    return a + b;
}

console.log(sumar(2, 3, 4, 5)); // 5 (ignora 4 y 5)
```

#### **Argumentos faltantes son undefined**

```javascript
function restar(a, b) {
    console.log(a, b);          // 5, undefined
    return a - b;               // 5 - undefined = NaN
}

console.log(restar(5));
```

#### **Parámetros con valores por defecto**

```javascript
function descuento(precio, porcentaje = 0.1) {
    return precio * (1 - porcentaje);
}

console.log(descuento(100));        // 90 (10% por defecto)
console.log(descuento(100, 0.2));   // 80 (20%)
```

#### _**`Rest parameters`**_**: capturar argumentos restantes**

```javascript
function sumarTodos(...numeros) {   // ...numeros recibe un array
    let total = 0;
    for (const num of numeros) {
        total += num;
    }
    return total;
}

console.log(sumarTodos(1, 2, 3, 4, 5)); // 15

// Combinar parámetros regulares con rest
function presentar(nombre, ...hobbies) {
    console.log(`${nombre} disfruta: ${hobbies.join(", ")}`);
}

presentar("Juan", "leer", "programar", "jugar"); 
// Juan disfruta: leer, programar, jugar
```

***

### 7.6. La Sentencia `return`

`return` finaliza la función y retorna un valor.

```javascript
function verificarEdad(edad) {
    if (edad >= 18) {
        return "Mayor de edad";
    }
    return "Menor de edad";      // Se ejecuta si la primera no lo hace
}

console.log(verificarEdad(25));  // "Mayor de edad"

// Sin return explícito, retorna undefined
function sinRetorno() {
    console.log("Haciendo algo");
}

console.log(sinRetorno());       // undefined
```

#### **Return múltiple**

```javascript
function validarEmail(email) {
    if (!email.includes("@")) {
        return false;
    }
    if (email.length < 5) {
        return false;
    }
    return true;
}
```

***

### 7.7. Scope y Closures

El **scope** define dónde una variable es accesible.

```javascript
let global = "Soy global";

function externa() {
    let local = "Soy local";
    console.log(global);        // Accede a global
    console.log(local);         // Accede a local
}

console.log(global);            // ✓ Funciona
console.log(local);             // ✗ ReferenceError
```

#### **Closures: funciones que recuerdan su contexto**

Una **closure** es una función que accede a variables de su scope externo, incluso después de que la función externa ha terminado.

```javascript
function crear_contador() {
    let contador = 0;
    return function() {
        contador++;
        return contador;
    };
}

const contador1 = crear_contador();
console.log(contador1());       // 1
console.log(contador1());       // 2
console.log(contador1());       // 3

// Cada closure tiene su propio contador
const contador2 = crear_contador();
console.log(contador2());       // 1 (independiente)
```

***

### 7.8. Recursión: Funciones que se Llaman a Sí Mismas

La **recursión** es cuando una función se llama a sí misma.

```javascript
// Factorial: 5! = 5 × 4 × 3 × 2 × 1 = 120
function factorial(n) {
    // Caso base: cuándo detener la recursión
    if (n <= 1) {
        return 1;
    }
    // Caso recursivo: llamada a sí misma
    return n * factorial(n - 1);
}

console.log(factorial(5));      // 120
```

#### **Visualizar la recursión**

```javascript
factorial(5)
= 5 * factorial(4)
= 5 * (4 * factorial(3))
= 5 * (4 * (3 * factorial(2)))
= 5 * (4 * (3 * (2 * factorial(1))))
= 5 * (4 * (3 * (2 * 1)))
= 5 * (4 * (3 * 2))
= 5 * (4 * 6)
= 5 * 24
= 120
```

#### **Fibonacci: ejemplo clásico**

```javascript
function fibonacci(n) {
    if (n <= 1) return n;
    return fibonacci(n - 1) + fibonacci(n - 2);
}

console.log(fibonacci(0));      // 0
console.log(fibonacci(1));      // 1
console.log(fibonacci(6));      // 8
```

#### **Recursión con arrays**

```javascript
function sumarArray(array, indice = 0) {
    // Caso base
    if (indice === array.length) {
        return 0;
    }
    // Caso recursivo
    return array[indice] + sumarArray(array, indice + 1);
}

console.log(sumarArray([1, 2, 3, 4, 5])); // 15
```

***

### Resumen del Capítulo

Las funciones son bloques fundamentales de la programación. Este capítulo ha cubierto declaraciones, expresiones, arrow functions, parámetros, closures y recursión. Dominar funciones es esencial para escribir código modular y mantenible.

#### **💡 Conceptos Clave:**

* **Function declaration**: Se elevan (hoisting)
* **Function expression**: No se elevan
* **Arrow functions**: Sintaxis moderna, sin `this` propio
* **Rest parameters**: Capturar múltiples argumentos
* **Return**: Termina y retorna un valor
* **Closures**: Funciones que recuerdan su contexto
* **Recursión**: Función que se llama a sí misma

#### **🤔 Preguntas de Reflexión:**

1. ¿Cuál es la diferencia entre parámetros y argumentos?
2. ¿Cuándo usarías arrow functions vs function expressions?
3. Explica qué es una closure y da un ejemplo práctico.
4. ¿Cuándo usarías recursión en lugar de un bucle?
5. Escribe una función recursiva que busque un elemento en un array anidado.

***
