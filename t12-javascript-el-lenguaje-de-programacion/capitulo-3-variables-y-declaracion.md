# Capítulo 3: Variables y Declaración

Tras lo visto en el [Tema 11](../t11-javascript-fundamentos/), donde se introdujo JavaScript en general, es momento de profundizar en cómo JavaScript gestiona las variables. Este capítulo es crítico: la forma en que declaras variables tiene implicaciones profundas para el scope, el hoisting y la calidad de tu código.

### 3.1. Declaración con `var`: Ámbito Global y Función

`var` fue la única forma de declarar variables en JavaScript durante décadas. Aunque funciona, tiene características sorprendentes que la hacen menos segura que `let` y `const`.

```javascript
var nombre = "Juan";
console.log(nombre);            // "Juan"

var edad = 30;
edad = 31;                       // Permite reasignación
console.log(edad);              // 31
```

#### **Scope de `var`: Función, no bloque**

A diferencia de otros lenguajes, `var` tiene _**function scope**_, no _block scope_. Esto significa que una variable declarada con `var` dentro de un `if` o `for` es visible fuera de ese bloque.

```javascript
function ejemplo() {
    if (true) {
        var x = 10;
    }
    console.log(x);             // 10 (visible fuera del if!)
}

for (var i = 0; i < 3; i++) {
    // i es variable de función, no de bucle
}
console.log(i);                 // 3 (visible fuera del for!)
```

Esta característica puede causar errores sutiles y es una de las razones por las que `let` y `const` son preferibles.

#### **`var` en&#x20;**_**global scope**_

Cuando declaras `var` a nivel global (fuera de cualquier función), la variable se convierte en propiedad del objeto global.

```javascript
var global_var = "Soy global";

// En el navegador:
console.log(window.global_var);  // "Soy global"

// En Node.js:
console.log(global.global_var);  // "Soy global"
```

***

### 3.2. Declaración con `let`: Ámbito de Bloque

`let`, introducida en ES6, es la forma moderna de declarar variables. Tiene _**block scope**_, lo que significa que solo existe dentro del bloque donde se declara.

```javascript
function ejemplo() {
    if (true) {
        let x = 10;
    }
    console.log(x);             // ReferenceError: x is not defined
}
```

#### _**Block scope**_**&#x20;en acción**

```javascript
for (let i = 0; i < 3; i++) {
    console.log(i);             // 0, 1, 2
}
console.log(i);                 // ReferenceError: i is not defined

// Cada iteración tiene su propio 'i'
for (let i = 0; i < 3; i++) {
    setTimeout(() => {
        console.log(i);         // 0, 1, 2 (correcto con let)
    }, 100);
}
```

Compáralo con `var`:

```javascript
for (var i = 0; i < 3; i++) {
    setTimeout(() => {
        console.log(i);         // 3, 3, 3 (todas imprimem 3)
    }, 100);
}
```

#### **`let` en bucles anidados**

```javascript
let x = "global";

{
    let x = "en el bloque";
    console.log(x);             // "en el bloque" (sombreado)
}

console.log(x);                 // "global"
```

***

### 3.3. Declaración con `const`: Inmutabilidad Aparente

`const` declara una variable que no puede ser **reasignada**. No significa que el valor sea inmutable (especialmente para objetos), sino que la referencia no cambia.

```javascript
const PI = 3.14159;
console.log(PI);                // 3.14159

PI = 3.14;                      // TypeError: Assignment to constant variable
```

#### **`const` con objetos: Mutable**

```javascript
const usuario = { nombre: "Juan", edad: 30 };

// Puedo modificar propiedades (la referencia es la misma)
usuario.edad = 31;
console.log(usuario);           // { nombre: "Juan", edad: 31 }

// No puedo reasignar el objeto completo
usuario = { nombre: "María" };  // TypeError
```

#### **`const` con arrays: Mutable**

```javascript
const numeros = [1, 2, 3];

// Puedo modificar elementos
numeros[0] = 10;
numeros.push(4);
console.log(numeros);           // [10, 2, 3, 4]

// No puedo reasignar el array
numeros = [5, 6, 7];           // TypeError
```

#### **Cuándo usar const, let y var**

| Declarador | Cuándo usarlo              | Razón                                 |
| ---------- | -------------------------- | ------------------------------------- |
| `const`    | Por defecto                | Previene reasignación accidental      |
| `let`      | Cuando necesites reasignar | Mejor scope que var                   |
| `var`      | Raramente                  | _Legacy_, comportamiento impredecible |

{% hint style="success" %}
**Recomendación moderna**: Usa `const` por defecto, `let` cuando necesites reasignar, nunca `var`.
{% endhint %}

***

### 3.4. Hoisting: Comportamiento de las Declaraciones

El **hoisting** es el comportamiento de JavaScript de "elevar" las declaraciones al inicio de su scope antes de ejecutar el código.

#### **`var` hoisting**

```javascript
console.log(x);                 // undefined (no ReferenceError)
var x = 5;
console.log(x);                 // 5

// JavaScript realmente hace esto:
// var x;
// console.log(x);              // undefined
// x = 5;
// console.log(x);              // 5
```

#### **`let` y `const`: Temporal Dead Zone (TDZ)**

`let` y `const` se elevan, pero **no se inicializan**, creando la **Temporal Dead Zone**.

```javascript
console.log(y);                 // ReferenceError: Cannot access 'y' before initialization
let y = 5;

// Existe una zona entre el inicio del scope y la declaración
{
    // TDZ comienza aquí
    console.log(z);             // ReferenceError
    let z = 10;
    // TDZ termina aquí
}
```

#### **Hoisting de funciones**

```javascript
console.log(saludar("Juan"));   // "Hola, Juan" (funciona)

function saludar(nombre) {
    return `Hola, ${nombre}`;
}

// Las function declarations se elevan completamente
```

Pero las _function expressions_ no:

```javascript
console.log(saludar("Juan"));   // TypeError: saludar is not a function

var saludar = function(nombre) {
    return `Hola, ${nombre}`;
};
```

***

### 3.5. Identificadores Válidos y Buenas Prácticas

Los nombres de variables deben seguir reglas específicas y convenciones.

#### **Reglas para identificadores**

* Comienzan con una letra, `_` (guión bajo) o `$` (dólar)
* Pueden contener números, pero no al inicio
* No pueden ser palabras reservadas de JavaScript
* Son sensibles a mayúsculas (case-sensitive)

```javascript
// Válidos
let nombre;
let _privado;
let $jquery;
let usuario123;
let MayúsculasYminúsculas;

// Inválidos
let 123usuario;             // SyntaxError
let nombre-usuario;         // SyntaxError (el guión es un operador)
let function;               // SyntaxError (palabra reservada)
```

#### **Convención: camelCase**

JavaScript usa **camelCase** para nombrar variables y funciones:

```javascript
// Buen estilo
let nombreUsuario;
let ageInYears;
let esMayorDeEdad;
let obtenerDatosDelServidor;

// Evitar
let nombre_usuario;        // snake_case (Python style)
let NombreUsuario;         // PascalCase (para clases)
let NOMBREUSUARIO;         // UPPER_CASE (para constantes)
```

#### **Nombres significativos**

```javascript
// Malo: nombres crípticos
let u = "Juan";
let a = 30;
let d = new Date();

// Bueno: nombres descriptivos
let usuario = "Juan";
let edad = 30;
let fechaRegistro = new Date();
```

***

### 3.6. Case-Sensitivity en JavaScript

JavaScript es **case-sensitive**: `nombre`, `Nombre` y `NOMBRE` son variables diferentes.

```javascript
let nombre = "Juan";
let Nombre = "María";
let NOMBRE = "Carlos";

console.log(nombre);        // "Juan"
console.log(Nombre);        // "María"
console.log(NOMBRE);        // "Carlos"

// Los tipos también son case-sensitive
console.log(typeof nombre); // "string"
// console.log(typeof String); // "function" (la clase String)
```

***

### 3.7. Temporal Dead Zone (TDZ)

La **Temporal Dead Zone** es el área entre el inicio del scope y donde se declara una variable con `let` o `const`.

```javascript
function ejemplo() {
    // TDZ comienza
    console.log(x);         // ReferenceError
    let x = 10;
    // TDZ termina
    console.log(x);         // 10
}
```

Incluso si hay una variable con el mismo nombre en un scope externo, la TDZ la oscurece:

```javascript
let x = "global";

{
    // Aquí, x está en TDZ (aunque existe globalmente)
    console.log(x);         // ReferenceError
    let x = "local";
}
```

***

### Resumen del Capítulo

Las variables son los bloques constructivos del código. Comprender las diferencias entre `var`, `let` y `const`, así como cómo JavaScript gestiona el scope y el hoisting, es fundamental para escribir código limpio y sin errores.

#### **💡 Conceptos Clave:**

* **var**: Function scope, hoisting completo (inicialización a undefined)
* **let**: Block scope, hoisting sin inicialización (Temporal Dead Zone)
* **const**: Block scope, no reasignación (pero objetos son mutables)
* **Preferencia moderna**: `const` por defecto, `let` cuando sea necesario
* **Hoisting**: var se eleva completamente, let/const crean TDZ
* **Case-sensitivity**: Variables con distinto caso son diferentes
* **camelCase**: Convención estándar de nombres en JavaScript

#### **🤔 Preguntas de Reflexión:**

1. ¿Por qué es peligroso `var` en bucles? Demuéstalo con un ejemplo práctico.
2. Explica la diferencia entre "no poder reasignar" y "ser inmutable". Da ejemplos con const.
3. ¿Qué es la Temporal Dead Zone? ¿Por qué existe?
4.  Convierte este código de `var` a `let`/`const` de forma segura:

    ```javascript
    for (var i = 0; i < 5; i++) {
        setTimeout(() => console.log(i), 100);
    }
    ```

***
