# Capítulo 1: Tipos de Datos

JavaScript es un lenguaje **dinámicamente tipado**, lo que significa que las variables no están vinculadas a un tipo específico en el momento de la declaración. Esta característica otorga una flexibilidad poderosa al lenguaje, pero también requiere comprensión para evitar errores sutiles. En este capítulo, exploraremos los pilares de los tipos de datos en JavaScript y cómo el lenguaje maneja las conversiones entre ellos.

### 1.1. Tipado Dinámico y Debilidad de Tipos

A diferencia de lenguajes como Java o C++, donde debes declarar explícitamente el tipo de una variable, JavaScript permite que una variable cambie de tipo durante su ejecución. Esta característica se denomina **tipado dinámico**.

```javascript
let valor = 42;           // Número
console.log(typeof valor); // "number"

valor = "Hola mundo";      // Ahora es una cadena
console.log(typeof valor); // "string"

valor = true;              // Ahora es un booleano
console.log(typeof valor); // "boolean"
```

JavaScript también es un lenguaje **débilmente tipado**, lo que significa que el lenguaje intentará realizar conversiones automáticas (coerción) entre tipos cuando sea necesario, incluso si esto puede llevar a comportamientos inesperados.

```javascript
console.log("5" + 3);      // "53" (concatenación, no suma)
console.log("5" - 3);      // 2 (conversión a número)
console.log(true + 1);     // 2 (true se convierte a 1)
```

***

### 1.2. Tipos Primitivos

JavaScript tiene **7 tipos primitivos** (también llamados tipos básicos). Los primitivos son valores que no son objetos y no tienen métodos propios, aunque JavaScript te permite acceder a métodos como si fueran objetos gracias al **autoboxing**.

#### **number**

Representa números, tanto enteros como decimales. A diferencia de otros lenguajes, JavaScript no distingue entre enteros y decimales; todos son del tipo `number`.

```javascript
let entero = 42;
let decimal = 3.14;
let negativo = -10;
let notacion_cientifica = 1.23e2; // 123
let infinito = Infinity;
let menos_infinito = -Infinity;
let indefinido_numerico = NaN;    // Not-a-Number
```

**Precisión de punto flotante**: Los números en JavaScript se representan según el estándar IEEE 754 (64 bits), lo que ocasiona problemas de precisión con decimales.

```javascript
console.log(0.1 + 0.2);           // 0.30000000000000004
console.log(0.1 + 0.2 === 0.3);   // false (¡sorpresa!)

// Solución: usar un margen de tolerancia
const EPSILON = 0.0001;
console.log(Math.abs((0.1 + 0.2) - 0.3) < EPSILON); // true
```

#### **string**

Representa texto. Las cadenas pueden delimitarse con comillas simples, dobles o comillas invertidas (_template strings_).

```javascript
let cadena1 = "Hola";
let cadena2 = 'Mundo';
let cadena3 = `Hola ${cadena2}`; // Template literal con interpolación

// Las cadenas son inmutables
let original = "JavaScript";
console.log(original[0]);         // "J"
console.log(original.length);     // 10
```

#### **boolean**

Representa un valor lógico: `true` o `false`. Es fundamental para estructuras de control como `if` y bucles.

```javascript
let activo = true;
let completado = false;

// Los booleanos se usan en condiciones
if (activo) {
    console.log("Activo");
}
```

#### **symbol**

Introducido en ES6, `symbol` crea identificadores únicos. Cada símbolo es diferente de cualquier otro, incluso si se crean con la misma descripción.

```javascript
const id1 = Symbol("identificador");
const id2 = Symbol("identificador");

console.log(id1 === id2);        // false (símbolos únicos)

// Los símbolos se usan como propiedades privadas de objetos
const usuario = {
    [id1]: "Admin"
};
```

#### **bigint**

Introducido en ES2020, permite trabajar con enteros arbitrariamente grandes, más allá del límite de `number` (2^53 - 1).

```javascript
let numero_grande = 1n;  // El sufijo 'n' indica BigInt
let otro_grande = BigInt("9007199254740992");

console.log(numero_grande + 1n);  // Funciona
// console.log(numero_grande + 1); // ERROR: no puedes mezclar number y BigInt
```

#### **undefined**

Significa que una variable ha sido declarada pero no asignada, o una función no retorna explícitamente un valor.

```javascript
let x;
console.log(x);                    // undefined

function sin_retorno() {}
console.log(sin_retorno());        // undefined

function con_retorno() {
    return;
}
console.log(con_retorno());        // undefined
```

#### **null**

Representa la **ausencia intencional** de un valor. A diferencia de `undefined`, `null` debe asignarse explícitamente. Es un valor que el programador usa para indicar "sin valor".

```javascript
let dato = null;                   // Intención explícita
console.log(typeof null);          // "object" (¡esto es un bug histórico!)

// null y undefined son "falsy"
if (!null) console.log("null es falsy");
if (!undefined) console.log("undefined es falsy");
```

{% hint style="info" %}
**Diferencia clave**: `undefined` es asignado automáticamente; `null` se asigna deliberadamente.



```javascript
console.log(null === undefined);   // false (diferente tipo)
console.log(null == undefined);    // true (igualdad flexible)
```
{% endhint %}

***

### 1.3. Tipos Complejos: `Object` y `Array`

#### **Object**

Los objetos son colecciones de pares clave-valor. Aunque los exploraremos en profundidad más adelante, es importante reconocer que casi todo en JavaScript es un objeto.

```javascript
let persona = {
    nombre: "Juan",
    edad: 30,
    activo: true
};

console.log(typeof persona);      // "object"
console.log(persona.nombre);      // "Juan"
```

#### **Array**

Los arrays son un tipo especial de objeto que almacena colecciones ordenadas de valores. Se accede a sus elementos mediante índices numéricos.

```javascript
let numeros = [1, 2, 3, 4, 5];
console.log(typeof numeros);      // "object" (los arrays son objetos)
console.log(numeros[0]);          // 1
console.log(numeros.length);      // 5
```

***

### 1.4. El Operador `typeof` y Detección de Tipos

El operador `typeof` retorna una cadena indicando el tipo de una variable.

```javascript
console.log(typeof 42);           // "number"
console.log(typeof "texto");      // "string"
console.log(typeof true);         // "boolean"
console.log(typeof undefined);    // "undefined"
console.log(typeof Symbol("id")); // "symbol"
console.log(typeof 42n);          // "bigint"

// ¡Cuidado con estos!
console.log(typeof {});           // "object"
console.log(typeof []);           // "object"
console.log(typeof null);         // "object" (bug histórico)
console.log(typeof function(){}); // "function"
```

Para diferenciar entre `null` y objetos reales, usa una comparación explícita:

```javascript
let valor = null;
if (typeof valor === "object" && valor !== null) {
    console.log("Es un objeto real");
} else if (valor === null) {
    console.log("Es null");
}
```

***

### 1.5. Coerción de Tipos

La coerción es la conversión automática entre tipos. JavaScript realiza coerciones frecuentemente, a veces de manera sorprendente.

#### **Coerción implícita**

El operador `+` es ambiguo: puede sumar números o concatenar cadenas.

```javascript
console.log(5 + 3);               // 8 (suma numérica)
console.log("5" + 3);             // "53" (concatenación)
console.log(3 + "5");             // "35" (la cadena gana)
console.log("5" - 3);             // 2 (resta fuerza número)
console.log("5" * "2");           // 10 (multiplicación fuerza números)
```

Reglas de coerción:

* Si uno de los operandos de `+` es una cadena, ambos se convierten a cadena.
* Para otros operadores aritméticos, se convierten a número.

#### **Valores&#x20;**_**truthy**_**&#x20;y&#x20;**_**falsy**_

En contextos booleanos, ciertos valores se convierten a `false` (**falsy**) y otros a `true` (**truthy**).

**Falsy**: `0`, `""` (cadena vacía), `null`, `undefined`, `NaN`, `false`&#x20;

**Truthy**: Cualquier otro valor (incluyendo `"0"`, `[]`, `{}`)

```javascript
if (0) console.log("Esto no se ejecuta");
if ("0") console.log("Esto sí se ejecuta");
if ([]) console.log("Arrays vacios son truthy");
if ({}) console.log("Objetos vacios son truthy");
```

#### **Coerción explícita**

Convierte tipos de forma deliberada y clara:

```javascript
// A número
console.log(Number("42"));         // 42
console.log(parseInt("42px"));     // 42 (ignora caracteres no numéricos)
console.log(parseFloat("3.14"));   // 3.14
console.log(+"42");                // 42 (operador unario +)
console.log(Boolean(1));           // true

// A cadena
console.log(String(42));           // "42"
console.log((42).toString());      // "42"
console.log(`${42}`);              // "42" (template literal)
```

***

### Resumen del Capítulo

Este capítulo ha introducido los tipos de datos fundamentales de JavaScript: los 7 tipos primitivos (number, string, boolean, symbol, bigint, undefined, null) y los tipos complejos (object, array). Comprender que JavaScript es dinámicamente tipado y débilmente tipado es crucial para evitar errores sutiles derivados de coerciones inesperadas.

#### **💡 Conceptos Clave:**

* **Tipado dinámico**: Las variables pueden cambiar de tipo durante la ejecución
* **Siete tipos primitivos**: number, string, boolean, symbol, bigint, undefined, null
* **null vs undefined**: null es intencional, undefined es automático
* **typeof operator**: Detecta tipos, pero ten cuidado con null y arrays
* **Coerción**: Conversiones automáticas (implícitas) y deliberadas (explícitas)
* **Truthy/Falsy**: Comportamiento en contextos booleanos
* **Autoboxing**: Acceso a métodos en primitivos mediante envoltura automática

#### **🤔 Preguntas de Reflexión:**

1. ¿Por qué crees que `typeof null` retorna `"object"` si `null` no es un objeto? ¿Cómo impactaría en tu código?
2. Explica con tus palabras la diferencia entre `undefined` y `null`. ¿Cuándo usarías cada uno?
3. ¿Qué ventajas y desventajas tiene que JavaScript sea débilmente tipado?
4. Dado `"10" + 5 - 3`, ¿cuál será el resultado? Explica paso a paso cómo JavaScript lo evalúa.
5. ¿Cuándo preferirías usar `Number()` vs `parseInt()` para convertir a número?
6. Diseña un sistema de validación que determine si un valor es un "booleano verdadero" (no solo truthy).

***
