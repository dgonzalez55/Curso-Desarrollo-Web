# Capítulo 5: Creación e Inserción de Elementos

Hasta ahora hemos aprendido a **seleccionar y modificar** elementos que ya existen en el HTML. Pero en aplicaciones dinámicas, frecuentemente necesitamos **crear elementos nuevos** desde JavaScript y añadirlos al DOM. Este capítulo cubre todo el ciclo de vida.

### 5.1. El ciclo de vida: Crear, Configurar, Insertar

El proceso típico para añadir un elemento al DOM es:

1. **Crear** el elemento en memoria (no aparece en la página aún)
2. **Configurar** sus propiedades, atributos, contenido
3. **Insertar** en el DOM para que aparezca en la página

```javascript
// Paso 1: Crear
const nuevoDiv = document.createElement('div');

// Paso 2: Configurar
nuevoDiv.textContent = "Soy nuevo";
nuevoDiv.classList.add('card');
nuevoDiv.id = 'card-1';

// Paso 3: Insertar
document.body.appendChild(nuevoDiv);
// Ahora aparece en la página
```

***

### 5.2. `createElement()` y `createTextNode()`

**`document.createElement(tag)`**: Crea un elemento vacío.

```javascript
// Crear varios tipos de elementos
const div = document.createElement('div');
const p = document.createElement('p');
const button = document.createElement('button');
const ul = document.createElement('ul');

// Los elementos existen pero no están en el DOM aún
console.log(div.parentElement); // null
```

**`document.createTextNode(text)`**: Crea un nodo de texto puro (poco usado, normalmente usamos `.textContent`).

```javascript
const texto = document.createTextNode("Contenido de texto");
// Útil para texto que quieres que sea completamente independiente
```

***

### 5.3. Métodos de inserción: `appendChild`, `append`, `prepend`

#### **`appendChild(element)`**

Añade un elemento como **último hijo** del contenedor.

```javascript
const contenedor = document.querySelector('#contenedor');
const nuevo = document.createElement('div');
nuevo.textContent = "Item nuevo";

contenedor.appendChild(nuevo);
```

#### **`append(...elements o texto)`**

Versión moderna de `appendChild`. Acepta múltiples argumentos (elementos o texto).

```javascript
const contenedor = document.querySelector('#contenedor');

// Un elemento
contenedor.append(document.createElement('div'));

// Múltiples elementos
const item1 = document.createElement('li');
const item2 = document.createElement('li');
contenedor.append(item1, item2);

// Incluso texto directo
contenedor.append("Texto directo en el DOM");
```

#### **`prepend(...elements o texto)`**

Lo opuesto: inserta como **primer hijo**.

```javascript
const lista = document.querySelector('ul');
const primerItem = document.createElement('li');
primerItem.textContent = "Primer elemento";

lista.prepend(primerItem); // Va al inicio
```

***

### 5.4. Inserción precisa: `insertAdjacentHTML` e `insertAdjacentElement`

Para insertar elementos en posiciones específicas (no solo al final o inicio), usa `insertAdjacentHTML` o `insertAdjacentElement`. El primero se usa para insertar una cadena de texto con código html mientras que el segundo para elementos ya existentes, en ambos casos el funcionamiento es similar.

Posiciones:

* `'beforebegin'`: Antes del elemento (como hermano anterior)
* `'afterbegin'`: Dentro, como primer hijo
* `'beforeend'`: Dentro, como último hijo
* `'afterend'`: Después del elemento (como hermano posterior)

```html
<!-- Contexto: <div id="box">Contenido</div> -->
```

```javascript
const box = document.querySelector('#box');

// beforebegin: <span></span><div id="box"></div>
box.insertAdjacentHTML('beforebegin', '<span>Antes</span>');

// afterbegin: <div id="box"><span>Dentro</span> ...</div>
box.insertAdjacentHTML('afterbegin', '<span>Dentro al inicio</span>');

// beforeend: <div id="box"> ...<span>Dentro</span></div>
box.insertAdjacentHTML('beforeend', '<span>Dentro al final</span>');

// afterend: <div id="box"></div><span>Después</span>
box.insertAdjacentHTML('afterend', '<span>Después</span>');
```

***

### 5.5. Eliminación de nodos: `remove()` y `removeChild()`

#### **`remove()`: Forma moderna**

Elimina el elemento del DOM directamente.

```javascript
const elemento = document.querySelector('.viejo');
elemento.remove(); // Desaparece del DOM
```

#### **`removeChild(child)`: Forma antigua**

El padre debe llamar este método para eliminar un hijo.

```javascript
const padre = document.querySelector('.contenedor');
const hijo = padre.querySelector('.item');

padre.removeChild(hijo); // Elimina el hijo
```

***

### 5.6. `DocumentFragment`: Renderizado eficiente

Cuando necesitas insertar **muchos elementos**, hacerlo uno por uno es lento porque el navegador actualiza el DOM después de cada inserción.

`DocumentFragment` es un contenedor temporal que acumula elementos en memoria, y luego los insertas todos de una vez.

```javascript
// Sin DocumentFragment (ineficiente)
const contenedor = document.querySelector('#lista');
for (let i = 0; i < 1000; i++) {
    const item = document.createElement('li');
    item.textContent = `Item ${i}`;
    contenedor.appendChild(item); // Actualiza DOM 1000 veces
}

// Con DocumentFragment (eficiente)
const fragment = document.createDocumentFragment();
for (let i = 0; i < 1000; i++) {
    const item = document.createElement('li');
    item.textContent = `Item ${i}`;
    fragment.appendChild(item); // No actualiza el DOM aún
}
// Una sola actualización del DOM
contenedor.appendChild(fragment);
```

***

### 5.7. Patrón práctico: Generar listas desde Arrays

Aprovechando lo que aprendiste en [**Tema 13**](../t13-javascript-arrays-y-objetos-avanzados/), puedes generar listas HTML dinámicamente:

```javascript
// Datos
const usuarios = [
    { id: 1, nombre: "Juan" },
    { id: 2, nombre: "María" },
    { id: 3, nombre: "Carlos" }
];

// Generar HTML con map
const htmlItems = usuarios
    .map(u => `<li data-id="${u.id}">${u.nombre}</li>`)
    .join('');

// Insertar de una vez
const lista = document.querySelector('ul');
lista.innerHTML = htmlItems;

// O con DocumentFragment para ser más eficiente
const fragment = document.createDocumentFragment();
usuarios.forEach(u => {
    const li = document.createElement('li');
    li.textContent = u.nombre;
    li.dataset.id = u.id;
    fragment.appendChild(li);
});
lista.appendChild(fragment);
```

***

### Resumen del Capítulo

Crear elementos dinámicamente es esencial para construir aplicaciones interactivas. Recuerda usar `DocumentFragment` para inserciones masivas y aprovecha los métodos de Array del [Tema 13](../t13-javascript-arrays-y-objetos-avanzados/) para generar contenido basado en datos.

#### **💡 Conceptos Clave:**

* **createElement()**: Crear elemento en memoria
* **appendChild()**: Insertar como último hijo
* **append()**: Versión moderna, acepta múltiples argumentos
* **prepend()**: Insertar como primer hijo
* **insertAdjacentHTML()**: Inserción precisa con posiciones
* **remove()**: Eliminar elemento del DOM
* **removeChild()**: Forma antigua de eliminar
* **DocumentFragment**: Optimizar inserciones masivas
* **Ciclo de vida**: Crear → Configurar → Insertar

#### **🤔 Preguntas de Reflexión:**

1. ¿Cuál es la diferencia entre `appendChild()` y `append()`?
2. ¿Por qué es más eficiente usar `DocumentFragment` para muchos elementos?
3. ¿Cómo generarías una lista HTML a partir de un Array de datos?
4. ¿Cuáles son los cuatro valores posibles de `insertAdjacentHTML()`?
5. ¿Qué sucede si intentas hacer `appendChild()` de un elemento que ya está en el DOM?
6. Crea dinámicamente una tabla HTML con 5 filas a partir de datos.

***
