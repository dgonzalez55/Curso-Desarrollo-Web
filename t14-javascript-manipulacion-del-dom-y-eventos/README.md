# T14: JavaScript - Manipulación del DOM y Eventos

### Tabla de Contenidos

#### **🌳** [**Capítulo 1: El DOM y el Árbol de Nodos**](capitulo-1-el-dom-y-el-arbol-de-nodos.md)

* 1.1. ¿Qué es el DOM? (Document Object Model)
* 1.2. La estructura de árbol y tipos de nodos
* 1.3. El objeto global `window` y `document`
* 1.4. La relación entre HTML y el DOM
* 1.5. Inspeccionando el DOM en DevTools

### **🔍** [**Capítulo 2: Selección de Elementos**](capitulo-2-seleccion-de-elementos.md)

* 2.1. Métodos modernos: `querySelector` y `querySelectorAll`
* 2.2. Métodos clásicos: `getElementById`, `getElementsByClassName`
* 2.3. NodeList vs HTMLCollection vs Array
* 2.4. Conversión a Array (uso de `Array.from` y spread)
* 2.5. Selectores CSS avanzados en JavaScript

### **✏️** [**Capítulo 3: Lectura y Modificación de Contenido**](capitulo-3-lectura-y-modificacion-de-contenido.md)

* 3.1. `textContent` vs `innerText`: Texto plano
* 3.2. `innerHTML`: Insertando HTML (y riesgos de XSS)
* 3.3. Leer y modificar atributos: `getAttribute`, `setAttribute`
* 3.4. Propiedades directas vs Atributos HTML (`id`, `src`, `value`, `href`)
* 3.5. Data Attributes (`dataset`): Guardando datos en el DOM

### **🎨** [**Capítulo 4: Estilos CSS y Clases**](capitulo-4-estilos-css-y-clases.md)

* 4.1. La propiedad `style`: Estilos en línea
* 4.2. `window.getComputedStyle()`: Leer estilos finales
* 4.3. Gestión profesional con `classList` (`add`, `remove`, `toggle`, `contains`)
* 4.4. Manipulación de variables CSS (Custom Properties)

### **🏗️ Capítulo 5: Creación e Inserción de Elementos**

* 5.1. El ciclo de vida: Crear, Configurar, Insertar
* 5.2. `createElement()` y `createTextNode()`
* 5.3. Métodos de inserción: `appendChild`, `append`, `prepend`
* 5.4. Inserción precisa: `insertAdjacentHTML` y `insertAdjacentElement`
* 5.5. Eliminación de nodos: `remove()` y `removeChild()`
* 5.6. `DocumentFragment`: Renderizado eficiente

### **🧭 Capítulo 6: Navegación por el DOM (Traversing)**

* 6.1. Navegar hacia los padres: `parentElement`, `closest`
* 6.2. Navegar hacia los hijos: `children`, `firstElementChild`, `lastElementChild`
* 6.3. Navegar entre hermanos: `nextElementSibling`, `previousElementSibling`
* 6.4. Diferencia entre Elementos y Nodos (texto/comentarios)

### **⚡ Capítulo 7: Introducción a los Eventos**

* 7.1. ¿Qué es un evento? Modelo asíncrono básico
* 7.2. `addEventListener`: La forma correcta de escuchar
* 7.3. El objeto `Event`: propiedades comunes (`target`, `type`)
* 7.4. Eliminar eventos: `removeEventListener`
* 7.5. El problema de `this` en los eventos y Arrow Functions

### **🖱️ Capítulo 8: Eventos de Ratón y Teclado**

* 8.1. Ratón: `click`, `dblclick`, `mousedown`, `mouseup`
* 8.2. Movimiento: `mousemove`, `mouseenter` vs `mouseover`
* 8.3. Teclado: `keydown`, `keyup` (y el obsoleto `keypress`)
* 8.4. Propiedades de teclado: `key` vs `code`
* 8.5. Modificadores: `ctrlKey`, `shiftKey`, `altKey`

### **📝 Capítulo 9: Formularios y sus Eventos**

* 9.1. Acceso a formularios y elementos (`document.forms`)
* 9.2. Eventos principales: `submit`, `input`, `change`, `focus`, `blur`
* 9.3. `event.preventDefault()`: Controlar el envío
* 9.4. Lectura de valores (`value`, `checked`)
* 9.5. Objeto `FormData`: Procesamiento moderno de formularios

### **🌊 Capítulo 10: El Flujo de Eventos (Propagation)**

* 10.1. Las 3 fases: Capturing, Target, Bubbling
* 10.2. Entendiendo el Bubbling (Burbujeo)
* 10.3. `stopPropagation()` y `stopImmediatePropagation()`
* 10.4. **Event Delegation**: El patrón de oro para rendimiento
* 10.5. Casos prácticos de delegación

### **🌍 Capítulo 11: El BOM y Web APIs Básicas**

* 11.1. El objeto `window` y dimensiones del viewport
* 11.2. `localStorage` y `sessionStorage` (Repaso práctico)
* 11.3. Timers: `setTimeout`, `setInterval` y `requestAnimationFrame`
* 11.4. Objeto `location` (URL) y `history`

### **🚀 Capítulo 12: Buenas Prácticas y Proyecto Integrador**

* 12.1. Minimizar Reflow y Repaint (Rendimiento)
* 12.2. Separación de responsabilidades (HTML/CSS/JS)
* 12.3. Gestión de memoria: limpiar eventos
* 12.4. Accesibilidad (A11Y) desde JavaScript
* 12.5. Estructura de una aplicación SPA vainilla
