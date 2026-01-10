# Capítulo 1: Introducción a la Asincronía

La asincronía es uno de los conceptos más importantes en JavaScript moderno. Sin ella, las aplicaciones web se congelarían esperando a que terminen operaciones lentas como descargas de archivos o consultas a bases de datos. Este capítulo introduce el concepto fundamental del código asíncrono.

### 1.1. ¿Qué es la asincronía? Operaciones bloqueantes vs no bloqueantes

**Operación bloqueante** (síncrona): El código espera a que termine una tarea antes de continuar.

```javascript
// Síncrono: Bloquea la ejecución
function cargarDatos() {
    console.log("1. Inicio de carga");
    
    // Simular una operación lenta (2 segundos)
    const inicio = Date.now();
    while (Date.now() - inicio < 2000) {
        // Esperar... la página está "congelada"
    }
    
    console.log("2. Datos cargados");
}

console.log("Antes");
cargarDatos();
console.log("Después");

// Output:
// Antes
// 1. Inicio de carga
// (espera 2 segundos... la página no responde)
// 2. Datos cargados
// Después
```

**Operación no bloqueante** (asíncrona): El código inicia una tarea y continúa sin esperar.

```javascript
// Asíncrono: NO bloquea
console.log("Antes");

setTimeout(() => {
    console.log("2. Datos cargados");
}, 2000);

console.log("Después");

// Output (instantáneo):
// Antes
// Después
// (2 segundos después...)
// 2. Datos cargados
```

{% hint style="success" %}
**La diferencia es crítica**: Con operaciones asíncronas, la interfaz de usuario sigue siendo responsiva mientras se esperan operaciones lentas.
{% endhint %}

***

### 1.2. El Event Loop: Cómo JavaScript ejecuta código asíncrono

JavaScript es **single-threaded** (un solo hilo de ejecución), pero parece ser multithread porque usa el **Event Loop**.

El Event Loop es un mecanismo que implementa los siguientes pasos:

1. Ejecuta el código síncrono (Call Stack)
2. Cuando se completa, revisa si hay tareas asíncronas que se han completado
3. Las ejecuta en orden

```javascript
console.log("1. Síncrono");

setTimeout(() => {
    console.log("3. Asíncrono (después de 0ms)");
}, 0);

console.log("2. Síncrono");

// Output:
// 1. Síncrono
// 2. Síncrono
// 3. Asíncrono (después de 0ms)

// Nota: Incluso con 0ms, el callback se ejecuta DESPUÉS del código síncrono
```

***

### 1.3. Call Stack, Web APIs y Task Queue

Visualiza cómo JavaScript procesa código:

```
┌─────────────────────────────────────────────────┐
│           JAVASCRIPT ENGINE                     │
│                                                 │
│  ┌──────────────────────────────────────────┐   │
│  │        CALL STACK (ejecución)            │   │
│  │  - Código síncrono                       │   │
│  │  - Se ejecuta línea por línea            │   │
│  └──────────────────────────────────────────┘   │
│                                                 │
│  ┌──────────────────────────────────────────┐   │
│  │        TASK QUEUE (Macrotasks)           │   │
│  │  - setTimeout, setInterval               │   │
│  │  - Eventos del DOM                       │   │
│  │  - I/O operations                        │   │
│  └──────────────────────────────────────────┘   │
│                                                 │
│  ┌──────────────────────────────────────────┐   │
│  │     MICROTASK QUEUE (Microtasks)         │   │
│  │  - Promises (.then, .catch, .finally)    │   │
│  │  - queueMicrotask()                      │   │
│  │  - MutationObserver                      │   │
│  └──────────────────────────────────────────┘   │
└─────────────────────────────────────────────────┘
        │
        │ (Web APIs: setTimeout, fetch, etc.)
        │
        ↓
    NAVEGADOR
```

**El Event Loop funciona así**:

1. Ejecuta TODO lo que hay en el **Call Stack**
2. Cuando se vacía, procesa la **Microtask Queue** (Promises)
3. Cuando se vacía, procesa la **Macrotask Queue** (setTimeout, eventos)
4. Vuelve al paso 2

```javascript
console.log("1. Stack");

setTimeout(() => {
    console.log("4. Macrotask (setTimeout)");
}, 0);

Promise.resolve().then(() => {
    console.log("3. Microtask (Promise)");
});

console.log("2. Stack");

// Output:
// 1. Stack
// 2. Stack
// 3. Microtask (Promise)
// 4. Macrotask (setTimeout)

// Las Promises se ejecutan ANTES que setTimeout, aunque setTimeout tenga 0ms
```

***

### 1.4. `setTimeout`: Primera aproximación al código asíncrono

**`setTimeout`** es la forma más simple de entender asincronía. Programa una función para ejecutarse después de un tiempo.

```javascript
// Sintaxis: setTimeout(callback, delay_en_ms)

setTimeout(() => {
    console.log("Se ejecuta después de 1 segundo");
}, 1000);

// Guardar el ID para cancelar después
const timerId = setTimeout(() => {
    console.log("Esto nunca se ejecutará");
}, 5000);

// Cancelar
clearTimeout(timerId);
```

**`setInterval`**: Ejecutar repetidamente cada X milisegundos.

```javascript
let contador = 0;

const intervalId = setInterval(() => {
    contador++;
    console.log(`Tick ${contador}`);
    
    if (contador === 5) {
        clearInterval(intervalId); // Detener
    }
}, 1000);

// Output:
// Tick 1 (después de 1s)
// Tick 2 (después de 2s)
// Tick 3 (después de 3s)
// Tick 4 (después de 4s)
// Tick 5 (después de 5s)
```

***

### 1.5. Ejemplos prácticos del orden de ejecución

#### **Ejemplo 1: Predecir el orden**

```javascript
console.log("A");

setTimeout(() => {
    console.log("B");
}, 0);

console.log("C");

// ¿Cuál es el orden?
// A
// C
// B

// Explicación:
// 1. "A" es síncrono (Call Stack)
// 2. setTimeout va a Macrotask Queue
// 3. "C" es síncrono (Call Stack)
// 4. Call Stack vacío, procesa Macrotask Queue → "B"
```

#### **Ejemplo 2: Mezclar Promesas y setTimeout**

```javascript
console.log("1");

setTimeout(() => {
    console.log("2");
}, 0);

Promise.resolve()
    .then(() => console.log("3"))
    .then(() => console.log("4"));

console.log("5");

// Output:
// 1
// 5
// 3
// 4
// 2

// Orden:
// Stack: 1, 5
// Microtasks: 3, 4 (Promises)
// Macrotasks: 2 (setTimeout)
```

#### **Ejemplo 3: Operación que parece lenta pero no lo es**

```javascript
console.log("Inicio");

// Esta función se ve como si esperara 2 segundos, pero en realidad
// vuelve instantáneamente. El console.log se ejecuta 2 segundos después.
setTimeout(() => {
    console.log("2 segundos después");
}, 2000);

console.log("Fin"); // Esto se ejecuta instantáneamente

// Output (inmediato):
// Inicio
// Fin
// (2 segundos después...)
// 2 segundos después
```

***

### Resumen del Capítulo

La asincronía es fundamental para JavaScript en el navegador. El Event Loop permite que JavaScript ejecute código síncrono rápidamente sin bloquear, mientras maneja operaciones lentas en paralelo. Entender Call Stack, Task Queues y el orden de ejecución es crucial para escribir código predecible.

#### **💡 Conceptos Clave:**

* **Síncrono**: Bloquea el flujo de ejecución (esperamos)
* **Asíncrono**: No bloquea (continuamos mientras se ejecuta)
* **Event Loop**: Mecanismo que orquestra la ejecución
* **Call Stack**: Ejecuta código síncrono línea por línea
* **Macrotask Queue**: setTimeout, eventos, I/O
* **Microtask Queue**: Promises, queueMicrotask
* **Single-threaded**: JavaScript solo tiene un hilo, pero parece multithread
* **setTimeout/setInterval**: Operaciones asíncronas simples

#### **🤔 Preguntas de Reflexión:**

1. ¿Cuál es la diferencia entre código bloqueante y no bloqueante?
2. ¿Por qué `console.log` con setTimeout(0) se ejecuta después del código síncrono?
3. ¿Qué es el Event Loop y cómo maneja diferentes tipos de tareas?
4. ¿Cuál se ejecuta primero: una Macrotask o una Microtask?
5. ¿Por qué JavaScript es single-threaded pero parece responder a múltiples cosas a la vez?
6. Predice el orden de ejecución de un código que mezcla setTimeout, Promise y console.log

***
