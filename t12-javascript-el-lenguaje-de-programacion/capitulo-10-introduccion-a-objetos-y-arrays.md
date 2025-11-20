# Capítulo 10: Introducción a Objetos y Arrays

Los objetos y arrays son tipos complejos que permiten almacenar colecciones de datos. Aunque se cubrirán en profundidad en temas posteriores, aquí introducimos los conceptos fundamentales.

### 10.1. Objetos en JavaScript: Estructura Clave-Valor

Un objeto es una colección de pares clave-valor, donde cada clave es una cadena y el valor puede ser cualquier tipo.

```javascript
let persona = {
    nombre: "Juan",
    edad: 30,
    ciudad: "Madrid",
    activo: true
};

console.log(typeof persona);      // "object"
```

***

### 10.2. Creación de Objetos: Sintaxis Literal

La forma más común es usar literal de objeto `{}`.

```javascript
let libro = {
    titulo: "Clean Code",
    autor: "Robert C. Martin",
    año: 2008,
    paginas: 464
};

console.log(libro);
```

***

### 10.3. Acceso a Propiedades

#### **Notación de punto**

```javascript
let usuario = { nombre: "Ana", edad: 25 };
console.log(usuario.nombre);    // "Ana"
console.log(usuario.edad);      // 25
```

#### **Notación de corchetes**

```javascript
console.log(usuario["nombre"]); // "Ana"
console.log(usuario["edad"]);   // 25

// Útil cuando la clave es una variable
let propiedad = "nombre";
console.log(usuario[propiedad]); // "Ana"
```

***

### 10.4. Adición y Modificación de Propiedades

```javascript
let coche = { marca: "Toyota", modelo: "Corolla" };

// Modificar
coche.año = 2023;
coche["color"] = "azul";

console.log(coche);
// { marca: 'Toyota', modelo: 'Corolla', año: 2023, color: 'azul' }

// Eliminar
delete coche.color;
console.log(coche);
// { marca: 'Toyota', modelo: 'Corolla', año: 2023 }
```

***

### 10.5. Arrays: Creación y Acceso a Elementos

Los arrays son objetos especializados que almacenan colecciones ordenadas.

```javascript
let frutas = ["manzana", "plátano", "naranja"];
console.log(typeof frutas);      // "object"
console.log(Array.isArray(frutas)); // true

// Acceso por índice
console.log(frutas[0]);          // "manzana"
console.log(frutas.length);      // 3
```

***

### 10.6. Métodos Básicos de Arrays

#### **`push()` y `pop()`**

```javascript
let numeros = [1, 2, 3];

numeros.push(4);                 // Añade al final
console.log(numeros);            // [1, 2, 3, 4]

let ultimo = numeros.pop();      // Extrae el último
console.log(ultimo);             // 4
console.log(numeros);            // [1, 2, 3]
```

#### **`shift()` y `unshift()`**

```javascript
let cola = [1, 2, 3];

let primero = cola.shift();      // Extrae el primero
console.log(primero);            // 1
console.log(cola);               // [2, 3]

cola.unshift(0);                 // Añade al inicio
console.log(cola);               // [0, 2, 3]
```

***

### 10.7. Iteración sobre Arrays

#### **Con `for` tradicional**

```javascript
let nombres = ["Juan", "María", "Carlos"];

for (let i = 0; i < nombres.length; i++) {
    console.log(nombres[i]);
}
```

#### **Con `for-of`**

```javascript
for (const nombre of nombres) {
    console.log(nombre);
}
```

#### **Con `forEach()`**

```javascript
nombres.forEach(function(nombre) {
    console.log(nombre);
});

// Con arrow function
nombres.forEach(nombre => console.log(nombre));
```

***

### 10.8. Diferencias entre Objetos y Arrays

| Aspecto      | Objeto                | Array                                             |
| ------------ | --------------------- | ------------------------------------------------- |
| **Acceso**   | Propiedades (nombres) | Índices (números)                                 |
| **Orden**    | No garantizado        | Ordenado                                          |
| **Tipo**     | `typeof` = "object"   | `typeof` = "object" (pero Array.isArray() = true) |
| **Longitud** | Requiere calcular     | Propiedad `.length`                               |
| **Métodos**  | Personalizados        | Integrados (push, pop, etc.)                      |

```javascript
// Objeto
let persona = { nombre: "Juan", edad: 30 };
console.log(Object.keys(persona)); // ["nombre", "edad"]

// Array
let numeros = [10, 20, 30];
console.log(numeros.length);       // 3
```

***

### Resumen del Capítulo

Los objetos y arrays son las estructuras de datos fundamentales en JavaScript. Aunque los exploraremos en profundidad más adelante, estos conceptos básicos son esenciales para cualquier programador.

#### **💡 Conceptos Clave:**

* **Objetos**: Colecciones clave-valor con propiedades
* **Arrays**: Colecciones ordenadas con índices
* **Notación punto vs corchetes**: Acceso a propiedades
* **Métodos básicos**: push, pop, shift, unshift
* **Iteración**: for, for-of, forEach
* **typeof vs Array.isArray()**: Diferencia en detección

#### **🤔 Preguntas de Reflexión:**

1. ¿Cuándo usarías un objeto en lugar de un array?
2. ¿Cuál es la diferencia entre shift() y pop()?
3. ¿Por qué Arrays son técnicamente objetos?
4. Crea un objeto que represente a un estudiante con múltiples propiedades.

***
