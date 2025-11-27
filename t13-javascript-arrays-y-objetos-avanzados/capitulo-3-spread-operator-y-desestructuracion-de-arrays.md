# Capítulo 3: Spread Operator y Desestructuración de Arrays

El spread operator (...) y la desestructuración son características modernas (ES6+) que simplifican enormemente el trabajo con arrays. Este capítulo explora estos patrones poderosos.

### 3.1. Spread Operator (`...`): Expansión de Arrays

El spread operator `...` expande un array en elementos individuales.

```javascript
let numeros = [1, 2, 3];

// Expandir array
console.log(...numeros);           // 1 2 3

// Pasarlo como argumentos
function sumar(a, b, c) {
    return a + b + c;
}

console.log(sumar(...numeros));    // 6

// Expandir en console.log
console.log("Números:", ...numeros); // Números: 1 2 3
```

***

### 3.2. Copiar Arrays: Spread vs `slice()`

```javascript
let original = [1, 2, 3];

// Con spread
let copia1 = [...original];

// Con slice
let copia2 = original.slice();

// Ambas crean copias superficiales
copia1.push(4);
console.log(original); // [1, 2, 3] (sin cambios)
console.log(copia1);   // [1, 2, 3, 4]

// ¡CUIDADO: copias profundas con objetos anidados!
let usuarios = [{id: 1, nombre: "Juan"}];
let usuarios2 = [...usuarios];
usuarios2[0].nombre = "María";
console.log(usuarios[0].nombre); // "María" (¡cambió el original!)
```

***

### 3.3. Combinar Arrays con Spread

```javascript
let array1 = [1, 2, 3];
let array2 = [4, 5, 6];

// Combinar con spread
let combinado = [...array1, ...array2];
console.log(combinado); // [1, 2, 3, 4, 5, 6]

// Intercalar elementos
let intercalado = [...array1, 0, ...array2];
console.log(intercalado); // [1, 2, 3, 0, 4, 5, 6]

// Mejor que concat()
console.log(array1.concat(array2)); // [1, 2, 3, 4, 5, 6]
```

***

### 3.4. Desestructuración Básica

La desestructuración extrae valores de arrays asignándolos a variables.

```javascript
// Array tradicional
let coordenadas = [10, 20];
let x = coordenadas[0];
let y = coordenadas[1];

// Con desestructuración
let [x, y] = [10, 20];
console.log(x, y); // 10, 20

// Ignorar elementos
let [primero, , tercero] = [1, 2, 3];
console.log(primero, tercero); // 1, 3

// De una función que retorna array
function obtenerCoordenadas() {
    return [5, 15];
}

let [a, b] = obtenerCoordenadas();
console.log(a, b); // 5, 15
```

***

### 3.5. Desestructuración Avanzada

```javascript
// Valores por defecto
let [x = 0, y = 0] = [10];
console.log(x, y); // 10, 0

// Intercambiar variables
let a = 1, b = 2;
[a, b] = [b, a];
console.log(a, b); // 2, 1

// Desestructuración anidada
let [[x1, y1], [x2, y2]] = [[1, 2], [3, 4]];
console.log(x1, y1, x2, y2); // 1, 2, 3, 4
```

***

### 3.6. Rest Parameters en Desestructuración

```javascript
// Capturar resto del array
let [primero, ...resto] = [1, 2, 3, 4, 5];
console.log(primero); // 1
console.log(resto);   // [2, 3, 4, 5]

// En funciones
function procesar([primero, ...otros]) {
    console.log("Primero:", primero);
    console.log("Otros:", otros);
}

procesar([10, 20, 30]);
// Primero: 10
// Otros: [20, 30]
```

***

### 3.7. Valores por Defecto

```javascript
// Simples
let [a = 10, b = 20] = [1];
console.log(a, b); // 1, 20

// Con funciones
function getDefecto() {
    return 100;
}

let [x = getDefecto()] = [];
console.log(x); // 100

// Complejos
let [primero = {}, segundo = []] = [];
console.log(primero, segundo); // {}, []
```

***

### 3.8. Intercambio de Variables

Una aplicación práctica común de la desestructuración:

```javascript
// Tradicional
let temp = a;
a = b;
b = temp;

// Con desestructuración
[a, b] = [b, a];

// Rotación de variables
let x = 1, y = 2, z = 3;
[x, y, z] = [y, z, x];
console.log(x, y, z); // 2, 3, 1
```

***

### Resumen del Capítulo

El spread operator y la desestructuración son características modernas que hacen el código más legible y conciso. Dominarlos es esencial para JavaScript moderno.

#### **💡 Conceptos Clave:**

* **Spread operator (...)**: Expande arrays en elementos individuales
* **Copiar arrays**: `[...original]` crea copia superficial
* **Combinar arrays**: `[...array1, ...array2]`
* **Desestructuración**: Extrae valores en variables
* **Rest parameters**: Captura resto con `...`
* **Valores por defecto**: En desestructuración
* **Intercambio**: Swap de variables elegante
* **Anidación**: Desestructuración de arrays anidados

#### **🤔 Preguntas de Reflexión:**

1. ¿Cuál es la diferencia entre `[...array]` y `array.slice()`?
2. ¿Cómo usarías la desestructuración para extraer múltiples valores?
3. ¿Qué son los rest parameters en la desestructuración?
4. ¿Cuándo preferirías spread vs concat()?
5. Demuestra cómo intercambiar dos variables con desestructuración.

***
