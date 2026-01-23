# Capítulo 4: Combinación de promesas

A veces necesitas trabajar con múltiples promesas simultáneamente: esperar a que todas se resuelvan, esperar a la más rápida, etc. Los **Promise combinators** son métodos estáticos que combinan múltiples promesas en nuevas promesas con comportamientos específicos.

### 4.1. `Promise.all()`: Todas deben cumplirse

`Promise.all()` espera a que **TODAS** las promesas se resuelvan. Si alguna se rechaza, falla todo.

```javascript
// Sintaxis: Promise.all([promesa1, promesa2, ...])

const p1 = Promise.resolve(1);
const p2 = Promise.resolve(2);
const p3 = Promise.resolve(3);

Promise.all([p1, p2, p3]).then((resultados) => {
    console.log(resultados); // [1, 2, 3]
});
```

#### **Caso de uso: Cargar múltiples recursos**

```javascript
function obtenerUsuario(id) {
    return new Promise((resolve) => {
        setTimeout(() => {
            resolve({ id, nombre: `Usuario${id}` });
        }, 1000);
    });
}

function obtenerPosts(usuarioId) {
    return new Promise((resolve) => {
        setTimeout(() => {
            resolve([
                { id: 1, titulo: "Post 1" },
                { id: 2, titulo: "Post 2" }
            ]);
        }, 1500);
    });
}

// Cargar usuario y posts en paralelo
Promise.all([
    obtenerUsuario(1),
    obtenerPosts(1)
]).then(([usuario, posts]) => {
    console.log("Usuario:", usuario);
    console.log("Posts:", posts);
    // Se completa en ~1500ms (no 2500ms)
});
```

**Si alguna falla, todo falla:**

```javascript
const p1 = Promise.resolve("ok");
const p2 = Promise.reject(new Error("Fallo"));
const p3 = Promise.resolve("ok");

Promise.all([p1, p2, p3])
    .then(resultados => console.log(resultados))
    .catch(error => console.error("Error:", error.message));

// Output:
// Error: Fallo
// p3 nunca se ejecuta
```

**Esperar a que terminen todas incluso si fallan:**

Para esto, usa `Promise.allSettled()` ([sección 4.3](capitulo-4-combinacion-de-promesas.md#id-4.3.-promise.allsettled-esperando-a-todas-es2020)).

***

### 4.2. `Promise.race()`: La primera que se resuelva

`Promise.race()` retorna **tan pronto como cualquier promesa** se resuelva o rechace. Las demás continúan pero se ignoran.

```javascript
const p1 = new Promise((resolve) => {
    setTimeout(() => resolve("lento"), 2000);
});

const p2 = new Promise((resolve) => {
    setTimeout(() => resolve("rápido"), 500);
});

Promise.race([p1, p2]).then((resultado) => {
    console.log(resultado); // "rápido"
    // p1 sigue en segundo plano pero se ignora
});
```

#### **Caso de uso: Timeout**

```javascript
function descargarConTimeout(url, timeoutMs) {
    const descarga = fetch(url).then(r => r.json());
    
    const timeout = new Promise((_, reject) => {
        setTimeout(() => {
            reject(new Error("Timeout"));
        }, timeoutMs);
    });
    
    return Promise.race([descarga, timeout]);
}

descargarConTimeout("https://api.example.com/datos", 5000)
    .then(datos => console.log("Datos:", datos))
    .catch(error => console.error("Error:", error.message));
```

***

### 4.3. `Promise.allSettled()`: Esperando a todas (ES2020)

`Promise.allSettled()` espera a que **TODAS** se resuelvan o rechacen, y retorna un array con los resultados y estados.

```javascript
const p1 = Promise.resolve(1);
const p2 = Promise.reject(new Error("Fallo"));
const p3 = Promise.resolve(3);

Promise.allSettled([p1, p2, p3]).then((resultados) => {
    console.log(resultados);
    // [
    //   { status: "fulfilled", value: 1 },
    //   { status: "rejected", reason: Error: Fallo },
    //   { status: "fulfilled", value: 3 }
    // ]
});
```

#### **Procesar resultados:**

```javascript
Promise.allSettled([p1, p2, p3]).then((resultados) => {
    const exitosos = resultados.filter(r => r.status === "fulfilled");
    const errores = resultados.filter(r => r.status === "rejected");
    
    console.log(`Exitosos: ${exitosos.length}, Errores: ${errores.length}`);
});
```

#### **Caso de uso: Descargar múltiples archivos**

```javascript
function descargarMultiples(urls) {
    const descargas = urls.map(url => fetch(url));
    
    return Promise.allSettled(descargas).then((resultados) => {
        const descargados = resultados
            .filter(r => r.status === "fulfilled")
            .map(r => r.value);
        
        const fallidos = resultados
            .filter(r => r.status === "rejected")
            .map(r => r.reason);
        
        return { descargados, fallidos };
    });
}

descargarMultiples([url1, url2, url3, url4])
    .then(({ descargados, fallidos }) => {
        console.log(`Descargados: ${descargados.length}`);
        console.log(`Fallidos: ${fallidos.length}`);
    });
```

***

### 4.4. `Promise.any()`: La primera que se cumpla (ES2021)

`Promise.any()` retorna **tan pronto como UNA se cumpla** (rechazar no cuenta). Si todas se rechazan, falla con `AggregateError`.

```javascript
const p1 = Promise.reject(new Error("Fallo 1"));
const p2 = Promise.reject(new Error("Fallo 2"));
const p3 = Promise.resolve("Éxito");

Promise.any([p1, p2, p3])
    .then(resultado => console.log(resultado)) // "Éxito"
    .catch(error => console.error(error));
```

#### **Si todas se rechazan:**

```javascript
const p1 = Promise.reject(new Error("Error 1"));
const p2 = Promise.reject(new Error("Error 2"));

Promise.any([p1, p2])
    .catch(error => {
        console.log(error instanceof AggregateError); // true
        console.log(error.errors); // [Error, Error]
    });
```

#### **Caso de uso: Probar múltiples servidores**

```javascript
function conectarAServidor() {
    const servidores = [
        "https://servidor1.com",
        "https://servidor2.com",
        "https://servidor3.com"
    ];
    
    const intentos = servidores.map(url => 
        fetch(url).then(() => url)
    );
    
    return Promise.any(intentos);
}

conectarAServidor()
    .then(servidorConexo => console.log("Conectado a:", servidorConexo))
    .catch(error => console.error("Todos los servidores están caídos"));
```

***

### 4.5. Comparación y casos prácticos

| Método                 | Espera          | Retorna                         | Si falla                      |
| ---------------------- | --------------- | ------------------------------- | ----------------------------- |
| **Promise.all**        | Todas           | Array de valores                | Rechaza si alguna falla       |
| **Promise.race**       | Primera         | Valor de la primera             | Rechaza si la primera rechaza |
| **Promise.allSettled** | Todas           | Array de {status, value/reason} | Siempre cumple                |
| **Promise.any**        | Primera exitosa | Valor de la primera exitosa     | Rechaza si todas fallan       |

#### **Patrón: Esperar a todas, continuar con resultados**

```javascript
async function procesarDatos() {
    try {
        const [usuarios, posts, comentarios] = await Promise.all([
            fetch("/usuarios").then(r => r.json()),
            fetch("/posts").then(r => r.json()),
            fetch("/comentarios").then(r => r.json())
        ]);
        
        return { usuarios, posts, comentarios };
    } catch (error) {
        console.error("Error cargando datos:", error);
    }
}
```

***

### Resumen del Capítulo

Los _Promise combinators_ son herramientas poderosas para manejar múltiples operaciones asincrónicas. Usa `Promise.all()` cuando necesites que todas tengan éxito, `Promise.race()` para la más rápida, `Promise.allSettled()` cuando quieras resultados incluso si algunas fallan, y `Promise.any()` cuando necesites la primera que tenga éxito.

#### **💡 Conceptos Clave:**

* **Promise.all()**: Todas deben cumplirse
* **Promise.race()**: La primera que termine
* **Promise.allSettled()**: Todas terminan, incluso si fallan
* **Promise.any()**: Primera que se cumpla exitosamente
* **AggregateError**: Error cuando todas fallan en Promise.any()
* **Ejecución en paralelo**: Los combinators ejecutan en paralelo, no secuencial
* **Casos de uso**: Cargas múltiples, timeouts, servidores redundantes

#### **🤔 Preguntas de Reflexión:**

1. ¿Cuál es la diferencia entre Promise.all y Promise.allSettled?
2. ¿Cuándo usarías Promise.race sobre Promise.any?
3. ¿Qué sucede si una Promise en Promise.all se rechaza?
4. ¿Cómo implementarías un timeout usando Promise.race?
5. ¿Cuál es el rendimiento de ejecutar múltiples fetch con Promise.all vs secuencialmente?
6. Crea un escenario donde usarías Promise.allSettled para procesar resultados.

***
