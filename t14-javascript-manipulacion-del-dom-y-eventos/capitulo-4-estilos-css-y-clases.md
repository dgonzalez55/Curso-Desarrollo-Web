# Capítulo 4: Estilos CSS y Clases

Manipular la apariencia de los elementos es una de las tareas más comunes en JavaScript frontend. Hay dos formas principales: modificar estilos directamente (inline) o gestionar clases CSS. Existe una forma profesional y una forma "rápida"; aquí aprenderás ambas.

### 4.1. La propiedad `style`: Estilos en línea

Cada elemento DOM tiene una propiedad `.style` que es un objeto. Puedes usarla para añadir estilos **inline** (en el atributo `style=""` del HTML).

{% hint style="info" %}
**Regla de oro**: Las propiedades CSS que tienen guiones (`background-color`) se escriben en **camelCase** en JavaScript (`backgroundColor`).
{% endhint %}

```javascript
const caja = document.querySelector('.box');

// Escribir estilos
caja.style.backgroundColor = 'red';
caja.style.fontSize = '20px';
caja.style.marginTop = '10px';
caja.style.borderRadius = '8px';

// Leer estilos inline
console.log(caja.style.backgroundColor); // "red"

// Borrar un estilo inline (vuelve al valor de la hoja de estilos)
caja.style.display = '';
```

#### **Desventajas de los estilos inline:**

* Alta especificidad (sobrescriben casi todo tu CSS)
* Ensucian el HTML
* Difíciles de mantener

{% hint style="warning" %}
**Úsalos solo para valores calculados dinámicamente**: coordenadas de una animación, colores elegidos por el usuario, dimensiones calculadas.
{% endhint %}

***

### 4.2. `getComputedStyle()`: Leer estilos finales

La propiedad `.style` **solo lee los estilos inline**. No puede leer los estilos definidos en tu hoja `.css`.

Para saber el estilo _real_ y final de un elemento (después de aplicar cascada CSS, herencia, especificidad), usa `window.getComputedStyle()`.

```javascript
const caja = document.querySelector('.box');
// Supongamos que en CSS: .box { color: blue; margin: 10px; }

// Esto no funciona (no ve CSS de la hoja)
console.log(caja.style.color); // "" (vacío)

// Esto sí funciona (ve todos los estilos aplicados)
const estilosReales = window.getComputedStyle(caja);
console.log(estilosReales.color); // "rgb(0, 0, 255)" o "blue"
console.log(estilosReales.margin); // "10px"

// También puedes pedir estilos pseudo-elementos
const before = window.getComputedStyle(caja, '::before');
console.log(before.content);
```

***

### 4.3. `classList`: Gestión profesional de clases

La mejor práctica en desarrollo frontend es **definir tus estilos en clases CSS** y usar JavaScript solo para **activar o desactivar** esas clases.

La propiedad `.className` existe pero es un string incómodo de manejar. Lo moderno y correcto es usar `.classList`.

Métodos de `classList`:

* **`add('clase')`**: Añade la clase (si ya existe, no la duplica).
* **`remove('clase')`**: Elimina la clase (si no existe, no falla).
* **`toggle('clase')`**: Si existe la quita, si no existe la pone. Ideal para interruptores.
* **`contains('clase')`**: Devuelve `true` o `false`. Útil para condicionales.
* **`replace('vieja', 'nueva')`**: Reemplaza una clase por otra.

```javascript
const boton = document.querySelector('#modo-oscuro');
const body = document.body;

boton.addEventListener('click', () => {
    // Alternar modo oscuro
    body.classList.toggle('dark-mode');

    // Verificar estado
    if (body.classList.contains('dark-mode')) {
        boton.textContent = '☀️ Modo claro';
    } else {
        boton.textContent = '🌙 Modo oscuro';
    }
});

// Añadir múltiples clases
const elemento = document.querySelector('.card');
elemento.classList.add('highlight', 'active', 'selected');

// Eliminar múltiples
elemento.classList.remove('highlight', 'active');

// Reemplazar
elemento.classList.replace('old-style', 'new-style');
```

***

### 4.4. Manipulación de variables CSS (Custom Properties)

Las variables CSS (también llamadas "Custom Properties") son extremadamente potentes combinadas con JavaScript. Se definen en CSS y se accede a ellas desde JS.

CSS:

```css
:root {
    --color-primario: #3498db;
    --tamaño-fuente: 16px;
}
```

JavaScript:

```javascript
const raiz = document.documentElement; // Elemento <html>

// Cambiar una variable global
raiz.style.setProperty('--color-primario', '#e74c3c');

// Cambiar una variable local a un elemento
const elemento = document.querySelector('.card');
elemento.style.setProperty('--padding', '20px');

// Leer una variable (necesitas getComputedStyle)
const estilos = getComputedStyle(raiz);
console.log(estilos.getPropertyValue('--color-primario')); // "#e74c3c"
```

***

### Resumen del Capítulo

Para modificar la apariencia de elementos:

1. **Si es un cambio de estado** (activo/inactivo, visible/oculto, modo oscuro/claro) → Usa **clases** con `classList`
2. **Si es un valor calculado dinámicamente** (posición X/Y, tamaño dinámico) → Usa **style**
3. **Para leer estilos CSS aplicados** → Usa `getComputedStyle`
4. **Para efectos dinámicos complejos** → Usa **variables CSS**

#### **💡 Conceptos Clave:**

* **`.style`**: Escribir estilos inline (camelCase)
* **`getComputedStyle()`**: Leer estilos CSS finales aplicados
* **`classList.add()`**: Añadir clase CSS
* **`classList.remove()`**: Eliminar clase CSS
* **`classList.toggle()`**: Alternar clase (activar/desactivar)
* **`classList.contains()`**: Verificar si tiene una clase
* **Variables CSS (--propiedad)**: Propiedades dinámicas desde JavaScript
* **Separación de responsabilidades**: CSS para estilos, JS para lógica

#### **🤔 Preguntas de Reflexión:**

1. ¿Por qué es mejor manipular clases que estilos inline?
2. ¿Cuál es la diferencia entre `.style.color` y `getComputedStyle(elemento).color`?
3. ¿Cómo implementarías un toggle de "modo oscuro" usando `classList`?
4. ¿Qué ventaja tienen las variables CSS sobre los estilos inline?
5. ¿Cuándo usarías `toggle` vs `add` en classList?
6. Crea un ejemplo donde cambies dinamicamente el color de fondo usando una variable CSS.

***
