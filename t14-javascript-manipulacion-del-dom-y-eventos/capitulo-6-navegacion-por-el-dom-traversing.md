# Capítulo 6: Navegación por el DOM (Traversing)

Una vez que has seleccionado un elemento, frecuentemente necesitas acceder a sus **parientes** en el árbol: padres, hijos, hermanos. Este capítulo cubre todas las formas de navegar.

### 6.1. Navegar hacia los padres: `parentElement` y `closest()`

#### **`parentElement`**

Accede al padre directo (elemento que contiene el elemento actual).

```javascript
const parrafo = document.querySelector('p');
const padre = parrafo.parentElement;
console.log(padre.tagName); // Ej: "DIV"

// Subir múltiples niveles
const abuelo = parrafo.parentElement.parentElement;
```

#### **`closest(selector)`**

Sube en la jerarquía hasta encontrar un elemento que coincida con el selector CSS. Es muy útil para "delegación de eventos".

```javascript
// HTML: <div class="contenedor"> <button class="btn">Haz clic</button> </div>
const boton = document.querySelector('button');

// Encuentra el contenedor más cercano
const contenedor = boton.closest('.contenedor');
console.log(contenedor); // <div class="contenedor">

// Si no encuentra nada, retorna null
const noExiste = boton.closest('.inexistente');
console.log(noExiste); // null

// Puede ser él mismo
const esElMismo = boton.closest('button');
console.log(esElMismo === boton); // true
```

***

### 6.2. Navegar hacia los hijos: `children`, `firstElementChild`, `lastElementChild`, `childNodes`

#### **`children`**

Una **HTMLCollection** con todos los elementos hijo (no incluye nodos de texto).

```javascript
const contenedor = document.querySelector('#lista');
console.log(contenedor.children); // HTMLCollection [li, li, li]
console.log(contenedor.children.length); // 3

// Acceder por índice
console.log(contenedor.children[0]); // Primer hijo
console.log(contenedor.children[contenedor.children.length - 1]); // Último
```

#### **`firstElementChild` y `lastElementChild`**

El primer y último elemento hijo.

```javascript
const lista = document.querySelector('ul');

const primero = lista.firstElementChild;
const ultimo = lista.lastElementChild;

console.log(primero.textContent); // Primer item
console.log(ultimo.textContent);  // Último item
```

#### **`childNodes` (con nodos de texto)**

Incluye **todos** los nodos, incluyendo nodos de texto (espacios, saltos de línea).

```html
<!-- HTML con espacios -->
<ul>
  <li>Item 1</li>
  <li>Item 2</li>
</ul>
```

```javascript
const lista = document.querySelector('ul');

// childNodes incluye nodos de texto (espacios)
console.log(lista.childNodes.length); // Posiblemente 5 o más

// children solo elementos
console.log(lista.children.length);   // 2 (solo <li>)

// **Recomendación**: Usa children si quieres solo elementos
```

***

### 6.3. Navegar entre hermanos: `nextElementSibling`, `previousElementSibling`

#### **`nextElementSibling`**

El siguiente elemento hermano.

```javascript
const item = document.querySelector('li');
const siguiente = item.nextElementSibling;
if (siguiente) {
    console.log(siguiente.textContent);
}
```

#### **`previousElementSibling`**

El elemento hermano anterior.

```javascript
const item = document.querySelector('li:last-child');
const anterior = item.previousElementSibling;
console.log(anterior.textContent);
```

#### **Recorrer hermanos**

Navegar entre hermanos es útil para lógica que necesita comparar o acceder a elementos relacionados.

```javascript
const itemActual = document.querySelector('.active');

// Desactivar hermanos
let hermano = itemActual.parentElement.firstElementChild;
while (hermano) {
    hermano.classList.remove('active');
    hermano = hermano.nextElementSibling;
}

// Activar el actual
itemActual.classList.add('active');
```

***

### 6.4. Diferencia entre Elementos y Nodos (texto/comentarios)

Este es un punto crítico que causa confusión:

* **Nodos (nodeType)**: Incluyen elementos, texto, comentarios, todo.
* **Elementos (Element)**: Solo etiquetas HTML.

```html
<!-- HTML: -->
<div id="contenedor">
  <!-- Comentario -->
  <p>Párrafo</p>
  
  <!-- Más espacios -->
</div>
```

```javascript
const contenedor = document.querySelector('#contenedor');

// childNodes: TODO (incluyendo espacios en blanco como TEXT_NODE)
console.log(contenedor.childNodes.length); // Posiblemente 5

// children: Solo elementos <p>
console.log(contenedor.children.length);   // 1

// Iterar sobre elementos (lo que generalmente quieres)
contenedor.children.forEach(elemento => {
    console.log(elemento.tagName);
});
```

***

### 6.5. Patrón práctico: Recorrer un árbol recursivamente

Buscar elementos profundamente anidados:

```javascript
function buscarPor(selector, root = document) {
    const resultados = [];
    
    function recorrer(nodo) {
        if (nodo.matches && nodo.matches(selector)) {
            resultados.push(nodo);
        }
        
        // Recorrer hijos
        for (let hijo of nodo.children) {
            recorrer(hijo);
        }
    }
    
    recorrer(root);
    return resultados;
}

// Usar
const todosLosBotones = buscarPor('button');
```

***

### Resumen del Capítulo

La navegación por el DOM es esencial para construir lógica que manipule múltiples elementos relacionados. Recuerda preferir `.children` (elementos) sobre `.childNodes` (todos los nodos) en la mayoría de casos, y usa `closest()` para subir en la jerarquía de forma elegante.

#### **💡 Conceptos Clave:**

* **parentElement**: Acceder al contenedor directo
* **closest(selector)**: Subir hasta encontrar coincidencia
* **children**: Todos los elementos hijo (HTMLCollection)
* **firstElementChild, lastElementChild**: Primer/último hijo
* **nextElementSibling, previousElementSibling**: Hermanos
* **childNodes vs children**: Nodos (incluyendo texto) vs solo elementos
* **Navegación**: Forma de recorrer relaciones en el árbol
* **Recorrido recursivo**: Para búsquedas profundas

#### **🤔 Preguntas de Reflexión:**

1. ¿Cuál es la diferencia entre `parentElement` y `closest()`?
2. ¿Qué retorna `nextElementSibling` si no hay siguiente?
3. ¿Por qué `.children` suele ser preferible a `.childNodes`?
4. ¿Cómo usarías `closest()` dentro de un event listener?
5. ¿Cómo recorrerías todos los elementos hermanos de un nodo?
6. Crea una función que suba al antecesor más cercano con clase 'card'.

***
