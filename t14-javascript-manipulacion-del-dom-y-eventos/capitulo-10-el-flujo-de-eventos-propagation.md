# Capítulo 10: El Flujo de Eventos (Propagation)

Entender cómo se propagan los eventos es crucial para dominar JavaScript en el navegador. Este capítulo cubre uno de los conceptos más importantes: el bubbling y la delegación de eventos.

### 10.1. Las 3 fases: Capturing, Target, Bubbling

Cuando ocurre un evento, el navegador lo procesa en **tres fases**:

1. **Capturing (Fase de Captura)**: El evento baja desde `window` hasta el elemento objetivo
2. **Target (Fase de Objetivo)**: El evento llega al elemento que disparó la acción
3. **Bubbling (Fase de Burbujeo)**: El evento sube desde el elemento objetivo hacia `window`

Visualización:

```
window (Capturing) → document → body → div (Target) → body → document → window (Bubbling)
         ↓
    Desciende               ↓              Asciende
                      Se ejecuta el
                      evento aquí
```

***

### 10.2. Entendiendo el Bubbling (Burbujeo)

**Bubbling** significa que un evento en un elemento "sube" hacia sus ancestros. Si registras un listener en un elemento padre, se ejecutará incluso si el evento ocurrió en un hijo.

```html
<div class="padre">
    <button class="hijo">Haz clic</button>
</div>
```

```javascript
const padre = document.querySelector('.padre');
const hijo = document.querySelector('.hijo');

// Listener en el hijo
hijo.addEventListener('click', (evento) => {
    console.log('1. Listener del hijo se ejecutó');
});

// Listener en el padre
padre.addEventListener('click', (evento) => {
    console.log('2. Listener del padre se ejecutó');
});

// Al hacer clic en el botón:
// Output:
// 1. Listener del hijo se ejecutó
// 2. Listener del padre se ejecutó (¡por bubbling!)
```

{% hint style="warning" %}
**Importante**: No todos los eventos hacen bubbling. Por ejemplo, `focus` NO hace bubbling, pero `click` SÍ.
{% endhint %}

***

### 10.3. `stopPropagation()` y `stopImmediatePropagation()`

#### **`stopPropagation()`**

Detiene la propagación hacia arriba (no llega a los ancestros).

```javascript
const boton = document.querySelector('button');
const contenedor = document.querySelector('.contenedor');

boton.addEventListener('click', (evento) => {
    evento.stopPropagation(); // Evita que llegue al contenedor
    console.log("Clic en botón");
});

contenedor.addEventListener('click', (evento) => {
    console.log("Clic en contenedor");
});

// Al hacer clic en el botón:
// Output: "Clic en botón"
// NO se ejecuta el listener del contenedor
```

#### **`stopImmediatePropagation()`**

Detiene la propagación Y evita que se ejecuten otros listeners en el **mismo elemento**.

```javascript
boton.addEventListener('click', (evento) => {
    evento.stopImmediatePropagation();
    console.log("Listener 1");
});

boton.addEventListener('click', (evento) => {
    console.log("Listener 2");
});

// Al hacer clic:
// Output: "Listener 1"
// Listener 2 NO se ejecuta
```

***

### 10.4. Event Delegation: El patrón de oro

**Event Delegation** significa registrar un listener en un elemento padre que captura eventos de muchos elementos hijo. Esto es **extremadamente eficiente** para listas dinámicas.

#### **Problema sin delegación (ineficiente):**

```html
<ul id="lista">
    <li>Item 1</li>
    <li>Item 2</li>
    <li>Item 3</li>
</ul>
```

```javascript
// ❌ Ineficiente: Un listener por cada item
const items = document.querySelectorAll('li');
items.forEach(item => {
    item.addEventListener('click', () => {
        console.log(item.textContent);
    });
});

// Si añades 1000 items más, necesitas 1000 listeners más
```

#### **Solución con delegación (eficiente):**

```javascript
// ✓ Eficiente: Un listener en el padre
const lista = document.querySelector('#lista');

lista.addEventListener('click', (evento) => {
    // evento.target es el elemento que fue clicado
    if (evento.target.tagName === 'LI') {
        console.log(evento.target.textContent);
    }
});

// Funciona automáticamente incluso para items añadidos después
```

#### **Patrón mejorado con `closest()`:**

```javascript
lista.addEventListener('click', (evento) => {
    const itemClicado = evento.target.closest('li');
    if (itemClicado) {
        console.log(itemClicado.textContent);
    }
});
```

***

### 10.5. Casos prácticos de delegación

#### **Caso 1: Tabla con botones dinámicos**

```html
<table id="usuarios">
    <tr>
        <td>Juan</td>
        <td><button class="eliminar">X</button></td>
    </tr>
    <tr>
        <td>María</td>
        <td><button class="eliminar">X</button></td>
    </tr>
</table>
```

```javascript
const tabla = document.querySelector('#usuarios');

tabla.addEventListener('click', (evento) => {
    if (evento.target.classList.contains('eliminar')) {
        const fila = evento.target.closest('tr');
        console.log(`Eliminar usuario: ${fila.textContent}`);
        fila.remove();
    }
});
```

#### **Caso 2: Carrito de compras**

```html
<div id="carrito">
    <div class="producto">
        <span>Laptop</span>
        <button class="aumentar">+</button>
        <button class="disminuir">-</button>
        <button class="eliminar">Quitar</button>
    </div>
    <!-- Más productos dinámicos -->
</div>
```

```javascript
const carrito = document.querySelector('#carrito');

carrito.addEventListener('click', (evento) => {
    const boton = evento.target;
    const producto = boton.closest('.producto');
    
    if (boton.classList.contains('aumentar')) {
        console.log("Aumentar cantidad");
    } else if (boton.classList.contains('disminuir')) {
        console.log("Disminuir cantidad");
    } else if (boton.classList.contains('eliminar')) {
        producto.remove();
    }
});
```

***

### 10.6. Captura (Capturing Phase) - Uso avanzado

Por defecto, los listeners se registran en la **fase de bubbling**. Para registrarse en la fase de captura, usa el tercer parámetro:

```javascript
elemento.addEventListener('click', callback, true); // Captura
elemento.addEventListener('click', callback, false); // Bubbling (por defecto)
```

Esto es raro que se necesite, pero en casos muy específicos de frameworks es útil.

***

### Resumen del Capítulo

El bubbling es lo que permite la delegación de eventos, una técnica fundamental para aplicaciones eficientes. En lugar de registrar miles de listeners, registra uno en el padre y usa `evento.target` para identificar quién disparó el evento. Esta es la base de los frameworks modernos como React.

#### **💡 Conceptos Clave:**

* **Captura, Target, Bubbling**: Las tres fases de un evento
* **Bubbling**: El evento "sube" hacia los ancestros
* **stopPropagation()**: Evita que el evento suba
* **stopImmediatePropagation()**: Evita propagación y otros listeners
* **Event Delegation**: Usar un listener en el padre para muchos hijos
* **evento.target**: El elemento que disparó el evento
* **closest()**: Subir hasta encontrar un selector (ideal con delegación)
* **Eficiencia**: Delegación es mucho más rápida que muchos listeners

#### **🤔 Preguntas de Reflexión:**

1. ¿Por qué es importante entender el bubbling?
2. ¿Cuál es la diferencia entre `stopPropagation()` y `stopImmediatePropagation()`?
3. ¿Cuándo usarías event delegation?
4. ¿Cómo usarías `evento.target` para identificar el elemento clicado?
5. ¿Por qué la delegación es más eficiente que registrar listeners individuales?
6. Crea una lista donde cada item puede ser clicado para cambiar de color, usando delegación.

***
