# Capítulo 9: Integración con el DOM

Ahora que sabes trabajar con APIs asincrónicas (Tema 15), es hora de **integrarlas con la manipulación del DOM** (Tema 14). Este capítulo cubre el patrón completo: Fetch → Procesar → Renderizar.

### 9.1. Patrón: Fetch → Procesar → Renderizar

Este es el ciclo típico en aplicaciones web modernas:

1. **Fetch**: Obtener datos de una API
2. **Procesar**: Transformar/validar los datos
3. **Renderizar**: Mostrar en el DOM

```javascript
// HTML
// <div id="app">
//   <button id="cargar">Cargar datos</button>
//   <div id="contenido"></div>
// </div>

async function cargarYMostrar() {
    try {
        // 1. FETCH: Obtener datos
        const respuesta = await fetch("/api/usuarios");
        
        if (!respuesta.ok) throw new Error(`HTTP ${respuesta.status}`);
        
        const usuarios = await respuesta.json();
        
        // 2. PROCESAR: Transformar si es necesario
        const usuariosFormateados = usuarios.map(u => ({
            ...u,
            nombreCompleto: `${u.nombre} ${u.apellido}`
        }));
        
        // 3. RENDERIZAR: Mostrar en el DOM
        const contenido = document.querySelector("#contenido");
        contenido.innerHTML = usuariosFormateados
            .map(u => `<div class="usuario"><h3>${u.nombreCompleto}</h3></div>`)
            .join("");
        
    } catch (error) {
        console.error("Error:", error);
        document.querySelector("#contenido").innerHTML = 
            `<p class="error">Error cargando datos: ${error.message}</p>`;
    }
}

// Llamar al hacer clic
document.querySelector("#cargar").addEventListener("click", cargarYMostrar);
```

***

### 9.2. Indicadores de carga (Loading spinners)

Es importante **mostrar feedback visual** mientras se cargan los datos:

```html
<div id="app">
    <button id="cargar">Cargar datos</button>
    <div id="contenido"></div>
    <div id="spinner" class="spinner" style="display: none;">
        Cargando...
    </div>
</div>
```

```javascript
async function cargarDatos() {
    const spinner = document.querySelector("#spinner");
    const contenido = document.querySelector("#contenido");
    
    try {
        // Mostrar spinner
        spinner.style.display = "block";
        contenido.innerHTML = "";
        
        const respuesta = await fetch("/api/usuarios");
        if (!respuesta.ok) throw new Error(`HTTP ${respuesta.status}`);
        
        const usuarios = await respuesta.json();
        
        // Renderizar
        contenido.innerHTML = usuarios
            .map(u => `<div>${u.nombre}</div>`)
            .join("");
        
    } catch (error) {
        contenido.innerHTML = `<p class="error">${error.message}</p>`;
        
    } finally {
        // Siempre ocultar spinner (éxito o error)
        spinner.style.display = "none";
    }
}
```

CSS para el spinner:

```css
.spinner {
    text-align: center;
    font-size: 18px;
    color: #666;
}

.spinner::after {
    content: "...";
    animation: dots 1.5s steps(4, end) infinite;
}

@keyframes dots {
    0%, 20% { content: "."; }
    40% { content: ".."; }
    60% { content: "..."; }
    80%, 100% { content: ""; }
}
```

***

### 9.3. Manejo de errores en la UI

Mostrar errores de forma clara al usuario:

```javascript
async function cargarDatos() {
    const contenido = document.querySelector("#contenido");
    
    try {
        const respuesta = await fetch("/api/datos");
        
        if (!respuesta.ok) {
            // Errores HTTP específicos
            if (respuesta.status === 404) {
                throw new Error("Datos no encontrados");
            } else if (respuesta.status === 500) {
                throw new Error("Error del servidor. Intenta más tarde.");
            } else {
                throw new Error(`Error ${respuesta.status}`);
            }
        }
        
        const datos = await respuesta.json();
        contenido.innerHTML = renderizar(datos);
        
    } catch (error) {
        // Mostrar error formateado
        contenido.innerHTML = `
            <div class="error-box">
                <h3>❌ Error</h3>
                <p>${error.message}</p>
                <button onclick="location.reload()">Reintentar</button>
            </div>
        `;
    }
}
```

CSS para errores:

```css
.error-box {
    border: 2px solid #f44;
    background: #fee;
    padding: 20px;
    border-radius: 8px;
    color: #c00;
}

.error-box button {
    background: #f44;
    color: white;
    border: none;
    padding: 10px 20px;
    border-radius: 4px;
    cursor: pointer;
    margin-top: 10px;
}
```

***

### 9.4. Actualizar la UI en tiempo real

A veces quieres **actualizar solo partes** del DOM sin recargar todo:

```javascript
async function actualizarEstado(usuarioId) {
    try {
        const respuesta = await fetch(`/api/usuarios/${usuarioId}/estado`, {
            method: "PATCH",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify({ estado: "activo" })
        });
        
        if (!respuesta.ok) throw new Error("Error al actualizar");
        
        const usuarioActualizado = await respuesta.json();
        
        // Actualizar solo el elemento en el DOM
        const elemento = document.querySelector(`[data-usuario-id="${usuarioId}"]`);
        elemento.classList.remove("inactivo");
        elemento.classList.add("activo");
        elemento.querySelector(".estado").textContent = usuarioActualizado.estado;
        
        // Mostrar notificación de éxito
        mostrarNotificacion("Usuario actualizado", "success");
        
    } catch (error) {
        mostrarNotificacion(`Error: ${error.message}`, "error");
    }
}

function mostrarNotificacion(mensaje, tipo) {
    const notif = document.createElement("div");
    notif.className = `notificacion ${tipo}`;
    notif.textContent = mensaje;
    document.body.appendChild(notif);
    
    // Desaparecer después de 3 segundos
    setTimeout(() => notif.remove(), 3000);
}
```

CSS para notificaciones:

```css
.notificacion {
    position: fixed;
    top: 20px;
    right: 20px;
    padding: 15px 20px;
    border-radius: 4px;
    z-index: 1000;
    animation: slideIn 0.3s ease-out;
}

.notificacion.success {
    background: #4f4;
    color: white;
}

.notificacion.error {
    background: #f44;
    color: white;
}

@keyframes slideIn {
    from { transform: translateX(400px); }
    to { transform: translateX(0); }
}
```

***

### 9.5. Patrón práctico: Lista con CRUD

Combinar todo para una lista funcional:

```html
<div id="app">
    <input id="nombre" placeholder="Nombre">
    <button id="agregar">Agregar</button>
    <ul id="lista"></ul>
    <div id="spinner" style="display: none;">Cargando...</div>
</div>
```

```javascript
const API = "/api/tareas";

// Cargar lista inicial
async function cargarTareas() {
    mostrarSpinner(true);
    try {
        const respuesta = await fetch(API);
        const tareas = await respuesta.json();
        renderizarTareas(tareas);
    } catch (error) {
        mostrarError(error);
    } finally {
        mostrarSpinner(false);
    }
}

// Agregar tarea
document.querySelector("#agregar").addEventListener("click", async () => {
    const nombre = document.querySelector("#nombre").value;
    
    if (!nombre.trim()) return alert("Escribe una tarea");
    
    try {
        const respuesta = await fetch(API, {
            method: "POST",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify({ nombre })
        });
        
        const tarea = await respuesta.json();
        agregarALista(tarea);
        document.querySelector("#nombre").value = "";
        
    } catch (error) {
        mostrarError(error);
    }
});

// Delegación de eventos para eliminar
document.querySelector("#lista").addEventListener("click", async (e) => {
    if (e.target.classList.contains("eliminar")) {
        const tareaId = e.target.dataset.id;
        
        try {
            await fetch(`${API}/${tareaId}`, { method: "DELETE" });
            e.target.closest("li").remove();
        } catch (error) {
            mostrarError(error);
        }
    }
});

function renderizarTareas(tareas) {
    const lista = document.querySelector("#lista");
    lista.innerHTML = tareas
        .map(t => `
            <li data-id="${t.id}">
                ${t.nombre}
                <button class="eliminar" data-id="${t.id}">X</button>
            </li>
        `)
        .join("");
}

function agregarALista(tarea) {
    const lista = document.querySelector("#lista");
    const li = document.createElement("li");
    li.dataset.id = tarea.id;
    li.innerHTML = `
        ${tarea.nombre}
        <button class="eliminar" data-id="${tarea.id}">X</button>
    `;
    lista.appendChild(li);
}

function mostrarSpinner(mostrar) {
    document.querySelector("#spinner").style.display = mostrar ? "block" : "none";
}

function mostrarError(error) {
    alert(`Error: ${error.message}`);
}

// Iniciar
cargarTareas();
```

***

### Resumen del Capítulo

Integrar Fetch con el DOM es donde la programación asincrónica cobra sentido. El patrón Fetch → Procesar → Renderizar es fundamental. Siempre proporciona feedback visual (spinners, errores) para una buena experiencia de usuario.

#### **💡 Conceptos Clave:**

* **Patrón F→P→R**: Fetch, Procesar, Renderizar
* **Spinners**: Indicadores de carga
* **Manejo de errores UI**: Mostrar errores de forma clara
* **Actualización parcial**: Modificar solo lo necesario
* **Delegación de eventos**: Manejar dinámicamente elementos nuevos
* **Notificaciones**: Feedback de éxito/error
* **CRUD en DOM**: Agregar, leer, actualizar, eliminar
* **finally**: Limpiar spinners siempre

#### **🤔 Preguntas de Reflexión:**

1. ¿Por qué es importante mostrar un spinner durante la carga?
2. ¿Cómo actualizarías solo un elemento en  el DOM sin recargar todo?
3. ¿Cuándo usarías delegación de eventos con datos remotos?
4. ¿Cómo mostrarías un mensaje de error útil al usuario?
5. ¿Qué diferencia hay entre `map()` y `forEach()` al renderizar?
6. Crea una lista CRUD completa con una API.

***
