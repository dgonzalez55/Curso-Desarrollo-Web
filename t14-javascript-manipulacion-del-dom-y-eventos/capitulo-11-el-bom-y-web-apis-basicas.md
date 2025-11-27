# Capítulo 11: El BOM y Web APIs Básicas

Mientras que el DOM (Document Object Model) se enfoca en manipular la página HTML, el **BOM (Browser Object Model)** proporciona acceso a la ventana del navegador y funciones globales. Este capítulo cubre las APIs más útiles.

### 11.1. El objeto `window` y dimensiones del viewport

El objeto `window` es el objeto global en el navegador. Todo lo que ejecutas está dentro de `window`.

#### **Propiedades de dimensión:**

```javascript
// Tamaño de la ventana (viewport)
console.log(window.innerWidth);   // Ancho usable (sin scrollbar)
console.log(window.innerHeight);  // Alto usable

// Tamaño total del documento (puede ser mayor si hay scroll)
console.log(document.documentElement.scrollWidth);
console.log(document.documentElement.scrollHeight);

// Posición del scroll
console.log(window.scrollX);      // Desplazamiento horizontal
console.log(window.scrollY);      // Desplazamiento vertical
```

#### **Evento de redimensionamiento:**

```javascript
window.addEventListener('resize', () => {
    console.log(`Nueva dimensión: ${window.innerWidth}x${window.innerHeight}`);
    // Útil para layouts responsive
});
```

***

### 11.2. `localStorage` y `sessionStorage` (Repaso práctico)

Estas APIs permiten guardar datos en el navegador de forma persistente.

#### **`localStorage`: Persiste incluso después de cerrar el navegador**

```javascript
// Guardar
localStorage.setItem('usuario', 'Juan');
localStorage.setItem('tema', 'oscuro');

// Leer
console.log(localStorage.getItem('usuario'));    // "Juan"

// Verificar existencia
if (localStorage.getItem('tema')) {
    console.log("Tema guardado encontrado");
}

// Eliminar
localStorage.removeItem('tema');

// Limpiar todo
localStorage.clear();

// Iterar
for (let i = 0; i < localStorage.length; i++) {
    const clave = localStorage.key(i);
    console.log(clave, localStorage.getItem(clave));
}
```

#### **`sessionStorage`: Se elimina al cerrar el navegador**

```javascript
// Mismo API que localStorage, pero temporal
sessionStorage.setItem('session_id', '12345');
console.log(sessionStorage.getItem('session_id')); // "12345"
```

#### **Patrón: Guardar objetos complejos**

```javascript
const usuario = { id: 1, nombre: "Juan", email: "juan@example.com" };

// Guardar como JSON
localStorage.setItem('usuario', JSON.stringify(usuario));

// Recuperar y parsear
const usuarioGuardado = JSON.parse(localStorage.getItem('usuario'));
console.log(usuarioGuardado.nombre); // "Juan"
```

#### **Evento de cambio (útil para sincronización entre pestañas)**

```javascript
window.addEventListener('storage', (evento) => {
    console.log(`${evento.key} cambió a ${evento.newValue}`);
});

// Se dispara en OTRAS pestañas cuando tú cambias storage
// (No en la misma pestaña)
```

***

### 11.3. Timers: `setTimeout`, `setInterval`, `requestAnimationFrame`

#### **`setTimeout`: Ejecutar código después de un tiempo**

```javascript
// Ejecutar una vez después de 2 segundos
const id = setTimeout(() => {
    console.log("Pasaron 2 segundos");
}, 2000);

// Cancelar (antes de que se ejecute)
clearTimeout(id);
```

#### **`setInterval`: Ejecutar código repetidamente**

```javascript
// Ejecutar cada 1 segundo
const id = setInterval(() => {
    console.log("Tick");
}, 1000);

// Cancelar
clearInterval(id);
```

#### **`requestAnimationFrame`: Para animaciones suaves**

```javascript
// Se ejecuta justo antes de que el navegador actualice la pantalla
// Perfecta sincronización con FPS del monitor

let x = 0;

function animar() {
    x += 5;
    elemento.style.left = x + 'px';
    
    if (x < 200) {
        requestAnimationFrame(animar); // Próxima frame
    }
}

requestAnimationFrame(animar);
```

***

### 11.4. Objeto `location`: Trabajar con URLs

#### **Propiedades:**

```javascript
// Dirección completa
console.log(location.href);        // "https://example.com:8080/page?id=1#section"

// Partes de la URL
console.log(location.protocol);    // "https:"
console.log(location.host);        // "example.com:8080"
console.log(location.hostname);    // "example.com"
console.log(location.port);        // "8080"
console.log(location.pathname);    // "/page"
console.log(location.search);      // "?id=1"
console.log(location.hash);        // "#section"
```

#### **Métodos:**

```javascript
// Navegar a una URL
location.href = "https://google.com";     // Recargar página
location.assign("https://google.com");    // Lo mismo

// Reemplazar el historial (no hay botón atrás)
location.replace("https://google.com");

// Recargar página
location.reload();

// Recargar sin cache
location.reload(true);
```

#### **`URLSearchParams`: Parsear query strings**

```javascript
const params = new URLSearchParams(location.search);
console.log(params.get('id'));     // "1" (del ?id=1)
console.log(params.getAll('tag')); // Array de valores si hay múltiples
```

***

### 11.5. Objeto `history`: Navegación del historial

```javascript
// Botón atrás
history.back();
history.go(-1); // Lo mismo

// Botón adelante
history.forward();
history.go(1);

// Ir a una página específica
history.go(0);  // Recargar
history.go(-2); // Dos páginas atrás
```

***

### 11.6. Patrón práctico: Tema persistente

Aplicación que guarda la preferencia del usuario:

```javascript
// HTML: <body> <button id="toggle-tema">Toggle Dark Mode</button> </body>

const html = document.documentElement;
const boton = document.querySelector('#toggle-tema');

// Cargar preferencia guardada al iniciar
const temaPrefierido = localStorage.getItem('tema') || 'claro';
html.classList.add(temaPrefierido);

// Cambiar tema
boton.addEventListener('click', () => {
    const temActual = html.classList.contains('oscuro') ? 'oscuro' : 'claro';
    const temaNuevo = temActual === 'oscuro' ? 'claro' : 'oscuro';
    
    html.classList.remove(temActual);
    html.classList.add(temaNuevo);
    
    // Guardar preferencia
    localStorage.setItem('tema', temaNuevo);
});
```

***

### Resumen del Capítulo

El BOM proporciona acceso a funcionalidades del navegador más allá del DOM. localStorage es fundamental para persistencia sin servidor, timers para ejecución retardada/repetida, y location/history para navegación. Estas APIs son la base para aplicaciones web modernas.

#### **💡 Conceptos Clave:**

* **window**: Objeto global del navegador
* **innerWidth/innerHeight**: Dimensiones del viewport
* **localStorage/sessionStorage**: Almacenamiento persistente
* **setTimeout/setInterval**: Ejecución retardada/repetida
* **requestAnimationFrame**: Animaciones sincronizadas con FPS
* **location**: Objeto de la URL actual
* **URLSearchParams**: Parsear query strings
* **history**: Navegación del historial

#### **🤔 Preguntas de Reflexión:**

1. ¿Cuál es la diferencia entre localStorage y sessionStorage?
2. ¿Cómo guardarías un objeto complejo en localStorage?
3. ¿Cuándo usarías requestAnimationFrame en lugar de setInterval?
4. ¿Cómo obtendrías el valor de un parámetro en la URL?
5. ¿Cuál es la diferencia entre location.href y location.replace()?
6. Crea una aplicación que guarde el tema del usuario y lo cargue al iniciar.

***
