# Capítulo 7: Introducción a los Eventos

Los eventos son la forma en que JavaScript responde a las acciones del usuario (clics, teclas, movimientos del ratón). Sin eventos, no hay interactividad. Este capítulo introduce el modelo de eventos de JavaScript.

### 7.1. ¿Qué es un evento? Modelo asíncrono básico

Un **evento** es algo que sucede en el navegador o en una página web: el usuario hace clic, teclea, mueve el ratón, etc.

JavaScript es fundamentalmente **asíncrono**: cuando estableces un "listener" de evento, le estás diciendo al navegador: "cuando esto suceda, ejecuta esta función". El navegador espera y ejecuta el código cuando sea necesario.

```javascript
// Pseudocódigo del flujo:
// 1. Página carga
// 2. Código JavaScript se ejecuta (registra listeners)
// 3. JavaScript ESPERA a que suceda algo
// 4. Usuario hace clic
// 5. Se ejecuta el callback del evento
// 6. Continúa el JavaScript
```

***

### 7.2. `addEventListener`: La forma correcta de escuchar

`addEventListener()` es el método moderno y recomendado para registrar listeners de eventos.

**Sintaxis**: `elemento.addEventListener(tipo, callback, opciones)`

```javascript
// HTML: <button id="btn">Haz clic</button>

const boton = document.querySelector('#btn');

// Registrar listener
boton.addEventListener('click', function(evento) {
    console.log("¡El usuario hizo clic!");
});

// Con arrow function (más común)
boton.addEventListener('click', (evento) => {
    console.log("Clic detectado");
});
```

#### **Ventajas de addEventListener:**

* Puedes registrar **múltiples listeners** para el mismo evento
* Fácil de quitar después (`removeEventListener`)
* Soporta opciones avanzadas (captura, una sola vez, etc.)

```javascript
// Múltiples listeners en el mismo elemento
boton.addEventListener('click', () => console.log("Listener 1"));
boton.addEventListener('click', () => console.log("Listener 2"));
// Al hacer clic, se ejecutan ambos
```

***

### 7.3. El objeto `Event`: propiedades comunes

Cuando ocurre un evento, el navegador crea un objeto `Event` que contiene información sobre lo sucedido.

```javascript
boton.addEventListener('click', (evento) => {
    // evento es el objeto Event
    console.log(evento.type);        // "click"
    console.log(evento.target);      // El elemento que disparó el evento
    console.log(evento.currentTarget); // El elemento con el listener
    console.log(evento.timeStamp);   // Cuándo sucedió
});
```

#### **Propiedades importantes:**

* **`event.type`**: El tipo de evento ("click", "keydown", etc.)
* **`event.target`**: El elemento que disparó el evento (donde pasó la acción)
* **`event.currentTarget`**: El elemento que tiene el listener (puede ser diferente si hay bubbling)
* **`event.timeStamp`**: Cuándo sucedió (en milisegundos)
* **`event.preventDefault()`**: Cancela la acción por defecto

***

### 7.4. Eliminar eventos: `removeEventListener`

Si necesitas dejar de escuchar un evento, usa `removeEventListener`. **Importante**: Debes pasar la **misma función** que registraste.

```javascript
// Registrar
function miManejador(evento) {
    console.log("Evento disparado");
}

boton.addEventListener('click', miManejador);

// Eliminar (debe ser la MISMA función)
boton.removeEventListener('click', miManejador);

// ESTO NO FUNCIONARÁ (función anónima diferente)
boton.addEventListener('click', () => console.log("Hola"));
boton.removeEventListener('click', () => console.log("Hola")); // No es la misma
```

#### **Patrón: Guardar referencia a la función**

```javascript
const miManejador = (evento) => {
    console.log("Clicked");
};

// Registrar
boton.addEventListener('click', miManejador);

// Eliminar
boton.removeEventListener('click', miManejador);
```

***

### 7.5. El problema de `this` en los eventos y Arrow Functions

Este es un tema sutil pero importante. El valor de `this` dentro de un listener depende de cómo lo definas.

```javascript
const usuario = {
    nombre: "Juan",
    saludar: function() {
        console.log("Hola, " + this.nombre);
    }
};

// Si pasas el método directamente...
boton.addEventListener('click', usuario.saludar);
// En el listener, `this` es el boton, NO el objeto usuario
// Output: "Hola, undefined"

// Solución 1: Bind
boton.addEventListener('click', usuario.saludar.bind(usuario));
// Output: "Hola, Juan"

// Solución 2: Arrow function envolvente
boton.addEventListener('click', () => usuario.saludar());
// Output: "Hola, Juan"

// Solución 3: Event currentTarget
boton.addEventListener('click', function() {
    console.log(this); // En una función normal, this es el boton
});

// Arrow functions: Heredan `this` del contexto exterior
const clase = {
    nombre: "MiClase",
    registrar: function(boton) {
        boton.addEventListener('click', () => {
            console.log(this.nombre); // "MiClase" (heredado del contexto)
        });
    }
};
```

***

### 7.6. Eventos inline (NO recomendado)

Existe una forma antigua de registrar eventos directamente en HTML. **No la uses** en código profesional:

```html
<!-- ❌ EVITAR -->
<button onclick="alert('Hola')">Clic</button>

<!-- ✓ CORRECTO -->
<button id="btn">Clic</button>
```

```javascript
// Registrar en JavaScript
document.querySelector('#btn').addEventListener('click', () => {
    alert('Hola');
});
```

***

### Resumen del Capítulo

Los eventos son el mecanismo por el cual JavaScript responde a acciones del usuario. `addEventListener()` es la forma moderna y flexible de registrar listeners. Recuerda entender el objeto `Event` y ser consciente de cómo se comporta `this` en los listeners, especialmente cuando trabajas con clases o métodos.

#### **💡 Conceptos Clave:**

* **Evento**: Acción que sucede en el navegador (clic, tecla, movimiento)
* **addEventListener()**: Registrar un listener de forma moderna
* **Objeto Event**: Contiene información sobre lo que sucedió
* **event.target**: El elemento que disparó el evento
* **event.preventDefault()**: Cancela la acción por defecto
* **removeEventListener()**: Dejar de escuchar (mismo callback)
* **`this` en listeners**: Cuidado con el contexto
* **Arrow functions**: Heredan `this` del contexto exterior

#### **🤔 Preguntas de Reflexión:**

1. ¿Cuál es la diferencia entre `event.target` y `event.currentTarget`?
2. ¿Por qué no puedes hacer `removeEventListener` con una función anónima?
3. ¿Cómo se comporta `this` en un listener si usas una arrow function vs una función normal?
4. ¿Qué es el "bubbling" de eventos? (Adelanto para el Cap. 10)
5. ¿Cuándo usarías `preventDefault()` en un evento?
6. Registra dos listeners diferentes en el mismo elemento para el evento 'click'.

***
