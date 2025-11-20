# Capítulo 1: Métodos de Arrays - Iteración y Transformación

Los métodos de iteración de arrays son el corazón de la programación funcional en JavaScript. Permiten procesar colecciones de datos de manera elegante y expresiva. Este capítulo explora los métodos más poderosos y versátiles.

### 1.1. `forEach()`: Iteración con Callback

`forEach()` ejecuta una función para cada elemento del array, pero **no retorna nada** (retorna `undefined`).

```javascript
let numeros = [1, 2, 3, 4, 5];

// Iteración simple
numeros.forEach(function(numero) {
    console.log(numero * 2);
});
// Output: 2, 4, 6, 8, 10

// Con arrow function (más moderno)
numeros.forEach(num => console.log(num * 2));

// Con índice y array
numeros.forEach((num, indice, array) => {
    console.log(`Posición ${indice}: ${num}`);
});
```

#### **`forEach()` no es mutable**

```javascript
let valores = [1, 2, 3];

// Intentar retornar valores no funciona
let resultado = valores.forEach(v => v * 2);
console.log(resultado);  // undefined (forEach no retorna nada)
```

#### **Cuándo usar `forEach()`**

```javascript
// ✓ Usar forEach() para efectos secundarios
let usuarios = [{id: 1, nombre: "Juan"}, {id: 2, nombre: "María"}];

usuarios.forEach(usuario => {
    console.log(`Usuario ${usuario.id}: ${usuario.nombre}`);
});

// ✗ No usar forEach() si necesitas un nuevo array
// ✓ Usar map() para eso
```

***

### 1.2. `map()`: Transformar Arrays

`map()` **transforma cada elemento** usando una función y **retorna un nuevo array**.

```javascript
let numeros = [1, 2, 3, 4, 5];

// Multiplicar cada número por 2
let duplicados = numeros.map(num => num * 2);
console.log(duplicados);  // [2, 4, 6, 8, 10]

// Transformar array de objetos
let usuarios = [
    { nombre: "Juan", edad: 30 },
    { nombre: "María", edad: 25 }
];

let nombres = usuarios.map(usuario => usuario.nombre);
console.log(nombres);     // ["Juan", "María"]

// Crear objetos transformados
let usuariosConMayuscula = usuarios.map(usuario => ({
    nombre: usuario.nombre.toUpperCase(),
    edad: usuario.edad
}));
```

#### **`map()` vs `forEach()`**

```javascript
// forEach() - efectos secundarios, no retorna nada
let resultado1 = numeros.forEach(n => console.log(n));
console.log(resultado1); // undefined

// map() - retorna nuevo array
let resultado2 = numeros.map(n => n * 2);
console.log(resultado2); // [2, 4, 6, 8, 10]
```

***

### 1.3. `filter()`: Filtrar Elementos

`filter()` **selecciona elementos** que cumplen una condición y **retorna un nuevo array**.

```javascript
let numeros = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

// Números pares
let pares = numeros.filter(n => n % 2 === 0);
console.log(pares);      // [2, 4, 6, 8, 10]

// Números mayores a 5
let mayores5 = numeros.filter(n => n > 5);
console.log(mayores5);   // [6, 7, 8, 9, 10]

// Filtrar objetos
let usuarios = [
    { nombre: "Juan", edad: 30, activo: true },
    { nombre: "María", edad: 25, activo: false },
    { nombre: "Carlos", edad: 35, activo: true }
];

let usuariosActivos = usuarios.filter(u => u.activo);
console.log(usuariosActivos); // Juan y Carlos

// Múltiples condiciones
let mayoresActivos = usuarios.filter(u => u.edad > 28 && u.activo);
```

***

### 1.4. `reduce()`: Agregar Valores

`reduce()` **acumula valores** en un solo resultado. Es el método más poderoso pero también el más complejo.

**Sintaxis**: `array.reduce((acumulador, elemento) => { return nuevo_acumulador }, valor_inicial)`

#### **Ejemplo básico: suma**

```javascript
let numeros = [1, 2, 3, 4, 5];

// Suma de todos
let suma = numeros.reduce((total, num) => total + num, 0);
console.log(suma);       // 15

// Visualizar paso a paso
numeros.reduce((total, num) => {
    console.log(`total: ${total}, num: ${num}`);
    return total + num;
}, 0);
// total: 0, num: 1
// total: 1, num: 2
// total: 3, num: 3
// total: 6, num: 4
// total: 10, num: 5
```

#### **`reduce()` para crear objetos**

```javascript
let usuarios = [
    { id: 1, nombre: "Juan" },
    { id: 2, nombre: "María" }
];

// Convertir array a objeto indexado por ID
let usuariosPorId = usuarios.reduce((obj, usuario) => {
    obj[usuario.id] = usuario;
    return obj;
}, {});

console.log(usuariosPorId);
// { 1: {id: 1, nombre: "Juan"}, 2: {id: 2, nombre: "María"} }
```

#### **`reduce()` para contar**

```javascript
let palabras = ["hola", "mundo", "hola", "javascript", "hola"];

// Contar ocurrencias
let conteo = palabras.reduce((acc, palabra) => {
    acc[palabra] = (acc[palabra] || 0) + 1;
    return acc;
}, {});

console.log(conteo); // {hola: 3, mundo: 1, javascript: 1}
```

***

### 1.5. `find()` y `findIndex()`: Búsqueda

#### **`find()`: obtener el elemento**

```javascript
let usuarios = [
    { id: 1, nombre: "Juan" },
    { id: 2, nombre: "María" },
    { id: 3, nombre: "Carlos" }
];

// Encontrar usuario con ID 2
let usuario = usuarios.find(u => u.id === 2);
console.log(usuario); // {id: 2, nombre: "María"}

// Si no existe, retorna undefined
let noExiste = usuarios.find(u => u.id === 99);
console.log(noExiste); // undefined
```

#### **`findIndex()`: obtener el índice**

```javascript
let indice = usuarios.findIndex(u => u.id === 2);
console.log(indice); // 1

let noExiste = usuarios.findIndex(u => u.id === 99);
console.log(noExiste); // -1
```

***

### 1.6. `some()` y `every()`: Validación

#### **`some()`: ¿Hay al menos uno?**

Retorna `true` si **al menos un** elemento cumple la condición.

```javascript
let numeros = [1, 2, 3, 4, 5];

let hayPares = numeros.some(n => n % 2 === 0);
console.log(hayPares); // true

let hayCien = numeros.some(n => n === 100);
console.log(hayCien);  // false
```

#### **`every()`: ¿Todos cumplen?**

Retorna `true` si **todos** los elementos cumplen la condición.

```javascript
let numeros = [2, 4, 6, 8];

let todosPares = numeros.every(n => n % 2 === 0);
console.log(todosPares); // true

let todos = [1, 2, 3, 4];
let todosParesAhora = todos.every(n => n % 2 === 0);
console.log(todosParesAhora); // false

// Validar objetos
let usuarios = [
    { nombre: "Juan", edad: 30 },
    { nombre: "María", edad: 25 }
];

let todosMayores18 = usuarios.every(u => u.edad >= 18);
console.log(todosMayores18); // true
```

***

### 1.7. Casos Prácticos Avanzados

#### **Filtrar y mapear juntos**

```javascript
let usuarios = [
    { id: 1, nombre: "Juan", activo: true, edad: 30 },
    { id: 2, nombre: "María", activo: false, edad: 25 },
    { id: 3, nombre: "Carlos", activo: true, edad: 35 }
];

// Obtener nombres de usuarios activos
let nombresActivos = usuarios
    .filter(u => u.activo)
    .map(u => u.nombre);

console.log(nombresActivos); // ["Juan", "Carlos"]
```

#### **Validar datos antes de procesar**

```javascript
let pedidos = [
    { id: 1, monto: 100, pagado: true },
    { id: 2, monto: 50, pagado: true },
    { id: 3, monto: 0, pagado: false }
];

// Verificar que todos tengan monto > 0
if (pedidos.every(p => p.monto > 0)) {
    console.log("Todos los pedidos son válidos");
} else {
    console.log("Hay pedidos inválidos");
}
```

***

### 1.8. Encadenamiento de Métodos (_Method Chaining_)

Los métodos de arrays pueden encadenarse para crear transformaciones complejas:

```javascript
let datos = [
    { nombre: "Juan", edad: 30, activo: true },
    { nombre: "María", edad: 25, activo: false },
    { nombre: "Carlos", edad: 35, activo: true },
    { nombre: "Ana", edad: 22, activo: true }
];

// Cadena compleja
let resultado = datos
    .filter(p => p.activo)              // Solo activos
    .filter(p => p.edad >= 25)          // Mayor o igual a 25
    .map(p => ({                        // Extraer y transformar
        nombre: p.nombre.toUpperCase(),
        edad: p.edad
    }))
    .sort((a, b) => a.edad - b.edad);   // Ordenar por edad

console.log(resultado);
// [{nombre: "JUAN", edad: 30}, {nombre: "CARLOS", edad: 35}]
```

#### **Legibilidad del encadenamiento**

```javascript
// Difícil de leer (una línea muy larga)
let resultado = usuarios.filter(u => u.activo).map(u => u.nombre).sort();

// Mejor legibilidad (con saltos de línea)
let resultado = usuarios
    .filter(u => u.activo)
    .map(u => u.nombre)
    .sort();
```

***

### Resumen del Capítulo

Los métodos de iteración y transformación son herramientas poderosas que permiten trabajar con arrays de manera funcional y expresiva. Dominar estos métodos es esencial para escribir código JavaScript moderno y limpio.

#### **💡 Conceptos Clave:**

* **forEach()**: Iteración con efectos secundarios (no retorna)
* **map()**: Transformación de arrays (retorna nuevo)
* **filter()**: Selección de elementos
* **reduce()**: Acumulación de valores (el más versátil)
* **find()/findIndex()**: Búsqueda de elementos
* **some()/every()**: Validación de condiciones
* **Encadenamiento**: Combinar múltiples métodos
* **Inmutabilidad**: Estos métodos no modifican el array original

#### **🤔 Preguntas de Reflexión:**

1. ¿Cuál es la diferencia entre forEach() y map()?
2. ¿Cuándo usarías filter() vs find()?
3. ¿Cómo usarías reduce() para crear un objeto indexado?
4. ¿Qué retorna some() vs every()?
5. Encadena filter(), map() y reduce() para resolver un problema complejo.
6. ¿Por qué el encadenamiento de métodos es preferible a bucles anidados?

***
