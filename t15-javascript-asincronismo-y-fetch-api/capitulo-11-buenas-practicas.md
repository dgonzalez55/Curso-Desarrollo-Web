# Capítulo 11: Buenas Prácticas

Este capítulo final, antes del proyecto integrador, debe permitirnos consolidar los patrones profesionales que permiten escribir código asincrónico mantenible, escalable y robusto.

### 11.1. Centralizar llamadas a APIs (módulos)

En lugar de hacer peticiones fetch esparcidas por el código, **crea un módulo API centralizado**:

```javascript
// api.js - Módulo centralizado para todas las peticiones

const API_BASE = "https://api.example.com";

// Configuración global
const defaultOptions = {
    headers: {
        "Content-Type": "application/json"
    }
};

// Función base para todas las peticiones
async function apiCall(endpoint, opciones = {}) {
    const url = `${API_BASE}${endpoint}`;
    
    const config = {
        ...defaultOptions,
        ...opciones,
        headers: {
            ...defaultOptions.headers,
            ...opciones.headers
        }
    };
    
    try {
        const respuesta = await fetch(url, config);
        
        // Manejo centralizado de errores HTTP
        if (!respuesta.ok) {
            const error = new Error();
            error.status = respuesta.status;
            error.statusText = respuesta.statusText;
            throw error;
        }
        
        return await respuesta.json();
        
    } catch (error) {
        console.error(`Error en ${endpoint}:`, error);
        throw error;
    }
}

// Funciones específicas (abstractas)
const usuarios = {
    obtenerTodos: () => apiCall("/usuarios"),
    obtenerPor: (id) => apiCall(`/usuarios/${id}`),
    crear: (datos) => apiCall("/usuarios", {
        method: "POST",
        body: JSON.stringify(datos)
    }),
    actualizar: (id, datos) => apiCall(`/usuarios/${id}`, {
        method: "PUT",
        body: JSON.stringify(datos)
    }),
    eliminar: (id) => apiCall(`/usuarios/${id}`, {
        method: "DELETE"
    })
};

const posts = {
    obtenerTodos: () => apiCall("/posts"),
    obtenerPorUsuario: (userId) => apiCall(`/posts?userId=${userId}`),
    crear: (datos) => apiCall("/posts", {
        method: "POST",
        body: JSON.stringify(datos)
    })
};

// Exportar
export { usuarios, posts };
```

#### **Uso desde la aplicación:**

```javascript
import { usuarios, posts } from "./api.js";

// Uso simple y consistente
try {
    const usuarios = await usuarios.obtenerTodos();
    const posts = await posts.obtenerTodos();
} catch (error) {
    console.error("Error cargando datos:", error);
}
```

***

### 11.2. Manejo consistente de errores

Crea patrones consistentes para errores:

```javascript
// errorHandler.js

class ApiError extends Error {
    constructor(status, message) {
        super(message);
        this.status = status;
        this.name = "ApiError";
    }
}

// Clasificar errores
function clasificarError(error) {
    if (error instanceof ApiError) {
        switch (error.status) {
            case 400:
                return { tipo: "VALIDACION", mensaje: "Datos inválidos" };
            case 401:
                return { tipo: "AUTENTICACION", mensaje: "No autenticado" };
            case 403:
                return { tipo: "AUTORIZACION", mensaje: "No autorizado" };
            case 404:
                return { tipo: "NO_ENCONTRADO", mensaje: "Recurso no encontrado" };
            case 500:
                return { tipo: "SERVIDOR", mensaje: "Error del servidor" };
            default:
                return { tipo: "DESCONOCIDO", mensaje: "Error desconocido" };
        }
    }
    
    if (error.name === "AbortError") {
        return { tipo: "CANCELADO", mensaje: "Operación cancelada" };
    }
    
    return { tipo: "RED", mensaje: "Error de conexión" };
}

// Mostrar error al usuario
function mostrarErrorUI(error) {
    const { tipo, mensaje } = clasificarError(error);
    
    const elemento = document.createElement("div");
    elemento.className = `error error-${tipo.toLowerCase()}`;
    elemento.innerHTML = `
        <strong>Error:</strong> ${mensaje}
        <button onclick="this.parentElement.remove()">✕</button>
    `;
    
    document.body.appendChild(elemento);
    
    // Auto-remover después de 5 segundos
    setTimeout(() => elemento.remove(), 5000);
}

export { ApiError, clasificarError, mostrarErrorUI };
```

#### **Uso:**

```javascript
try {
    const datos = await fetch("/api/datos");
} catch (error) {
    mostrarErrorUI(error);
}
```

***

### 11.3. Separar lógica de datos de renderizado

Usa la arquitectura **Presentación-Lógica-Datos (PLD)**:

```javascript
// datos.js - Lógica de datos
class RepositorioUsuarios {
    async obtenerTodos() {
        const respuesta = await fetch("/api/usuarios");
        return await respuesta.json();
    }
    
    async obtenerPor(id) {
        const respuesta = await fetch(`/api/usuarios/${id}`);
        return await respuesta.json();
    }
}

// interfaz.js - Lógica de presentación
class VistaUsuarios {
    constructor(repositorio, contenedorId) {
        this.repo = repositorio;
        this.contenedor = document.querySelector(contenedorId);
    }
    
    async mostrarTodos() {
        try {
            const usuarios = await this.repo.obtenerTodos();
            this.renderizar(usuarios);
        } catch (error) {
            this.mostrarError(error);
        }
    }
    
    renderizar(usuarios) {
        this.contenedor.innerHTML = usuarios
            .map(u => this.plantillaUsuario(u))
            .join("");
    }
    
    plantillaUsuario(usuario) {
        return `
            <div class="usuario">
                <h3>${usuario.nombre}</h3>
                <p>${usuario.email}</p>
            </div>
        `;
    }
    
    mostrarError(error) {
        this.contenedor.innerHTML = `<p class="error">${error.message}</p>`;
    }
}

// app.js - Orquestación
const repo = new RepositorioUsuarios();
const vista = new VistaUsuarios(repo, "#usuarios");

vista.mostrarTodos();
```

***

### 11.4. Testing de código asíncrono

Con Jest u otro framework, debes esperar a que terminen las Promises:

```javascript
// usuarios.test.js

describe("RepositorioUsuarios", () => {
    it("debe obtener usuarios", async () => {
        const repo = new RepositorioUsuarios();
        
        // Esperar a que la Promise se resuelva
        const usuarios = await repo.obtenerTodos();
        
        expect(usuarios).toBeDefined();
        expect(usuarios.length).toBeGreaterThan(0);
    });
    
    it("debe manejar errores", async () => {
        const repo = new RepositorioUsuarios();
        
        // Esperar el rechazo
        await expect(repo.obtenerPor(-1)).rejects.toThrow();
    });
    
    it("debe fallar si no hay conexión", async () => {
        // Mock de fetch para simular error de red
        global.fetch = jest.fn(() => 
            Promise.reject(new Error("Network error"))
        );
        
        const repo = new RepositorioUsuarios();
        
        await expect(repo.obtenerTodos()).rejects.toThrow("Network error");
    });
});
```

***

### 11.5. Evitar antipatrones comunes

#### **❌ Antipatrón 1: Múltiples await secuenciales sin necesidad**

```javascript
// MALO: Secuencial innecesario (tarda 6 segundos)
async function malo() {
    const usuario = await fetch("/usuario").then(r => r.json());     // 2s
    const posts = await fetch("/posts").then(r => r.json());         // 2s
    const comentarios = await fetch("/comentarios").then(r => r.json()); // 2s
}

// BUENO: Paralelo (tarda 2 segundos)
async function bueno() {
    const [usuario, posts, comentarios] = await Promise.all([
        fetch("/usuario").then(r => r.json()),
        fetch("/posts").then(r => r.json()),
        fetch("/comentarios").then(r => r.json())
    ]);
}
```

#### **❌ Antipatrón 2: No manejar rechazos**

```javascript
// MALO: El rechazo no está manejado
async function malo() {
    const datos = await fetch("/datos").then(r => r.json());
    console.log(datos);
}

// BUENO: Siempre try/catch o .catch()
async function bueno() {
    try {
        const datos = await fetch("/datos").then(r => r.json());
        console.log(datos);
    } catch (error) {
        console.error("Error:", error);
    }
}
```

#### **❌ Antipatrón 3: Mezclar .then() y async/await**

```javascript
// MALO: Inconsistente
async function malo() {
    const respuesta = await fetch("/datos");
    return respuesta.json().then(d => ({ resultado: d }));
}

// BUENO: Consistente
async function bueno() {
    const respuesta = await fetch("/datos");
    const datos = await respuesta.json();
    return { resultado: datos };
}
```

#### **❌ Antipatrón 4: No limpiar recursos**

```javascript
// MALO: Controller nunca se usa
document.querySelector("#buscar").addEventListener("input", async (e) => {
    const respuesta = await fetch(`/api/buscar?q=${e.target.value}`);
    console.log(await respuesta.json());
});

// BUENO: Cancelar búsquedas previas
let controller = null;

document.querySelector("#buscar").addEventListener("input", async (e) => {
    if (controller) controller.abort();
    
    controller = new AbortController();
    const respuesta = await fetch(`/api/buscar?q=${e.target.value}`, {
        signal: controller.signal
    });
    console.log(await respuesta.json());
});
```

***

### Resumen del Capítulo

El código profesional requiere **centralización, consistencia y claridad**. Usa módulos API, manejo uniforme de errores, separación de responsabilidades y siempre prueba tu código asincrónico.

#### **💡 Conceptos Clave:**

* **Módulos API**: Centralizar llamadas
* **Manejo consistente**: Patrones predecibles
* **Separación**: Datos, lógica, presentación
* **Testing**: Esperar a Promises, mocksear fetch
* **Antipatrones**: Qué evitar
* **Limpiar recursos**: AbortController, timeouts
* **Documentación**: Explicar comportamiento asincrónico
* **Logging**: Rastrear operaciones

#### **🤔 Preguntas de Reflexión:**

1. ¿Por qué centralizar llamadas API?
2. ¿Cómo estructurarías el manejo de errores?
3. ¿Cuál es la ventaja de separar datos de presentación?
4. ¿Cómo testearías una función asincrónica?
5. ¿Cuáles son los antipatrones más comunes?
6. Crea un módulo API reutilizable y testeable.

***
