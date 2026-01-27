# Capítulo 8: Peticiones POST/PUT/DELETE

Hasta ahora solo hemos hecho peticiones GET (obtener datos). Ahora aprenderemos a **enviar datos** al servidor usando POST, PUT y DELETE para operaciones CRUD completas.

### 8.1. Configurar el objeto `options` en `fetch`

Para cambiar el método HTTP y enviar datos, usamos el segundo parámetro de `fetch()`:

```javascript
// GET (por defecto, sin opciones)
fetch("/api/usuarios");

// POST (con opciones)
fetch("/api/usuarios", {
    method: "POST",
    headers: {
        "Content-Type": "application/json"
    },
    body: JSON.stringify({ nombre: "Juan", email: "juan@example.com" })
});
```

#### **Objeto `options` completo:**

```javascript
const options = {
    method: "POST",              // GET, POST, PUT, DELETE, PATCH, etc.
    headers: {                   // Headers HTTP
        "Content-Type": "application/json",
        "Authorization": "Bearer TOKEN"
    },
    body: JSON.stringify(datos), // Para POST/PUT/DELETE
    mode: "cors",                // cors, no-cors, same-origin
    credentials: "include",      // Incluir cookies
    timeout: 5000                // Timeout en ms (algunos navegadores)
};

fetch("/api/endpoint", options);
```

***

### 8.2. Body: `JSON.stringify` y `Content-Type`

El `body` es el contenido que enviamos al servidor. **Debe ser una cadena**, no un objeto.

```javascript
// ❌ ERROR: Pasar un objeto directamente
fetch("/api/usuarios", {
    method: "POST",
    body: { nombre: "Juan" } // ❌ Error: debe ser string
});

// ✓ CORRECTO: Usar JSON.stringify
const datos = { nombre: "Juan", email: "juan@example.com" };
fetch("/api/usuarios", {
    method: "POST",
    headers: {
        "Content-Type": "application/json" // Indicar que es JSON
    },
    body: JSON.stringify(datos) // ✓ Convertir a string
});
```

#### **Content-Type (tipo de contenido):**

```javascript
// JSON (más común)
headers: {
    "Content-Type": "application/json"
}
body: JSON.stringify(datos)

// Form data (enviar archivos)
headers: {
    // ¡NO establecer Content-Type! El navegador lo hará automáticamente
}
body: new FormData()

// Texto plano
headers: {
    "Content-Type": "text/plain"
}
body: "Texto simple"

// URL encoded (formularios tradicionales)
headers: {
    "Content-Type": "application/x-www-form-urlencoded"
}
body: "nombre=Juan&email=juan@example.com"
```

***

### 8.3. Método `POST`: Enviar datos

POST se usa para **crear nuevos recursos**.

```javascript
async function crearUsuario(usuario) {
    try {
        const respuesta = await fetch("/api/usuarios", {
            method: "POST",
            headers: {
                "Content-Type": "application/json"
            },
            body: JSON.stringify(usuario)
        });
        
        if (!respuesta.ok) {
            throw new Error(`HTTP ${respuesta.status}`);
        }
        
        const usuarioCreado = await respuesta.json();
        console.log("Usuario creado:", usuarioCreado);
        
        return usuarioCreado;
        
    } catch (error) {
        console.error("Error al crear usuario:", error);
    }
}

// Usar
crearUsuario({
    nombre: "Juan García",
    email: "juan@example.com",
    edad: 30
});
```

#### **Ejemplo con JSONPlaceholder:**

```javascript
async function crearPost() {
    try {
        const respuesta = await fetch(
            "https://jsonplaceholder.typicode.com/posts",
            {
                method: "POST",
                headers: {
                    "Content-Type": "application/json"
                },
                body: JSON.stringify({
                    title: "Mi primer post",
                    body: "Este es el contenido del post",
                    userId: 1
                })
            }
        );
        
        const post = await respuesta.json();
        console.log("Post creado:", post);
        // Nota: JSONPlaceholder simula la creación, no persiste realmente
        
    } catch (error) {
        console.error("Error:", error);
    }
}

crearPost();
```

***

### 8.4. Métodos `PUT` y `DELETE`: Actualizar y eliminar

#### **`PUT`: Actualizar un recurso existente**

```javascript
async function actualizarUsuario(userId, datosActualizados) {
    try {
        const respuesta = await fetch(`/api/usuarios/${userId}`, {
            method: "PUT",
            headers: {
                "Content-Type": "application/json"
            },
            body: JSON.stringify(datosActualizados)
        });
        
        if (!respuesta.ok) {
            throw new Error(`HTTP ${respuesta.status}`);
        }
        
        const usuarioActualizado = await respuesta.json();
        return usuarioActualizado;
        
    } catch (error) {
        console.error("Error al actualizar:", error);
    }
}

// Usar
actualizarUsuario(1, { nombre: "Juan Nuevo", edad: 31 });
```

#### **`DELETE`: Eliminar un recurso**

```javascript
async function eliminarUsuario(userId) {
    try {
        const respuesta = await fetch(`/api/usuarios/${userId}`, {
            method: "DELETE"
            // No necesita body ni Content-Type
        });
        
        if (!respuesta.ok) {
            throw new Error(`HTTP ${respuesta.status}`);
        }
        
        console.log("Usuario eliminado");
        
    } catch (error) {
        console.error("Error al eliminar:", error);
    }
}

// Usar
eliminarUsuario(1);
```

#### **`PATCH`: Actualizar parcialmente**

```javascript
// Similar a PUT, pero solo actualiza los campos especificados
async function actualizarParcial(userId, cambios) {
    const respuesta = await fetch(`/api/usuarios/${userId}`, {
        method: "PATCH",
        headers: {
            "Content-Type": "application/json"
        },
        body: JSON.stringify(cambios)
    });
    
    return await respuesta.json();
}

// Solo actualiza nombre, mantiene otros campos
actualizarParcial(1, { nombre: "Juan Nuevo" });
```

***

### 8.5. Ejemplo completo: CRUD con una API

Aquí está un ejemplo completo de operaciones CRUD:

```javascript
const API_URL = "https://jsonplaceholder.typicode.com/users";

// CREATE: Crear un nuevo usuario
async function crearUsuario(usuario) {
    const respuesta = await fetch(API_URL, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(usuario)
    });
    return await respuesta.json();
}

// READ: Obtener todos los usuarios
async function obtenerUsuarios() {
    const respuesta = await fetch(API_URL);
    return await respuesta.json();
}

// READ: Obtener un usuario específico
async function obtenerUsuario(id) {
    const respuesta = await fetch(`${API_URL}/${id}`);
    return await respuesta.json();
}

// UPDATE: Actualizar un usuario
async function actualizarUsuario(id, datos) {
    const respuesta = await fetch(`${API_URL}/${id}`, {
        method: "PUT",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(datos)
    });
    return await respuesta.json();
}

// DELETE: Eliminar un usuario
async function eliminarUsuario(id) {
    const respuesta = await fetch(`${API_URL}/${id}`, {
        method: "DELETE"
    });
    return respuesta.ok;
}

// Ejemplo de uso:
(async () => {
    // Leer
    const usuarios = await obtenerUsuarios();
    console.log("Usuarios:", usuarios.length);
    
    // Crear
    const nuevoUsuario = await crearUsuario({
        name: "Juan García",
        email: "juan@example.com"
    });
    console.log("Usuario creado:", nuevoUsuario.id);
    
    // Actualizar
    const actualizado = await actualizarUsuario(1, {
        name: "Juan Actualizado"
    });
    console.log("Actualizado:", actualizado.name);
    
    // Eliminar
    const eliminado = await eliminarUsuario(1);
    console.log("Eliminado:", eliminado);
})();
```

***

### 8.6. Códigos de estado HTTP comunes

Al trabajar con POST/PUT/DELETE, es importante entender los códigos:

| Código | Significado  | Acción                                 |
| ------ | ------------ | -------------------------------------- |
| 200    | OK           | Operación exitosa (generalmente GET)   |
| 201    | Created      | Recurso creado (POST)                  |
| 204    | No Content   | Éxito pero sin contenido (DELETE, PUT) |
| 400    | Bad Request  | Datos inválidos                        |
| 401    | Unauthorized | No autenticado                         |
| 403    | Forbidden    | No autorizado                          |
| 404    | Not Found    | Recurso no existe                      |
| 409    | Conflict     | Conflicto (duplicado, etc.)            |
| 500    | Server Error | Error del servidor                     |

***

### Resumen del Capítulo

POST, PUT y DELETE permiten manipular datos en el servidor. Siempre recuerda usar `JSON.stringify()` para el body, establecer el `Content-Type` correcto, y verificar los códigos de estado HTTP para manejo de errores apropiado.

#### **💡 Conceptos Clave:**

* **method**: GET, POST, PUT, DELETE, PATCH
* **headers**: Content-Type y autenticación
* **body**: Datos a enviar (como string JSON)
* **JSON.stringify()**: Convertir objeto a string
* **POST**: Crear recursos (status 201)
* **PUT**: Actualizar completamente
* **PATCH**: Actualizar parcialmente
* **DELETE**: Eliminar recursos
* **Códigos HTTP**: Interpretación de respuestas

#### **🤔 Preguntas de Reflexión:**

1. ¿Cuál es la diferencia entre PUT y PATCH?
2. ¿Por qué necesitas usar `JSON.stringify()` en el body?
3. ¿Qué es Content-Type y por qué es importante?
4. ¿Cuál es el código HTTP esperado para POST exitoso?
5. ¿Cómo manejarías un error 409 (Conflict)?
6. Crea una función CRUD completa para un recurso.

***
