# Capítulo 6: Introducción a Fetch API

La **Fetch API** es la forma moderna de hacer peticiones HTTP desde JavaScript. Reemplaza el antiguo `XMLHttpRequest` con una interfaz mucho más limpia y basada en promesas.

### 6.1. ¿Qué es Fetch? Reemplazo moderno de `XMLHttpRequest`

`XMLHttpRequest` era la forma antigua de hacer peticiones (complicada y verbosa):

```javascript
// ❌ Antiguo: XMLHttpRequest (complicado)
const xhr = new XMLHttpRequest();
xhr.open("GET", "/datos.json");
xhr.onload = () => console.log(xhr.responseText);
xhr.onerror = () => console.error("Error");
xhr.send();
```

`Fetch API` es moderna, basada en promesas, mucho más limpia:

```javascript
// ✓ Moderno: Fetch (simple)
fetch("/datos.json")
    .then(respuesta => respuesta.json())
    .then(datos => console.log(datos))
    .catch(error => console.error("Error:", error));
```

***

### 6.2. `fetch(url, options)`: Parámetros y objeto Response

`fetch()` toma dos parámetros: la URL y un objeto de opciones (opcional).

```javascript
// Sintaxis: fetch(url, options?)

// GET simple (sin options)
fetch("/datos.json");

// CON opciones
fetch("/datos.json", {
    method: "GET",           // GET, POST, PUT, DELETE, etc.
    headers: {               // Headers HTTP
        "Content-Type": "application/json"
    },
    body: JSON.stringify({ nombre: "Juan" }) // Para POST/PUT
});
```

#### **El objeto Response:**

```javascript
fetch("/datos.json").then(respuesta => {
    console.log(respuesta.status);      // 200, 404, 500, etc.
    console.log(respuesta.ok);          // true si 200-299
    console.log(respuesta.headers);     // Headers de la respuesta
    console.log(respuesta.url);         // URL de la respuesta
});
```

***

### 6.3. Peticiones GET: Obtener datos JSON

GET es el método por defecto. Se usa para obtener datos.

```javascript
// GET simple
fetch("/api/usuarios")
    .then(respuesta => {
        // Verificar si la petición fue exitosa
        if (!respuesta.ok) {
            throw new Error(`HTTP Error: ${respuesta.status}`);
        }
        return respuesta;
    })
    .then(respuesta => respuesta.json()) // Parsear JSON
    .then(datos => console.log(datos))
    .catch(error => console.error("Error:", error));

// Con async/await (más legible)
async function obtenerUsuarios() {
    try {
        const respuesta = await fetch("/api/usuarios");
        
        if (!respuesta.ok) {
            throw new Error(`HTTP Error: ${respuesta.status}`);
        }
        
        const datos = await respuesta.json();
        console.log(datos);
    } catch (error) {
        console.error("Error:", error);
    }
}
```

#### **Parámetros en la URL:**

```javascript
// Query string
const url = new URL("https://api.example.com/usuarios");
url.searchParams.append("id", "1");
url.searchParams.append("nombre", "Juan");

fetch(url)
    .then(r => r.json())
    .then(datos => console.log(datos));
    
// URL resultante: https://api.example.com/usuarios?id=1&nombre=Juan
```

***

### 6.4. Métodos del Response: `.json()`, `.text()`, `.blob()`

Después de obtener la respuesta, puedes parsearla de diferentes formas:

```javascript
const respuesta = await fetch("/datos");

// .json(): Parsear como JSON
const json = await respuesta.json();

// .text(): Obtener como texto plano
const texto = await respuesta.text();

// .blob(): Obtener como binario (para descargar archivos)
const blob = await respuesta.blob();

// .arrayBuffer(): Obtener como buffer binario
const buffer = await respuesta.arrayBuffer();

// .clone(): Copiar la respuesta (solo se puede leer una vez)
const copia = respuesta.clone();
```

***

### 6.5. Manejo de errores: Red vs HTTP status

Es importante entender que hay **dos tipos de errores**:

1. **Errores de red**: No hay conexión (fetch rechaza)
2. **Errores HTTP**: Servidor retorna 404, 500, etc. (fetch resuelve igual)

```javascript
// IMPORTANTE: Fetch NO rechaza para códigos de error HTTP
async function obtenerDatos() {
    try {
        const respuesta = await fetch("/datos");
        
        // 404, 500, etc. NO causan error aquí
        // Necesitas verificar respuesta.ok o respuesta.status
        
        if (!respuesta.ok) {
            // Ahora sí: HTTP Error
            throw new Error(`HTTP ${respuesta.status}`);
        }
        
        return await respuesta.json();
        
    } catch (error) {
        // Aquí capturamos:
        // - Errores de red (conexión perdida)
        // - Errores de parseo (JSON inválido)
        // - Errores que lanzamos nosotros (HTTP Error)
        console.error("Error:", error.message);
    }
}
```

#### **Códigos HTTP comunes:**

```javascript
const respuesta = await fetch("/api/usuarios");

if (respuesta.status === 200) {
    console.log("OK");
} else if (respuesta.status === 404) {
    console.log("No encontrado");
} else if (respuesta.status === 500) {
    console.log("Error del servidor");
} else if (respuesta.status === 401) {
    console.log("No autorizado");
}

// O simplemente usar .ok
if (respuesta.ok) {
    console.log("Éxito");
} else {
    console.log("Fallo", respuesta.status);
}
```

***

### 6.6. Ejemplo completo: Cargar datos y mostrar en consola

```javascript
async function cargarDatos() {
    const url = "https://jsonplaceholder.typicode.com/posts/1";
    
    try {
        console.log("Descargando...");
        
        const respuesta = await fetch(url);
        
        if (!respuesta.ok) {
            throw new Error(`HTTP ${respuesta.status}`);
        }
        
        const post = await respuesta.json();
        
        console.log("Post cargado:");
        console.log("Título:", post.title);
        console.log("Contenido:", post.body);
        
    } catch (error) {
        console.error("Error al descargar:", error.message);
    }
}

cargarDatos();
```

***

### Resumen del Capítulo

Fetch API es la forma moderna y recomendada de hacer peticiones HTTP en JavaScript. Siempre recuerda verificar `respuesta.ok` o `respuesta.status` para diferenciar entre éxito y error HTTP, ya que Fetch no rechaza automáticamente en esos casos.

#### **💡 Conceptos Clave:**

* **fetch()**: Función para peticiones HTTP
* **URL y options**: Parámetros de configuración
* **Response object**: Información de la respuesta
* **.json(), .text(), .blob()**: Parsear respuesta
* **respuesta.ok**: Verificar si fue exitosa
* **respuesta.status**: Código HTTP
* **Errores de red**: Fetch rechaza
* **Errores HTTP**: Debes verificar manualmente

#### **🤔 Preguntas de Reflexión:**

1. ¿Cuál es la diferencia entre Fetch API y XMLHttpRequest?
2. ¿Por qué necesitas verificar respuesta.ok en lugar de solo usar .then()?
3. ¿Cuándo usarías .json() vs .text()?
4. ¿Qué sucede si fetch falla? ¿Se rechaza la promesa?
5. ¿Cómo pasarías parámetros en una URL con Fetch?
6. ¿Cuál es la diferencia entre un error de red y un error HTTP?

***
