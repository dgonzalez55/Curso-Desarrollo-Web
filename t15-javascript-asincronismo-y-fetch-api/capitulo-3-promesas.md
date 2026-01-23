# Capítulo 3: Promesas

Las Promesas son el pilar de la programación asíncrona moderna en JavaScript. Resuelven el problema del callback hell y proporcionan una forma clara y predecible de trabajar con operaciones asincrónicas. Este capítulo cubre todo lo que necesitas saber sobre Promesas.

### 3.1. Creación de Promesas: `new Promise(executor)`

Una Promesa es un objeto que representa una operación asíncrona que terminará en el futuro (o ha terminado ya).

```javascript
// Sintaxis: new Promise((resolve, reject) => { ... })

const miPromesa = new Promise((resolve, reject) => {
    // resolve: Cuando todo va bien
    // reject: Cuando hay un error
    
    if (Math.random() > 0.5) {
        resolve("¡Éxito!");
    } else {
        reject("¡Error!");
    }
});

// Las Promesas están listas para usar después de crearlas
console.log(miPromesa); // Promise { <pending> }
```

#### **Ejemplo práctico: Simular una descarga**

```javascript
function descargarArchivo(url) {
    return new Promise((resolve, reject) => {
        console.log("Descargando...");
        
        setTimeout(() => {
            if (url.startsWith("https")) {
                resolve("archivo.pdf descargado");
            } else {
                reject(new Error("URL inválida"));
            }
        }, 2000);
    });
}

// Las Promesas se crean al llamar a la función
const descarga = descargarArchivo("https://example.com/archivo.pdf");
console.log(descarga); // Promise { <pending> }
```

***

### 3.2. Estados: pending, fulfilled, rejected

Una Promesa tiene exactamente tres estados:

1. **pending** (pendiente): La operación está en progreso
2. **fulfilled** (cumplida): La operación terminó exitosamente (se llamó `resolve`)
3. **rejected** (rechazada): Hubo un error (se llamó `reject`)

```javascript
// PENDING: Cuando se crea
const promesa1 = new Promise((resolve, reject) => {
    console.log("State: pending");
    // No hemos llamado resolve ni reject
});

console.log(promesa1); // Promise { <pending> }

// FULFILLED: Cuando llamamos resolve
const promesa2 = new Promise((resolve, reject) => {
    resolve("Éxito");
});

console.log(promesa2); // Promise { "Éxito" }

// REJECTED: Cuando llamamos reject
const promesa3 = new Promise((resolve, reject) => {
    reject(new Error("Algo salió mal"));
});

console.log(promesa3); // Promise { <rejected> Error: Algo salió mal }
```

#### **Cambio de estado (irreversible):**

```javascript
const promesa = new Promise((resolve, reject) => {
    resolve("Primera resolución");
    
    // Esto NO hace nada porque ya está resuelta
    resolve("Segunda resolución");
    reject(new Error("Error"));
});

// Promise { "Primera resolución" }
// El estado una vez fijado, no puede cambiar
```

***

### 3.3. Métodos `.then()`, `.catch()`, `.finally()`

Para trabajar con Promesas, usamos estos métodos para especificar qué hacer cuando se resuelvan o rechacen.

#### **`.then(onFulfilled, onRejected)`**

Se ejecuta cuando la Promesa se cumple (**fulfill**) o se rechaza (**reject**).

```javascript
const promesa = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve("Datos cargados");
    }, 1000);
});

// .then recibe dos callbacks opcionales
promesa.then(
    (valor) => {
        console.log("Éxito:", valor);
    },
    (error) => {
        console.error("Error:", error);
    }
);

// Output (después de 1s):
// Éxito: Datos cargados
```

#### **`.catch(onRejected)`**

Solo maneja rechazos (es equivalente a `.then(null, onRejected)`).

```javascript
const promesa = new Promise((resolve, reject) => {
    setTimeout(() => {
        reject(new Error("Algo salió mal"));
    }, 1000);
});

promesa.catch((error) => {
    console.error("Error capturado:", error.message);
});

// Output (después de 1s):
// Error capturado: Algo salió mal
```

#### **`.finally(onFinally)`**

Se ejecuta siempre, sin importar si fue éxito o error. Útil para limpiar o cerrar conexiones.

```javascript
const promesa = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve("Datos");
    }, 1000);
});

promesa
    .then(datos => console.log("Datos:", datos))
    .catch(error => console.error("Error:", error))
    .finally(() => console.log("Operación completada"));

// Output (después de 1s):
// Datos: Datos
// Operación completada
```

***

### 3.4. Promise chaining: Encadenar promesas

La verdadera potencia de las Promesas es poder **encadenarlas** de forma clara sin callback hell.

```javascript
function paso1() {
    return new Promise((resolve) => {
        setTimeout(() => {
            console.log("Paso 1 completado");
            resolve("resultado1");
        }, 1000);
    });
}

function paso2(resultado1) {
    return new Promise((resolve) => {
        setTimeout(() => {
            console.log("Paso 2 completado", resultado1);
            resolve("resultado2");
        }, 1000);
    });
}

function paso3(resultado2) {
    return new Promise((resolve) => {
        setTimeout(() => {
            console.log("Paso 3 completado", resultado2);
            resolve("resultado3");
        }, 1000);
    });
}

// Encadenar: es MUCHO más legible que callbacks
paso1()
    .then(r1 => paso2(r1))
    .then(r2 => paso3(r2))
    .then(r3 => console.log("Todo listo:", r3))
    .catch(error => console.error("Error en la cadena:", error));

// Output (después de 3 segundos):
// Paso 1 completado
// Paso 2 completado resultado1
// Paso 3 completado resultado2
// Todo listo: resultado3
```

#### **Forma abreviada (arrow functions):**

```javascript
paso1()
    .then(paso2)
    .then(paso3)
    .then(r3 => console.log("Todo listo:", r3))
    .catch(error => console.error("Error:", error));
```

***

### 3.5. Propagación de errores en cadenas

Si alguna Promesa en la cadena se rechaza, el error se propaga automáticamente al siguiente `.catch()`.

```javascript
function paso1() {
    return Promise.resolve("ok");
}

function paso2() {
    return Promise.reject(new Error("Fallo en paso 2"));
}

function paso3() {
    return Promise.resolve("ok");
}

paso1()
    .then(() => paso2())
    .then(() => paso3())
    .then(() => console.log("Completado"))
    .catch((error) => {
        console.error("Se capturó error:", error.message);
    });

// Output:
// Se capturó error: Fallo en paso 2
// paso3() nunca se ejecuta porque paso2 falló
```

#### **Capturar y continuar:**

```javascript
paso1()
    .then(() => paso2())
    .catch((error) => {
        console.error("Error en paso 2, continuando...");
        return "valor_por_defecto";
    })
    .then((valor) => paso3())
    .catch((error) => {
        console.error("Error final:", error);
    });
```

***

### 3.6. Promesas ya resueltas y perezosas

#### **Promesas inmediatamente resueltas:**

```javascript
// Promise.resolve: Éxito instantáneo
const exito = Promise.resolve("datos");
exito.then(d => console.log(d)); // "datos"

// Promise.reject: Error instantáneo
const error = Promise.reject(new Error("error"));
error.catch(e => console.error(e.message)); // "error"
```

#### **Promesas perezosas (lazy):**

Las Promesas comienzan a ejecutarse inmediatamente por defecto. Para hacer una "lazy Promise" que espere a ser evaluada, necesitas una función:

```javascript
// ❌ Eager: Se ejecuta inmediatamente
const promesa = new Promise((resolve) => {
    console.log("Ejecutándose");
    resolve("ok");
});

// ✓ Lazy: Solo se ejecuta cuando lo llamas
function crearPromesa() {
    return new Promise((resolve) => {
        console.log("Ejecutándose");
        resolve("ok");
    });
}

// No hace nada hasta que la llames
const lazy = crearPromesa;
lazy().then(r => console.log(r)); // Ahora se ejecuta
```

***

### Resumen del Capítulo

Las Promesas reemplazan los callbacks con una forma de manejar asincronía más legible y segura. El chaining de Promises permite escribir flujos secuenciales sin anidamiento profundo. Entender estados, `.then()`, `.catch()` y propagación de errores es fundamental para JavaScript asíncrono moderno.

#### **💡 Conceptos Clave:**

* **Promise**: Objeto que representa una operación asíncrona futura
* **Estados**: pending, fulfilled, rejected (inmutables)
* **resolve/reject**: Funciones para cambiar el estado
* **.then()**: Maneja éxito o error
* **.catch()**: Maneja solo errores
* **.finally()**: Se ejecuta siempre
* **Promise chaining**: Encadenar operaciones sin callback hell
* **Propagación de errores**: Los errores se propagan automáticamente
* **Eager vs Lazy**: Las Promesas son eager por defecto (se ejecutan inmediatamente)

#### **🤔 Preguntas de Reflexión:**

1. ¿Cuáles son los tres estados de una Promesa?
2. ¿Cuál es la diferencia entre `.then()` y `.catch()`?
3. ¿Por qué `.finally()` es útil incluso aunque retorne nada?
4. ¿Cómo se propagan los errores en una cadena de Promesas?
5. ¿Qué sucede si llamas `resolve` y luego `reject` en la misma Promesa?
6. ¿Por qué es más legible una cadena de Promesas que callbacks anidados?
7. Crea una Promesa que simule una descarga y encadena operaciones después.

***
