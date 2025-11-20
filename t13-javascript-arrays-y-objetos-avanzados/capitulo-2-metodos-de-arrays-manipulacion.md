# Capítulo 2: Métodos de Arrays - Manipulación

Este capítulo continúa explorando los métodos de arrays, enfocándose en manipulación directa de arrays: cómo modificarlos, extraer porciones, combinar y reordenar.

### 2.1. `push()`, `pop()`, `shift()`, `unshift()`

Estos métodos modifican el array original.

```javascript
let numeros = [1, 2, 3];

// push(): añade al final
numeros.push(4, 5);
console.log(numeros); // [1, 2, 3, 4, 5]

// pop(): extrae y retorna el último
let ultimo = numeros.pop();
console.log(ultimo);  // 5
console.log(numeros); // [1, 2, 3, 4]

// shift(): extrae y retorna el primero
let primero = numeros.shift();
console.log(primero); // 1
console.log(numeros); // [2, 3, 4]

// unshift(): añade al inicio
numeros.unshift(0, 1);
console.log(numeros); // [0, 1, 2, 3, 4]
```

#### **Retorno de valores:**

```javascript
let arr = [1, 2];

console.log(arr.push(3));    // 3 (nueva longitud)
console.log(arr.pop());      // 3 (valor extraído)
console.log(arr.shift());    // 1 (valor extraído)
console.log(arr.unshift(0)); // 2 (nueva longitud)
```

***

### 2.2. `splice()`: Insertar y Eliminar Elementos

`splice()` modifica el array original eliminando y/o insertando elementos.

**Sintaxis**: `array.splice(índice_inicio, cantidad_a_eliminar, ...elementos_a_insertar)`

```javascript
let frutas = ["manzana", "plátano", "naranja", "fresa"];

// Eliminar 2 elementos comenzando en índice 1
let eliminadas = frutas.splice(1, 2);
console.log(eliminadas);  // ["plátano", "naranja"]
console.log(frutas);      // ["manzana", "fresa"]

// Insertar sin eliminar (cantidad = 0)
frutas.splice(1, 0, "piña", "mango");
console.log(frutas); // ["manzana", "piña", "mango", "fresa"]

// Reemplazar: eliminar 1, insertar 2
frutas.splice(2, 1, "pera", "uva");
console.log(frutas); // ["manzana", "piña", "pera", "uva", "fresa"]

// Índices negativos (desde el final)
let numeros = [1, 2, 3, 4, 5];
numeros.splice(-2, 1); // Elimina un elemento 2 posiciones desde el final
console.log(numeros); // [1, 2, 3, 5]
```

***

### 2.3. `slice()`: Extraer Porciones sin Modificar

`slice()` retorna una **copia** de una porción sin modificar el original.

```javascript
let numeros = [1, 2, 3, 4, 5];

// Extraer elementos del índice 1 al 3 (no incluye 3)
let copia = numeros.slice(1, 3);
console.log(copia);  // [2, 3]
console.log(numeros); // [1, 2, 3, 4, 5] (sin cambios)

// Desde índice al final
let desde2 = numeros.slice(2);
console.log(desde2); // [3, 4, 5]

// Últimos N elementos
let ultimos2 = numeros.slice(-2);
console.log(ultimos2); // [4, 5]

// Copia completa
let copia_completa = numeros.slice();
console.log(copia_completa); // [1, 2, 3, 4, 5]
```

***

### 2.4. `concat()`: Combinar Arrays

```javascript
let array1 = [1, 2, 3];
let array2 = [4, 5];
let array3 = [6, 7];

// Combinar múltiples arrays
let combinado = array1.concat(array2, array3);
console.log(combinado); // [1, 2, 3, 4, 5, 6, 7]

// Original no cambia
console.log(array1); // [1, 2, 3]

// Combinar arrays y valores
let resultado = array1.concat(99, array2, 100);
console.log(resultado); // [1, 2, 3, 99, 4, 5, 100]
```

***

### 2.5. `join()` y `split()`: Convertir entre Arrays y Strings

#### **`join()`: Array → String**

```javascript
let frutas = ["manzana", "plátano", "naranja"];

let cadena1 = frutas.join();        // "manzana,plátano,naranja"
let cadena2 = frutas.join(" - ");   // "manzana - plátano - naranja"
let cadena3 = frutas.join("");      // "manzanaplátanonaranja"
let cadena4 = frutas.join("\n");    // multiline

// Path o URL
let ruta = ["home", "documents", "archivo.txt"];
console.log(ruta.join("/")); // "home/documents/archivo.txt"
```

#### **`split()`: String → Array (método de String)**

```javascript
let texto = "JavaScript es poderoso";
let palabras = texto.split(" ");
console.log(palabras); // ["JavaScript", "es", "poderoso"]

let csv = "Juan,30,Madrid,Ingeniero";
let datos = csv.split(",");
console.log(datos); // ["Juan", "30", "Madrid", "Ingeniero"]

// Split sin argumento
let cadena = "abc";
let caracteres = cadena.split("");
console.log(caracteres); // ["a", "b", "c"]
```

***

### 2.6. `reverse()` y `sort()`&#x20;

#### **`reverse()`: Invertir orden**

```javascript
let numeros = [1, 2, 3, 4, 5];
numeros.reverse();
console.log(numeros); // [5, 4, 3, 2, 1]

// reverse() muta el array original
let palabras = ["hola", "mundo"];
palabras.reverse();
console.log(palabras); // ["mundo", "hola"]
```

#### **`sort()`: Ordenar (¡cuidado!)**

```javascript
// Sort por defecto ordena como strings
let numeros = [10, 5, 40, 25];
numeros.sort();
console.log(numeros); // [10, 25, 40, 5] (¡incorrecto!)

// Solución: función comparadora
numeros.sort((a, b) => a - b); // Ascendente
console.log(numeros); // [5, 10, 25, 40]

numeros.sort((a, b) => b - a); // Descendente
console.log(numeros); // [40, 25, 10, 5]

// Sort con strings
let palabras = ["zebra", "apple", "mango"];
palabras.sort();
console.log(palabras); // ["apple", "mango", "zebra"]

// Sort de objetos
let usuarios = [
    { nombre: "Juan", edad: 30 },
    { nombre: "María", edad: 25 },
    { nombre: "Carlos", edad: 35 }
];

usuarios.sort((a, b) => a.edad - b.edad);
console.log(usuarios); // Ordenado por edad
```

***

### 2.7. `includes()`: Buscar Existencia

```javascript
let numeros = [1, 2, 3, 4, 5];

console.log(numeros.includes(3));    // true
console.log(numeros.includes(10));   // false

// Con strings
let frutas = ["manzana", "plátano", "naranja"];
console.log(frutas.includes("plátano")); // true

// fromIndex: comenzar búsqueda desde índice
console.log(numeros.includes(2, 2)); // false (busca desde índice 2)

// Diferencia con indexOf
console.log(numeros.indexOf(3) !== -1);  // true (forma antigua)
console.log(numeros.includes(3));       // true (forma moderna)
```

***

### 2.8. `flat()` y `flatMap()`: Arrays Anidados

#### **`flat()`: Aplanar arrays anidados**

```javascript
let anidado = [1, 2, [3, 4], [5, [6, 7]]];

// Nivel 1 de profundidad
let plano1 = anidado.flat();
console.log(plano1); // [1, 2, 3, 4, 5, [6, 7]]

// Nivel 2 de profundidad
let plano2 = anidado.flat(2);
console.log(plano2); // [1, 2, 3, 4, 5, 6, 7]

// Infinito
let planoTotal = anidado.flat(Infinity);
console.log(planoTotal); // [1, 2, 3, 4, 5, 6, 7]

// Eliminar huecos
let conHuecos = [1, 2, , 4, , 6];
console.log(conHuecos.flat()); // [1, 2, 4, 6]
```

#### **`flatMap()`: `map()` + `flat()`**

```javascript
let numeros = [1, 2, 3];

// Sin flatMap: map() retorna array anidado
let resultado1 = numeros.map(n => [n, n * 2]);
console.log(resultado1); // [[1, 2], [2, 4], [3, 6]]

// Con flatMap: combina map + flat
let resultado2 = numeros.flatMap(n => [n, n * 2]);
console.log(resultado2); // [1, 2, 2, 4, 3, 6]

// Filtrar y mapear
let palabras = ["hola", "javascript"];
let resultado3 = palabras.flatMap(palabra => 
    palabra.split("")
);
console.log(resultado3); 
// ["h", "o", "l", "a", "j", "a", "v", "a", "s", "c", "r", "i", "p", "t"]
```

***

### Resumen del Capítulo

Los métodos de manipulación de arrays permiten modificar, reorganizar y transformar datos de manera eficiente. Es importante recordar que algunos mutan el array original mientras que otros crean copias.

#### **💡 Conceptos Clave:**

* **Métodos mutables**: push, pop, shift, unshift, splice, reverse, sort
* **Métodos no mutables**: slice, concat, join, flat, flatMap
* **splice()**: El más versátil para inserción y eliminación
* **slice()**: Extraer sin mutar
* **sort()**: Requiere función comparadora para números
* **flat()/flatMap()**: Aplanar y transformar arrays anidados
* **join()/split()**: Conversión string-array
* **includes()**: Búsqueda moderna vs indexOf()

#### **🤔 Preguntas de Reflexión:**

1. ¿Cuál es la diferencia entre splice() y slice()?
2. ¿Por qué sort() necesita una función comparadora para números?
3. ¿Cuándo usarías flat() vs flatMap()?
4. ¿Cómo usarías join() para crear una URL desde un array?
5. ¿Cuál es la diferencia entre mutables y no mutables?
6. Demuestra cómo aplanar un array profundamente anidado.

***
