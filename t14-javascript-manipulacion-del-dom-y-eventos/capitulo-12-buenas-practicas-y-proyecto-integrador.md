# Capítulo 12: Buenas Prácticas y Proyecto Integrador

Este capítulo final consolida lo aprendido y establece patrones profesionales para construir aplicaciones web escalables y mantenibles.

### 12.1. Minimizar Reflow y Repaint (Rendimiento)

El navegador necesita actualizar la pantalla cuando el JavaScript modifica el DOM. Estas operaciones son costosas.

**Reflow**: Recalcular layout (más caro)&#x20;

**Repaint**: Actualizar píxeles (menos caro que reflow)

#### **Evitar reflows innecesarios:**

```javascript
// ❌ MALO: 5 reflows
elemento.style.width = '100px';     // Reflow 1
elemento.style.height = '100px';    // Reflow 2
elemento.style.margin = '10px';     // Reflow 3

// ✓ MEJOR: 1 reflow usando clase
elemento.classList.add('tamaño-grande');

// ✓ MEJOR: Usar cssText
elemento.style.cssText = 'width: 100px; height: 100px; margin: 10px;';
```

#### **Lectura después de escritura:**

```javascript
// ❌ MALO: Fuerza reflow
elemento.style.width = '100px';
console.log(elemento.offsetWidth); // Reflow forzado
elemento.style.height = '100px';
console.log(elemento.offsetHeight); // Reflow forzado

// ✓ MEJOR: Leer luego escribir
console.log(elemento.offsetWidth);  // Una lectura
console.log(elemento.offsetHeight); // Una lectura
elemento.style.width = '100px';     // Una escritura
elemento.style.height = '100px';    // Una escritura
```

#### **DocumentFragment para inserciones masivas:**

```javascript
// ❌ MALO: 1000 reflows
for (let i = 0; i < 1000; i++) {
    const item = document.createElement('li');
    lista.appendChild(item); // Reflow en cada iteración
}

// ✓ MEJOR: 1 reflow
const fragment = document.createDocumentFragment();
for (let i = 0; i < 1000; i++) {
    const item = document.createElement('li');
    fragment.appendChild(item); // No actualiza DOM
}
lista.appendChild(fragment); // Reflow una sola vez
```

***

### 12.2. Separación de responsabilidades (HTML/CSS/JS)

Mantén clara la separación: HTML (estructura), CSS (estilos), JavaScript (lógica).

```html
<!-- ❌ EVITAR: Lógica en HTML -->
<button onclick="alert('Hola')">Haz clic</button>

<!-- ✓ CORRECTO: Estructura limpia -->
<button id="mi-boton">Haz clic</button>
```

```css
/* CSS: Define estados visuales */
.activo {
    background: blue;
    color: white;
}

.inactivo {
    background: gray;
    color: black;
}
```

```javascript
// JavaScript: Controla lógica
const boton = document.querySelector('#mi-boton');

boton.addEventListener('click', () => {
    boton.classList.toggle('activo');
});
```

***

### 12.3. Gestión de memoria: Limpiar eventos

Cuando eliminas elementos del DOM, debes también eliminar sus event listeners para evitar memory leaks.

```javascript
// ❌ Memory leak
function crearElemento() {
    const elem = document.createElement('div');
    
    elem.addEventListener('click', () => {
        console.log("Clickeado");
    });
    
    document.body.appendChild(elem);
}

for (let i = 0; i < 1000; i++) {
    crearElemento();
}

// Aunque elimines los elementos, los listeners quedan en memoria

// ✓ CORRECTO: Limpiar listeners
function crearElemento() {
    const elem = document.createElement('div');
    
    const handler = () => console.log("Clickeado");
    elem.addEventListener('click', handler);
    
    // Guardamos método de limpieza
    elem.cleanup = () => {
        elem.removeEventListener('click', handler);
    };
    
    document.body.appendChild(elem);
    
    return elem;
}

// Al eliminar
elemento.cleanup();
elemento.remove();
```

***

### 12.4. Accesibilidad (A11Y) desde JavaScript

Accesibilidad es responsabilidad de HTML + CSS + JavaScript.

```javascript
// ❌ INACCESIBLE: Usando div como botón
const div = document.createElement('div');
div.textContent = "Comprar";
div.addEventListener('click', () => { /* ... */ });

// ✓ ACCESIBLE: Usar elementos semánticos
const boton = document.createElement('button');
boton.textContent = "Comprar";
boton.addEventListener('click', () => { /* ... */ });

// ✓ MEJOR: Atributos ARIA
const hamburguesa = document.createElement('button');
hamburguesa.setAttribute('aria-label', 'Abrir menú');
hamburguesa.setAttribute('aria-expanded', 'false');

hamburguesa.addEventListener('click', () => {
    const expandido = hamburguesa.getAttribute('aria-expanded') === 'true';
    hamburguesa.setAttribute('aria-expanded', !expandido);
});
```

***

### 12.5. Estructura de una aplicación SPA vainilla

**SPA** = Single Page Application. Una página que maneja el contenido dinámicamente.

```javascript
// app.js - Estructura básica

class App {
    constructor() {
        this.currentPage = 'home';
        this.init();
    }
    
    init() {
        this.registerEventListeners();
        this.render();
    }
    
    registerEventListeners() {
        // Delegación de eventos
        document.addEventListener('click', (evento) => {
            if (evento.target.classList.contains('nav-link')) {
                this.currentPage = evento.target.dataset.page;
                this.render();
            }
        });
    }
    
    render() {
        const contenedor = document.querySelector('#app');
        
        switch (this.currentPage) {
            case 'home':
                contenedor.innerHTML = this.renderHome();
                break;
            case 'about':
                contenedor.innerHTML = this.renderAbout();
                break;
            default:
                contenedor.innerHTML = this.render404();
        }
    }
    
    renderHome() {
        return `<h1>Bienvenido</h1>`;
    }
    
    renderAbout() {
        return `<h1>Acerca de</h1>`;
    }
    
    render404() {
        return `<h1>404 - No encontrado</h1>`;
    }
}

// Iniciar aplicación
const app = new App();
```

HTML:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Mi SPA</title>
</head>
<body>
    <nav>
        <a href="#" class="nav-link" data-page="home">Home</a>
        <a href="#" class="nav-link" data-page="about">About</a>
    </nav>
    
    <div id="app"></div>
    
    <script src="app.js"></script>
</body>
</html>
```

***

### 12.6. Proyecto integrador: Todo App

Aplicación de tareas con almacenamiento persistente:

```javascript
class TodoApp {
    constructor() {
        this.todos = [];
        this.loadFromStorage();
        this.init();
    }
    
    init() {
        this.cacheDOM();
        this.registerEvents();
        this.render();
    }
    
    cacheDOM() {
        this.input = document.querySelector('#todo-input');
        this.addBtn = document.querySelector('#add-btn');
        this.list = document.querySelector('#todo-list');
    }
    
    registerEvents() {
        this.addBtn.addEventListener('click', () => this.addTodo());
        this.input.addEventListener('keydown', (e) => {
            if (e.key === 'Enter') this.addTodo();
        });
        
        // Delegación
        this.list.addEventListener('click', (e) => {
            if (e.target.classList.contains('delete')) {
                this.deleteTodo(e.target.dataset.id);
            } else if (e.target.classList.contains('toggle')) {
                this.toggleTodo(e.target.dataset.id);
            }
        });
    }
    
    addTodo() {
        const texto = this.input.value.trim();
        if (!texto) return;
        
        const todo = {
            id: Date.now(),
            texto,
            completado: false
        };
        
        this.todos.push(todo);
        this.input.value = '';
        this.saveToStorage();
        this.render();
    }
    
    deleteTodo(id) {
        this.todos = this.todos.filter(t => t.id !== parseInt(id));
        this.saveToStorage();
        this.render();
    }
    
    toggleTodo(id) {
        const todo = this.todos.find(t => t.id === parseInt(id));
        if (todo) {
            todo.completado = !todo.completado;
            this.saveToStorage();
            this.render();
        }
    }
    
    render() {
        this.list.innerHTML = this.todos
            .map(t => `
                <li class="${t.completado ? 'completado' : ''}">
                    <input type="checkbox" class="toggle" 
                           data-id="${t.id}" 
                           ${t.completado ? 'checked' : ''}>
                    <span>${t.texto}</span>
                    <button class="delete" data-id="${t.id}">✕</button>
                </li>
            `)
            .join('');
    }
    
    saveToStorage() {
        localStorage.setItem('todos', JSON.stringify(this.todos));
    }
    
    loadFromStorage() {
        const datos = localStorage.getItem('todos');
        this.todos = datos ? JSON.parse(datos) : [];
    }
}

const app = new TodoApp();
```

***

### Resumen del Capítulo

El desarrollo profesional de aplicaciones web requiere entender rendimiento, accesibilidad y arquitectura. Usa patrones como delegación de eventos, separación de responsabilidades y almacenamiento local para crear aplicaciones escalables y mantenibles.

#### **💡 Conceptos Clave:**

* **Reflow/Repaint**: Optimizar actualizaciones del DOM
* **DocumentFragment**: Inserciones masivas eficientes
* **Separación**: HTML (estructura), CSS (estilos), JS (lógica)
* **Memory leaks**: Limpiar listeners al eliminar elementos
* **Accesibilidad**: ARIA, elementos semánticos
* **SPA**: Single Page Application con enrutamiento dinámico
* **Delegación**: Un listener para muchos elementos
* **localStorage**: Persistencia sin servidor

#### **🤔 Preguntas de Reflexión:**

1. ¿Cómo minimizarías reflows en una operación masiva?
2. ¿Qué es un memory leak y cómo evitarlo?
3. ¿Cuál es la importancia de la accesibilidad en JavaScript?
4. ¿Cómo estructurarías una SPA con enrutamiento?
5. ¿Cómo combinarías delegación de eventos con localStorage?
6. Crea una aplicación completa (notas, favoritos, etc.) con persistencia.
