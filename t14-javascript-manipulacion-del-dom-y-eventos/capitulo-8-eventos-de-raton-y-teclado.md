# Capítulo 8: Eventos de Ratón y Teclado

Este capítulo cubre los tipos de eventos más comunes: los relacionados con el ratón (mouse) y el teclado. Aprenderás qué evento usar en cada situación.

### 8.1. Eventos de ratón principales

#### **`click`**

Se dispara cuando el usuario **hace clic** (presiona y suelta).

```javascript
const boton = document.querySelector('button');
boton.addEventListener('click', (evento) => {
    console.log("Click detectado");
});
```

#### **`dblclick`**

Se dispara en un **doble clic** (rápido).

```javascript
elemento.addEventListener('dblclick', (evento) => {
    console.log("Doble clic");
});
```

#### **`mousedown` y `mouseup`**

* `mousedown`: Se dispara cuando el usuario **presiona** el botón del ratón
* `mouseup`: Se dispara cuando el usuario **suelta** el botón

```javascript
const area = document.querySelector('#area');

area.addEventListener('mousedown', () => {
    console.log("Ratón presionado");
});

area.addEventListener('mouseup', () => {
    console.log("Ratón soltado");
});
```

#### **`mousemove`**

Se dispara **constantemente** mientras el usuario mueve el ratón sobre el elemento. ¡Usa con cuidado porque se dispara muchas veces!

```javascript
elemento.addEventListener('mousemove', (evento) => {
    console.log(evento.clientX, evento.clientY); // Coordenadas
});
```

***

### 8.2. Movimiento: `mouseenter` vs `mouseover`

#### **`mouseenter`**

Se dispara cuando el ratón **entra** en el área del elemento.

#### **`mouseover`**

Similar a `mouseenter`, pero **sí hace bubbling** (veremos más adelante).

#### **`mouseleave`**

Se dispara cuando el ratón **sale** del elemento.

#### **`mouseout`**

Similar a `mouseleave`, pero **sí hace bubbling**.

```javascript
// Para efectos simples, mouseenter/mouseleave es mejor
const carta = document.querySelector('.card');

carta.addEventListener('mouseenter', () => {
    carta.classList.add('highlight');
});

carta.addEventListener('mouseleave', () => {
    carta.classList.remove('highlight');
});
```

{% hint style="success" %}
**Recomendación**: Usa `mouseenter` y `mouseleave` para la mayoría de casos por su comportamiento más predecible.
{% endhint %}

***

### 8.3. Eventos de teclado

#### **`keydown`**

Se dispara cuando el usuario **presiona** una tecla (se repite si la mantiene presionada).

#### **`keyup`**

Se dispara cuando el usuario **suelta** una tecla.

#### **`keypress`**

{% hint style="danger" %}
**Obsoleto**. No lo uses. Usa `keydown` o `keyup` en su lugar.
{% endhint %}

```javascript
document.addEventListener('keydown', (evento) => {
    console.log(`Tecla presionada: ${evento.key}`);
});

document.addEventListener('keyup', (evento) => {
    console.log(`Tecla soltada: ${evento.key}`);
});
```

***

### 8.4. Propiedades de teclado: `key` vs `code`

Cuando se dispara un evento de teclado, el objeto `Event` contiene dos propiedades relacionadas:

* **`event.key`**: El carácter que el usuario intentó escribir ("a", "A", "Enter", "ArrowUp")
* **`event.code`**: La posición física de la tecla en el teclado ("KeyA", "ShiftRight")

```javascript
document.addEventListener('keydown', (evento) => {
    console.log(evento.key);   // "a" o "A" según Shift
    console.log(evento.code);  // "KeyA" (siempre igual)
});

// Esto es importante para juegos o atajos de teclado:
// - Usa `key` si te importa qué carácter se escribió
// - Usa `code` si te importa qué tecla física se presionó
```

#### **Teclas especiales**

```javascript
document.addEventListener('keydown', (evento) => {
    // Teclas especiales con nombres
    if (evento.key === 'Enter') {
        console.log("Enter presionado");
    }
    if (evento.key === 'Escape') {
        console.log("Escape presionado");
    }
    if (evento.key === 'ArrowUp') {
        console.log("Flecha arriba presionada");
    }
    if (evento.key === ' ') {
        console.log("Espacio presionado");
    }
});
```

***

### 8.5. Modificadores: `ctrlKey`, `shiftKey`, `altKey`

Puedes detectar si se presionaron teclas modificadoras junto con otra tecla.

```javascript
document.addEventListener('keydown', (evento) => {
    if (evento.ctrlKey && evento.key === 's') {
        evento.preventDefault(); // Evitar el guardado nativo
        console.log("Atajo Ctrl+S detectado");
    }
});

// Más modificadores
if (evento.shiftKey) console.log("Shift presionado");
if (evento.altKey) console.log("Alt presionado");
if (evento.metaKey) console.log("Meta (Cmd en Mac, Win en PC) presionado");
```

***

### 8.6. Patrón práctico: Detectar Enter en un input

Un caso muy común es ejecutar código cuando el usuario presiona Enter en un campo de texto.

```html
<input type="text" id="buscar" placeholder="Escribe...">
```

```javascript
const input = document.querySelector('#buscar');

input.addEventListener('keydown', (evento) => {
    if (evento.key === 'Enter') {
        console.log("Usuario presionó Enter");
        console.log("Valor:", input.value);
        // Hacer búsqueda, enviar formulario, etc.
    }
});
```

***

### 8.7. Propiedades adicionales de eventos de ratón

El objeto `Event` de ratón contiene información sobre la posición:

```javascript
elemento.addEventListener('click', (evento) => {
    console.log(evento.clientX);    // Posición X relativa a ventana
    console.log(evento.clientY);    // Posición Y relativa a ventana
    console.log(evento.pageX);      // Posición X relativa a página (con scroll)
    console.log(evento.pageY);      // Posición Y relativa a página
    console.log(evento.screenX);    // Posición X relativa a pantalla del PC
    console.log(evento.screenY);    // Posición Y relativa a pantalla
});
```

***

### 8.8. Patrón práctico: Detectar botón del ratón

```javascript
elemento.addEventListener('mousedown', (evento) => {
    if (evento.button === 0) {
        console.log("Botón izquierdo");
    } else if (evento.button === 1) {
        console.log("Rueda central");
    } else if (evento.button === 2) {
        console.log("Botón derecho");
    }
});
```

***

### Resumen del Capítulo

Los eventos de ratón y teclado son los más comunes en aplicaciones web. Aprende a usar los eventos correctos para cada situación: `click` para clics simples, `keydown`/`keyup` para teclado, y `mouseenter`/`mouseleave` para hover effects. Recuerda diferenciar entre `key` (carácter) y `code` (posición física) en eventos de teclado.

#### **💡 Conceptos Clave:**

* **click**: Clic simple
* **dblclick**: Doble clic
* **mousedown/mouseup**: Presionar y soltar ratón
* **mousemove**: Movimiento constantemente
* **mouseenter/mouseleave**: Entrar y salir del área
* **keydown/keyup**: Presionar y soltar tecla
* **event.key**: Carácter del teclado
* **event.code**: Posición física de la tecla
* **Modificadores**: ctrlKey, shiftKey, altKey, metaKey
* **event.clientX/clientY**: Coordenadas del ratón

#### **🤔 Preguntas de Reflexión:**

1. ¿Cuál es la diferencia entre `mouseenter` y `mouseover`?
2. ¿Cuándo usarías `keydown` vs `keyup`?
3. ¿Cuál es la diferencia entre `event.key` y `event.code`?
4. ¿Cómo detectarías el atajo de teclado Ctrl+Z?
5. ¿Cómo obtendrías la posición exacta del ratón en un evento `mousemove`?
6. Crea un input que se enfoque al presionar la tecla '/'

***
