# Capítulo 5: Async/Await

`async/await` es la forma moderna y más legible de escribir código asíncrono en JavaScript. Bajo el capó, usa promesas, pero la sintaxis es mucho más parecida al código síncrono. Este capítulo cubre cómo usar estas palabras clave.

### 5.1. Funciones `async`: Definición y retorno implícito de promesas

Una función `async` siempre retorna una **promesa**, incluso si no la creas explícitamente.

```javascript
// Sintaxis: async function nombre() { ... }

async function saludar() {
    return "Hola";
}

// Una función async SIEMPRE retorna una Promise
const promesa = saludar();
console.log(promesa); // Promise { "Hola" }

// Para obtener el valor, usa .then() o await
promesa.then(valor => console.log(valor)); // "Hola"
```

#### **Comportamiento automático:**

```javascript
async function ejemplo1() {
    return 42;
}

async function ejemplo2() {
    return Promise.resolve(42);
}

async function ejemplo3() {
    throw new Error("Error");
}

// Todos retornan Promesas
ejemplo1().then(v => console.log(v)); // 42
ejemplo2().then(v => console.log(v)); // 42
ejemplo3().catch(e => console.error(e)); // Error
```

***

### 5.2. La palabra clave `await`: Esperar una promesa

`await` pausa la ejecución de la función async hasta que la promesa se resuelva o rechace. **Solo funciona dentro de funciones async**.

```javascript
// ❌ Error: await fuera de función async
const resultado = await Promise.resolve(42);

// ✓ Correcto: await dentro de async
async function obtenerDatos() {
    const resultado = await Promise.resolve(42);
    console.log(resultado); // 42
}

obtenerDatos();
```

#### **Esperar una promesa:**

```javascript
function descargarDatos(url) {
    return new Promise((resolve) => {
        setTimeout(() => {
            resolve({ id: 1, nombre: "Juan" });
        }, 2000);
    });
}

async function cargar() {
    console.log("Descargando...");
    
    // await pausa aquí hasta que la promesa se resuelva
    const datos = await descargarDatos("/api/usuarios/1");
    
    console.log("Datos recibidos:", datos);
}

cargar();

// Output (después de 2s):
// Descargando...
// Datos recibidos: { id: 1, nombre: "Juan" }
```

***

### 5.3. Equivalencia con `.then()` y por qué es más legible

`async/await` y las promesas son exactamente equivalentes, pero `async/await` es más legible.

#### **Comparación: Promesas vs Async/Await**

```javascript
// CON .then() (Promise chaining)
function obtenerUsuarioYPosts1(userId) {
    return obtenerUsuario(userId)
        .then(usuario => {
            return obtenerPosts(userId)
                .then(posts => {
                    return { usuario, posts };
                });
        })
        .catch(error => console.error("Error:", error));
}

// CON async/await (mucho más legible)
async function obtenerUsuarioYPosts2(userId) {
    try {
        const usuario = await obtenerUsuario(userId);
        const posts = await obtenerPosts(userId);
        return { usuario, posts };
    } catch (error) {
        console.error("Error:", error);
    }
}

// Son exactamente equivalentes, pero async/await es más clara
```

#### **Parecido a código síncrono:**

```javascript
// Con async/await, parecen líneas síncronas
async function procesar() {
    const datos1 = await obtenerDatos1();
    const datos2 = await obtenerDatos2(datos1);
    const resultado = datos1 + datos2;
    return resultado;
}

// No está bloqueando: está esperando promesas bajo el capó
```

***

### 5.4. Manejo de errores: `try`/`catch` asíncrono

Con `async/await`, manejas errores con el bloque `try/catch` que ya conoces.

```javascript
async function descargarArchivo(url) {
    try {
        const respuesta = await fetch(url);
        
        if (!respuesta.ok) {
            throw new Error(`HTTP Error: ${respuesta.status}`);
        }
        
        const datos = await respuesta.json();
        return datos;
        
    } catch (error) {
        console.error("Error descargando:", error.message);
        // Puedes retornar un valor por defecto
        return null;
    } finally {
        console.log("Operación completada");
    }
}

descargarArchivo("/datos.json");
```

#### **Diferencia vs `.catch()`:**

```javascript
// CON .then().catch() (Promise chaining)
fetch("/datos.json")
    .then(r => r.json())
    .then(datos => console.log(datos))
    .catch(error => console.error("Error:", error));

// CON async/await (más limpio)
async function cargar() {
    try {
        const r = await fetch("/datos.json");
        const datos = await r.json();
        console.log(datos);
    } catch (error) {
        console.error("Error:", error);
    }
}

cargar();
```

***

### 5.5. Operaciones en paralelo vs secuencial con `async`/`await`

#### **Secuencial (esperamos cada una):**

```javascript
async function secuencial() {
    console.time("secuencial");
    
    const datos1 = await obtenerDatos1(); // Espera 1s
    const datos2 = await obtenerDatos2(); // Espera 1s (total: 2s)
    const datos3 = await obtenerDatos3(); // Espera 1s (total: 3s)
    
    console.timeEnd("secuencial");
    return [datos1, datos2, datos3];
}

// Resultado: ~3 segundos
```

#### **Paralelo (con `Promise.all`):**

```javascript
async function paralelo() {
    console.time("paralelo");
    
    // Iniciar TODAS a la vez, esperar a que terminen
    const [datos1, datos2, datos3] = await Promise.all([
        obtenerDatos1(),
        obtenerDatos2(),
        obtenerDatos3()
    ]);
    
    console.timeEnd("paralelo");
    return [datos1, datos2, datos3];
}

// Resultado: ~1 segundo
```

#### **Regla de oro:**

```javascript
// ❌ MALO: Secuencial sin necesidad (lento)
async function malo() {
    const user = await fetch("/usuario").then(r => r.json());
    const posts = await fetch("/posts").then(r => r.json());
    const comentarios = await fetch("/comentarios").then(r => r.json());
}

// ✓ BUENO: Paralelo cuando no dependen (rápido)
async function bueno() {
    const [user, posts, comentarios] = await Promise.all([
        fetch("/usuario").then(r => r.json()),
        fetch("/posts").then(r => r.json()),
        fetch("/comentarios").then(r => r.json())
    ]);
}
```

***

### 5.6. Arrow functions async

También puedes usar `async` con arrow functions:

```javascript
// Arrow function async
const obtenerDatos = async () => {
    const respuesta = await fetch("/datos.json");
    return await respuesta.json();
};

obtenerDatos().then(datos => console.log(datos));
```

***

### 5.7. Async IIFE (Immediately Invoked Function Expression)

A veces necesitas ejecutar código async en el nivel superior:

```javascript
// IIFE async
(async () => {
    try {
        const datos = await fetch("/datos.json").then(r => r.json());
        console.log("Datos cargados:", datos);
    } catch (error) {
        console.error("Error:", error);
    }
})();
```

***

### Resumen del Capítulo

`async/await` es la forma moderna de escribir código asíncrono que es legible y mantenible. Bajo el capó, son solo promesas, pero la sintaxis es mucho más clara. Recuerda usar `try/catch` para errores y `Promise.all()` para operaciones paralelas.

#### **💡 Conceptos Clave:**

* **async function**: Siempre retorna una promesa
* **await**: Pausa y espera una promesa
* **Solo en async**: await solo funciona dentro de funciones async
* **try/catch**: Manejo de errores
* **finally**: Se ejecuta siempre
* **Secuencial vs Paralelo**: Usa Promise.all para paralelizar
* **Equivalencia**: async/await es equivalente al uso de promesas
* **Arrow functions async**: `async () => { ... }`

#### **🤔 Preguntas de Reflexión:**

1. ¿Por qué una función `async` siempre retorna una promesa?
2. ¿Cuál es la diferencia entre esperar secuencialmente y en paralelo?
3. ¿Cómo maneja `async/await` los errores comparado con `.catch()`?
4. ¿Cuándo usarías `await` vs `Promise.all()`?
5. ¿Qué sucede si olvidas `await` ante una promesa?
6. ¿Por qué es más legible `async/await` que Promise chaining?
7. Convierte una cadena de promesas a `async/await`.

***
