# Capítulo 1: El DOM y el Árbol de Nodos

Para que JavaScript pueda interactuar con el HTML, el navegador crea una representación intermedia llamada **DOM (Document Object Model)**. Sin el DOM, JavaScript no tendría forma de entender qué es un `<div>` o un `<h1>`.

### 1.1. ¿Qué es el DOM?

El DOM es una interfaz de programación (API) para documentos web. Representa la página de tal manera que los programas pueden cambiar la estructura, el estilo y el contenido del documento.

Imagina el DOM como el "puente" entre el código HTML (texto estático) y JavaScript (lógica dinámica). Cuando el navegador carga una página, convierte el HTML en una estructura de objetos en memoria.

```javascript
// Acceso al documento desde cualquier lugar
console.log(document); // El objeto raíz del DOM
console.log(document.title); // "Mi Página"
console.log(document.body); // El elemento <body>
```

***

### 1.2. La estructura de árbol y tipos de nodos

El DOM organiza el documento como un **árbol jerárquico**.

* **Raíz**: El documento entero (`document`).
* **Ramas y Hojas**: Elementos, atributos y texto.

Ejemplo HTML:

```html
<!DOCTYPE html>
<html>
  <body>
    <h1>Hola</h1>
    <p>Texto</p>
  </body>
</html>
```

En el DOM, esto se convierte en una jerarquía:

* `document` (DOCUMENT\_NODE)
  * `html` (ELEMENT\_NODE)
    * `body` (ELEMENT\_NODE)
      * `h1` (ELEMENT\_NODE) → "Hola" (TEXT\_NODE)
      * `p` (ELEMENT\_NODE) → "Texto" (TEXT\_NODE)

#### **Tipos principales de Nodos**

En el DOM, **todo es un nodo**, pero existen tipos diferentes:

1. **ELEMENT\_NODE (Tipo 1)**: Etiquetas HTML (`<div>`, `<p>`, `<body>`, etc.). Son los que más manipulamos.
2. **TEXT\_NODE (Tipo 3)**: El contenido de texto dentro de una etiqueta. **Importante**: Los saltos de línea y espacios vacíos en tu HTML también crean nodos de texto.
3. **COMMENT\_NODE (Tipo 8)**: Comentarios HTML `<!-- ... -->`.
4. **DOCUMENT\_NODE (Tipo 9)**: El documento completo.

```javascript
// Acceder al tipo de un nodo
const elemento = document.querySelector('h1');
console.log(elemento.nodeType); // 1 (ELEMENT_NODE)
console.log(elemento.nodeName); // "H1"
```

***

### 1.3. El objeto global `window` y `document`

Estos dos objetos son el punto de entrada a todo lo que JavaScript puede hacer en el navegador.

* **`window`**: Representa la ventana del navegador completa. Es el objeto global en el entorno del navegador. Contiene el historial, la barra de direcciones, y al propio documento.
* **`document`**: Es una propiedad de `window` (`window.document`). Representa el contenido de la página web cargada. Es nuestro punto de entrada principal para manipular el HTML.

```javascript
console.log(window.innerWidth);  // Ancho de la ventana
console.log(window.innerHeight); // Alto de la ventana
console.log(document.title);     // Título de la página
console.log(document.body);      // El elemento <body>
```

***

### 1.4. La relación entre HTML y el DOM

Es vital entender que **el DOM no es exactamente el HTML original**.

1. **Corrección automática**: Si escribes HTML inválido (ej: te falta cerrar un `table`), el navegador lo corregirá automáticamente al generar el DOM.
2. **Modificación por JavaScript**: Si insertas un elemento con JS, el DOM cambia, pero el archivo HTML original en el servidor sigue igual.
3. **Dinámico**: El DOM cambia constantemente mientras el usuario interactúa con la página.

```javascript
// Modificar el DOM
document.body.innerHTML = "<h1>Nuevo contenido</h1>";
// El HTML del servidor no cambió, solo el DOM en la memoria
```

***

### 1.5. Inspeccionando el DOM en DevTools

Como desarrollador, tu mejor herramienta es la pestaña **Elements** (Elementos) de las DevTools del navegador (F12, Ctrl+Shift+I o Cmd+Option+I).

* Lo que ves ahí es el **DOM actual**, no el código fuente HTML original.
* Si seleccionas un elemento en esa pestaña, puedes acceder a él en la consola escribiendo `$0`.
* Los cambios que hagas en DevTools son temporales; desaparecen al recargar.

***

### Resumen del Capítulo

El DOM es una representación en forma de árbol en memoria del documento HTML. `document` es el punto de entrada principal para acceder a este árbol desde JavaScript. Entender que existen diferentes tipos de nodos (elementos vs texto vs comentarios) es clave para evitar errores al navegar por la estructura y manipularla eficientemente.

#### **💡 Conceptos Clave:**

* **DOM (Document Object Model)**: Representación en árbol del HTML en memoria
* **Tipos de nodos**: ELEMENT\_NODE, TEXT\_NODE, COMMENT\_NODE, DOCUMENT\_NODE
* **`window`**: Objeto global que representa la ventana del navegador
* **`document`**: Objeto que representa el contenido de la página cargada
* **Diferencia HTML vs DOM**: El DOM es dinámico y puede ser modificado por JavaScript
* **DevTools Elements**: Herramienta para inspeccionar y debuggear el DOM en tiempo real
* **`$0`**: En la consola, referencia al elemento seleccionado en DevTools

#### **🤔 Preguntas de Reflexión:**

1. ¿Cuál es la diferencia entre el HTML original del servidor y el DOM que ve JavaScript?
2. ¿Qué es un nodo de texto y por qué es importante entenderlos?
3. ¿Por qué `document.body` es el punto de partida común para acceder al contenido?
4. Abre DevTools en cualquier página web y selecciona un elemento. ¿Cómo accederías a ese elemento desde la consola?
5. ¿Cómo verías el tipo de nodo de un elemento usando propiedades de JavaScript?
6. ¿Qué sucede con el DOM cuando modificas el HTML desde JavaScript? ¿Se guarda en el servidor?

***
