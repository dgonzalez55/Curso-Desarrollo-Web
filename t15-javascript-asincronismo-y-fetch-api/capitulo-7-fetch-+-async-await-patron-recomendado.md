# Capítulo 7: Fetch + Async/Await (Patrón Recomendado)

La combinación de Fetch API con `async/await` es el patrón recomendado en JavaScript moderno. Es claro, legible y fácil de mantener. Este capítulo consolida todo lo anterior.

### 7.1. Reescribir promesas con async/await

Ya conoces ambos patrones. Ahora veamos cómo convertirlos entre ellos.

#### **Promise chaining (antiguo patrón):**

```javascript
function obtenerPost(id) {
    return fetch(`/api/posts/${id}`)
        .then(respuesta => {
            if (!respuesta.ok) throw new Error(`HTTP ${respuesta.status}`);
            return respuesta.json();
        })
        .then(post => {
            console.log("Post obtenido:", post.title);
            return post;
        })
        .catch(error => {
            console.error("Error:", error);
        });
}
```

#### **`Async/Await` (patrón moderno):**

```javascript
async function obtenerPost(id) {
    try {
        const respuesta = await fetch(`/api/posts/${id}`);
        
        if (!respuesta.ok) throw new Error(`HTTP ${respuesta.status}`);
        
        const post = await respuesta.json();
        console.log("Post obtenido:", post.title);
        
        return post;
        
    } catch (error) {
        console.error("Error:", error);
    }
}
```

La versión con `async/await` es **más clara** porque se lee como código síncrono.

***

### 7.2. Estructura típica: `fetch` → `ok` → `json()`

Este es el patrón estándar que verás en todas partes:

```javascript
async function obtenerDatos(url) {
    try {
        // 1. Hacer la petición
        const respuesta = await fetch(url);
        
        // 2. Verificar que fue exitosa
        if (!respuesta.ok) {
            throw new Error(`HTTP Error: ${respuesta.status}`);
        }
        
        // 3. Parsear el JSON
        const datos = await respuesta.json();
        
        // 4. Retornar los datos
        return datos;
        
    } catch (error) {
        console.error("Error:", error);
        // Retornar null o un valor por defecto
        return null;
    }
}

// Usar
const datos = await obtenerDatos("/api/usuarios");
console.log(datos);
```

***

### 7.3. Manejo de errores con `try/catch`

`try/catch` es el mecanismo estándar para manejar errores asíncronos.

```javascript
async function descargarArchivo(url) {
    try {
        // Intenta descargar
        const respuesta = await fetch(url);
        
        // Error HTTP
        if (!respuesta.ok) {
            throw new Error(`No se puede descargar: ${respuesta.status}`);
        }
        
        const blob = await respuesta.blob();
        return blob;
        
    } catch (error) {
        // Aquí caen:
        // - Errores de red
        // - Errores HTTP que lanzamos
        // - Errores de parseo
        
        console.error("Error al descargar:", error.message);
        
        // Puedes retornar un valor por defecto
        return null;
        
    } finally {
        // Se ejecuta siempre (limpiar recursos, etc.)
        console.log("Operación completada");
    }
}
```

***

### 7.4. Casos prácticos: APIs públicas

Aquí hay ejemplos reales usando APIs públicas gratuitas:

#### **JSONPlaceholder (API de prueba):**

```javascript
async function obtenerPostsDeUsuario(userId) {
    try {
        const respuesta = await fetch(
            `https://jsonplaceholder.typicode.com/posts?userId=${userId}`
        );
        
        if (!respuesta.ok) {
            throw new Error(`HTTP ${respuesta.status}`);
        }
        
        const posts = await respuesta.json();
        return posts;
        
    } catch (error) {
        console.error("Error:", error);
        return [];
    }
}

// Usar
obtenerPostsDeUsuario(1).then(posts => {
    console.log("Posts del usuario 1:", posts.length);
    posts.forEach(post => console.log("- ", post.title));
});
```

#### **OpenWeather (Datos meteorológicos):**

```javascript
async function obtenerClima(ciudad) {
    const apiKey = "TU_API_KEY"; // Necesitas registrarte
    const url = `https://api.openweathermap.org/data/2.5/weather?q=${ciudad}&appid=${apiKey}&units=metric`;
    
    try {
        const respuesta = await fetch(url);
        
        if (!respuesta.ok) {
            throw new Error(`Ciudad no encontrada: ${respuesta.status}`);
        }
        
        const datos = await respuesta.json();
        
        return {
            ciudad: datos.name,
            temperatura: datos.main.temp,
            descripcion: datos.weather[0].description
        };
        
    } catch (error) {
        console.error("Error al obtener clima:", error);
        return null;
    }
}

// Usar
const clima = await obtenerClima("Madrid");
console.log(`Clima en ${clima.ciudad}: ${clima.temperatura}°C`);
```

***

### 7.5. Depuración: Inspeccionar respuestas

Cuando algo no funciona, es útil inspeccionar qué retorna la API:

```javascript
async function debugFetch(url) {
    console.log("📤 Haciendo petición a:", url);
    
    try {
        const respuesta = await fetch(url);
        
        console.log("📥 Status:", respuesta.status);
        console.log("📥 OK:", respuesta.ok);
        console.log("📥 Headers:", respuesta.headers);
        
        const datos = await respuesta.json();
        console.log("📥 Datos:", datos);
        
        return datos;
        
    } catch (error) {
        console.error("❌ Error:", error);
        console.error("Mensaje:", error.message);
        console.error("Stack:", error.stack);
    }
}
```

***

### 7.6. Patrón: Función reutilizable para `fetch`

Es común crear una función genérica para manejar el patrón estándar:

```javascript
// Función auxiliar genérica
async function apiCall(url, opciones = {}) {
    try {
        const config = {
            method: "GET",
            headers: {
                "Content-Type": "application/json",
                ...opciones.headers
            },
            ...opciones
        };
        
        const respuesta = await fetch(url, config);
        
        if (!respuesta.ok) {
            throw new Error(`HTTP Error ${respuesta.status}`);
        }
        
        return await respuesta.json();
        
    } catch (error) {
        console.error("API Error:", error);
        throw error; // Re-lanzar para que el llamador lo maneje
    }
}

// Usar
try {
    const usuarios = await apiCall("/api/usuarios");
    console.log(usuarios);
} catch (error) {
    console.error("No se pudieron cargar usuarios:", error);
}
```

***

### 7.7. Peticiones simultáneas con `Promise.all`

Para cargar múltiples recursos eficientemente:

```javascript
async function cargarDatosPerfil(userId) {
    try {
        // Cargar todo en paralelo
        const [usuario, posts, comentarios] = await Promise.all([
            apiCall(`/api/usuarios/${userId}`),
            apiCall(`/api/posts?userId=${userId}`),
            apiCall(`/api/comentarios?userId=${userId}`)
        ]);
        
        return {
            usuario,
            posts: posts.length,
            comentarios: comentarios.length
        };
        
    } catch (error) {
        console.error("Error cargando perfil:", error);
        return null;
    }
}

// Usar
const perfil = await cargarDatosPerfil(1);
console.log(`Usuario ${perfil.usuario.name} tiene ${perfil.posts} posts`);
```

***

### Resumen del Capítulo

`async/await` + Fetch es el patrón moderno recomendado para trabajar con APIs en JavaScript. Es legible, mantenible y funciona perfectamente con `try/catch` para manejar errores. Combina Fetch con `Promise.all()` para operaciones paralelas eficientes.

#### **💡 Conceptos Clave:**

* **async/await sobre Fetch**: El patrón recomendado
* **Estructura: fetch → ok → json()**: El flujo estándar
* **try/catch**: Manejo de errores
* **finally**: Limpiar recursos
* **Promise.all**: Cargar múltiples recursos en paralelo
* **Debugging**: Inspeccionar respuestas con console.log
* **Funciones reutilizables**: Crear helpers genéricos
* **APIs públicas**: JSONPlaceholder para pruebas

#### **🤔 Preguntas de Reflexión:**

1. ¿Por qué `async/await` es más legible que Promise chaining?
2. ¿Cuál es el patrón estándar para fetch?
3. ¿Cómo usarías `Promise.all` para cargar múltiples recursos?
4. ¿Cuándo usarías `finally` en una operación fetch?
5. ¿Cómo crearías una función reutilizable para fetch?
6. ¿Qué diferencia hay entre error de red y error HTTP?
7. Crea una función que cargue datos de dos APIs y los combine.

***
