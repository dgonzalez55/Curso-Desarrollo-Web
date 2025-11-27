# Capítulo 10: Composición y Patrones Funcionales

Este capítulo explora técnicas de programación funcional avanzada.

### 10.1. Funciones de Orden Superior (HOF)

```javascript
// Retornar una función
function multiplicar(factor) {
    return function(numero) {
        return numero * factor;
    };
}

let doble = multiplicar(2);
let triple = multiplicar(3);

console.log(doble(5));  // 10
console.log(triple(5)); // 15

// Pasar función como argumento
function aplicar(fn, x) {
    return fn(x);
}

console.log(aplicar(doble, 5)); // 10
```

***

### 10.2. Currying: Retornar Funciones

```javascript
// Función tradicional
function suma(a, b, c) {
    return a + b + c;
}

// Currificada
function sumaCurrificada(a) {
    return function(b) {
        return function(c) {
            return a + b + c;
        };
    };
}

console.log(sumaCurrificada(1)(2)(3)); // 6

// Versión con arrow
const add = a => b => c => a + b + c;
console.log(add(1)(2)(3)); // 6
```

***

### 10.3. Composición de Funciones

```javascript
// Funciones pequeñas
const agregar1 = x => x + 1;
const multiplicar2 = x => x * 2;
const restar3 = x => x - 3;

// Compose: aplicar de derecha a izquierda
function compose(...funciones) {
    return x => funciones.reduceRight((v, f) => f(v), x);
}

const operacion = compose(restar3, multiplicar2, agregar1);
console.log(operacion(5)); // ((5+1)*2)-3 = 9

// Pipe: aplicar de izquierda a derecha
function pipe(...funciones) {
    return x => funciones.reduce((v, f) => f(v), x);
}

const operacion2 = pipe(agregar1, multiplicar2, restar3);
console.log(operacion2(5)); // ((5+1)*2)-3 = 9
```

***

### 10.4. Pipe vs Compose

```javascript
// Ejemplo práctico
const usuarios = [
    { nombre: "Juan", edad: 30 },
    { nombre: "María", edad: 25 }
];

const filtroMayores25 = arr => arr.filter(u => u.edad > 25);
const mapNombres = arr => arr.map(u => u.nombre);
const ordenar = arr => arr.sort();

// Compose (RDD - derecha a izquierda)
const obtenerNombresCompose = compose(
    ordenar,
    mapNombres,
    filtroMayores25
);

// Pipe (LTR - izquierda a derecha)
const obtenerNombresPipe = pipe(
    filtroMayores25,
    mapNombres,
    ordenar
);

console.log(obtenerNombresPipe(usuarios)); // ["Juan"]
```

***

### 10.5. Memoización

```javascript
// Sin memoización (lento)
function fibonacci(n) {
    if (n <= 1) return n;
    return fibonacci(n - 1) + fibonacci(n - 2);
}

// Con memoización (rápido)
function memoize(fn) {
    const cache = {};
    return function(n) {
        if (n in cache) {
            return cache[n];
        }
        const resultado = fn(n);
        cache[n] = resultado;
        return resultado;
    };
}

const fibMemo = memoize(fibonacci);
console.log(fibMemo(40)); // Instantáneo vs 20+ segundos
```

***

### 10.6. Partial Application

```javascript
// Aplicación parcial de argumentos
function bindeo(fn, ...argsIniciales) {
    return (...argsFinales) => fn(...argsIniciales, ...argsFinales);
}

function sumar(a, b, c) {
    return a + b + c;
}

const sumar10 = bindeo(sumar, 10);
console.log(sumar10(5, 3)); // 18

const sumar10y5 = bindeo(sumar, 10, 5);
console.log(sumar10y5(3)); // 18
```

***

### 10.7. Casos Prácticos: Builders

```javascript
// Builder pattern con composición
function crearUsuarioBuilder() {
    let usuario = {};
    
    return {
        conNombre(nombre) {
            usuario.nombre = nombre;
            return this;
        },
        conEdad(edad) {
            usuario.edad = edad;
            return this;
        },
        conEmail(email) {
            usuario.email = email;
            return this;
        },
        construir() {
            return usuario;
        }
    };
}

const usuario = crearUsuarioBuilder()
    .conNombre("Juan")
    .conEdad(30)
    .conEmail("juan@example.com")
    .construir();

console.log(usuario);
// {nombre: "Juan", edad: 30, email: "juan@example.com"}
```

***

### 10.8. Integración con Arrays y Objetos

```javascript
// Transformar datos complejos
const datos = [
    { id: 1, nombre: "Juan", ventas: 5000 },
    { id: 2, nombre: "María", ventas: 7000 },
    { id: 3, nombre: "Carlos", ventas: 3000 }
];

// Composición de transformaciones
const procesarVentas = pipe(
    arr => arr.filter(p => p.ventas > 4000),
    arr => arr.map(p => ({ ...p, comision: p.ventas * 0.1 })),
    arr => arr.sort((a, b) => b.comision - a.comision)
);

console.log(procesarVentas(datos));
```

***

### Resumen del Capítulo

La programación funcional permite escribir código modular, reutilizable y predecible.

#### **💡 Conceptos Clave:**

* **HOF**: Funciones que retornan o aceptan funciones
* **Currying**: Aplicación parcial de argumentos
* **Composición**: Combinar funciones pequeñas
* **Pipe vs Compose**: Orden de aplicación
* **Memoización**: Cachear resultados
* **Builders**: Patrón de construcción fluida

#### **🤔 Preguntas de Reflexión:**

1. ¿Qué es una función de orden superior?
2. ¿Cuál es la diferencia entre compose y pipe?
3. ¿Cuándo usarías memoización?
4. Implementa un builder pattern.

***
