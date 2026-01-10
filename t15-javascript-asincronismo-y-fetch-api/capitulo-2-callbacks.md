# Capítulo 2: Callbacks

Los callbacks son la forma fundamental de trabajar con código asíncrono en JavaScript. Un callback es simplemente una función que se pasa como argumento a otra función para que sea ejecutada posteriormente. Este capítulo cubre cómo usarlos correctamente y sus limitaciones.

### 2.1. ¿Qué es un callback? Función pasada como argumento

Un **callback** es una función que se pasa a otra función como argumento, para que sea llamada más tarde.

```javascript
// Ejemplo simple
function saludar(nombre, callback) {
    console.log(`Hola, ${nombre}`);
    callback(); // Ejecutar el callback
}

function despedir() {
    console.log("¡Adiós!");
}

saludar("Juan", despedir);

// Output:
// Hola, Juan
// ¡Adiós!
```

Los callbacks se usan típicamente en código **asíncrono** para ejecutar una función cuando una operación termina:

```javascript
// Callback asíncrono
function cargarDatos(url, callback) {
    setTimeout(() => {
        const datos = { id: 1, nombre: "Juan" };
        callback(datos); // Ejecutar cuando se "cargan los datos"
    }, 2000);
}

cargarDatos("https://api.example.com/usuarios/1", (datos) => {
    console.log("Datos cargados:", datos);
});

// Output (después de 2s):
// Datos cargados: { id: 1, nombre: "Juan" }
```

***

### 2.2. Callbacks síncronos vs asíncronos

#### **Callbacks síncronos (ejecutados inmediatamente)**

```javascript
// Callback síncrono: Se ejecuta dentro de la función
const numeros = [1, 2, 3, 4, 5];

numeros.forEach((num) => {
    console.log(num);
});

// Output (inmediato):
// 1
// 2
// 3
// 4
// 5

// El callback se ejecuta inmediatamente, NO hay espera
```

#### **Callbacks asíncronos (ejecutados después)**

```javascript
// Callback asíncrono: Se ejecuta después
function downloadFile(url, callback) {
    console.log("Descargando...");
    
    setTimeout(() => {
        console.log("Descarga completa");
        callback("archivo.pdf"); // Se ejecuta después de 3 segundos
    }, 3000);
}

downloadFile("https://example.com/archivo.pdf", (nombreArchivo) => {
    console.log(`Archivo descargado: ${nombreArchivo}`);
});

// Output:
// Descargando...
// (3 segundos después...)
// Descarga completa
// Archivo descargado: archivo.pdf
```

***

### 2.3. Error-first callbacks: Patrón estándar

En JavaScript, existe un patrón estándar para callbacks asíncronos: el **error-first callback**. El primer argumento es siempre un error (o null si no hay error).

```javascript
// Patrón error-first
function leerArchivo(ruta, callback) {
    setTimeout(() => {
        // Simulamos un error en este caso
        const error = new Error("Archivo no encontrado");
        const datos = null;
        
        // Pasar (error, datos) al callback
        callback(error, datos);
    }, 1000);
}

leerArchivo("config.json", (error, datos) => {
    if (error) {
        console.error("Error:", error.message);
    } else {
        console.log("Datos:", datos);
    }
});

// Output (después de 1s):
// Error: Archivo no encontrado
```

**Ejemplo exitoso:**

```javascript
function obtenerUsuario(id, callback) {
    setTimeout(() => {
        if (id > 0) {
            const usuario = { id, nombre: "Juan" };
            callback(null, usuario); // null = sin error
        } else {
            const error = new Error("ID inválido");
            callback(error, null);
        }
    }, 500);
}

obtenerUsuario(1, (error, usuario) => {
    if (error) {
        console.error("Error:", error.message);
    } else {
        console.log("Usuario:", usuario);
    }
});

// Output:
// Usuario: { id: 1, nombre: "Juan" }
```

***

### 2.4. Limitaciones: El "callback hell" o "pyramid of doom"

Cuando necesitas hacer múltiples operaciones asíncronas en secuencia, los callbacks se anidan cada vez más. Esto es el **"callback hell"**.

**Ejemplo del problema:**

```javascript
// CALLBACK HELL: Muy difícil de leer y mantener
function procesarPedido(pedidoId, callback) {
    obtenerPedido(pedidoId, (error, pedido) => {
        if (error) {
            callback(error);
        } else {
            obtenerCliente(pedido.clienteId, (error, cliente) => {
                if (error) {
                    callback(error);
                } else {
                    obtenerFactura(pedido.id, (error, factura) => {
                        if (error) {
                            callback(error);
                        } else {
                            procesarPago(factura.total, (error, pago) => {
                                if (error) {
                                    callback(error);
                                } else {
                                    callback(null, {
                                        pedido,
                                        cliente,
                                        factura,
                                        pago
                                    });
                                }
                            });
                        }
                    });
                }
            });
        }
    });
}

// ¡La pirámide es cada vez más profunda!
```

**Por qué es un problema:**

1. **Difícil de leer**: Tienes que seguir la indentación
2. **Difícil de mantener**: Añadir lógica nueva requiere reorganizar todo
3. **Gestión de errores incómoda**: Necesitas `if (error)` en cada nivel
4. **Propenso a errores**: Fácil cometer fallos

***

### 2.5. Cuándo usar callbacks y cuándo evitarlos

#### **✓ Usar callbacks cuando:**

* Son callbacks síncronos de bibliotecas (Array.forEach, Array.map)
* Trabajas con APIs antiguas que solo soportan callbacks
* El flujo es simple (una o dos operaciones)

```javascript
// BIEN: Un solo callback (simple)
function cargarDatos(callback) {
    setTimeout(() => {
        callback(null, [1, 2, 3]);
    }, 1000);
}

cargarDatos((error, datos) => {
    if (!error) {
        console.log(datos);
    }
});
```

#### **❌ Evitar callbacks cuando:**

* Necesitas múltiples operaciones en secuencia
* Quieres código más legible y mantenible
* Necesitas un mejor manejo de errores

```javascript
// EVITAR: Múltiples operaciones anidadas
// Usa Promises o async/await en su lugar
```

***

### 2.6. Convertir callbacks en Promesas

La solución al callback hell es usar **Promesas** (siguiente capítulo), pero puedes convertir un callback a una promesa:

```javascript
// Función con callback
function obtenerDatos(callback) {
    setTimeout(() => {
        callback(null, { id: 1, nombre: "Juan" });
    }, 1000);
}

// Convertir a Promise (promisify)
function obtenerDatosPromesa() {
    return new Promise((resolve, reject) => {
        obtenerDatos((error, datos) => {
            if (error) {
                reject(error);
            } else {
                resolve(datos);
            }
        });
    });
}

// Ahora es mucho más legible
obtenerDatosPromesa()
    .then(datos => console.log("Datos:", datos))
    .catch(error => console.error("Error:", error));
```

***

### Resumen del Capítulo

Los callbacks son la forma más básica de trabajar con código asíncrono, pero tienen limitaciones importantes. Para múltiples operaciones secuenciales, el anidamiento de callbacks crea código ilegible (callback hell). Las Promesas, que veremos en el próximo capítulo, resuelven este problema.

#### **💡 Conceptos Clave:**

* **Callback**: Función pasada como argumento para ejecutar después
* **Callbacks síncronos**: Se ejecutan inmediatamente (ej: Array.forEach)
* **Callbacks asíncronos**: Se ejecutan después (ej: setTimeout)
* **Error-first pattern**: Primer argumento es el error (null si sin error)
* **Callback hell**: Anidamiento profundo cuando hay múltiples operaciones
* **"Pyramid of doom"**: Indentación cada vez más profunda
* **Promisify**: Convertir callbacks a Promesas
* **Limitación**: Difícil de leer y mantener con múltiples operaciones

#### **🤔 Preguntas de Reflexión:**

1. ¿Cuál es la diferencia entre un callback síncrono y uno asíncrono?
2. ¿Qué es el patrón error-first callback y por qué es estándar?
3. ¿Qué es "callback hell" y cuándo aparece?
4. ¿Por qué es difícil de mantener el código con muchos callbacks anidados?
5. ¿Cómo convertirías una función con callback en una Promesa?
6. ¿En qué casos seguirías usando callbacks en lugar de Promesas?
7. Escribe una función que acepta un callback y es ejecutada asíncronamente.

***
