# Capítulo 2: Selección de Elementos

Antes de poder hacer algo con un elemento (cambiar su color, ocultarlo, leer su texto), necesitas **encontrarlo** en el árbol del DOM. JavaScript nos ofrece varias herramientas para esto, desde métodos modernos hasta clásicos.

### 2.1. Métodos modernos: `querySelector` y `querySelectorAll`

Son los métodos estándar hoy en día. Permiten seleccionar elementos usando **selectores CSS**, lo que los hace extremadamente potentes y flexibles.

* **`document.querySelector(selector)`**: Devuelve el **primer** elemento que coincida. Si no encuentra nada, devuelve `null`.
* **`document.querySelectorAll(selector)`**: Devuelve una lista (**NodeList**) con **todos** los elementos que coincidan.

```javascript
// Seleccionar por etiqueta
const titulo = document.querySelector('h1');

// Seleccionar por clase (nota el punto)
const tarjeta = document.querySelector('.card');

// Seleccionar por ID (nota la almohadilla)
const header = document.querySelector('#main-header');

// Selectores complejos (hijo directo)
const links = document.querySelectorAll('nav > ul > li > a');

// Seleccionar con atributos
const inputs = document.querySelectorAll('input[type="text"]');
```

***

### 2.2. Métodos clásicos: `getElementById`, `getElementsByClassName`, `getElementsByTagName`

Estos métodos son más antiguos pero siguen siendo muy rápidos y específicos. Es probable que los encuentres en código _legacy_.

* **`document.getElementById('id')`**: El más rápido. Devuelve un elemento único. Nota: No lleva `#`.
* **`document.getElementsByClassName('clase')`**: Devuelve una **HTMLCollection** (colección "viva") de elementos.
* **`document.getElementsByTagName('tag')`**: Similar al anterior, pero por etiqueta (ej: 'div').

```javascript
// Método clásico
const elemento = document.getElementById('principal');

// Equivalente con querySelector
const elemento2 = document.querySelector('#principal');

// getElementsByClassName devuelve HTMLCollection viva
const activos = document.getElementsByClassName('active');
```

***

### 2.3. NodeList vs HTMLCollection vs Array

Aquí es donde muchos principiantes se confunden. Las colecciones devueltas por los métodos de selección **no son Arrays verdaderos**.

* **HTMLCollection**: Es una colección "viva". Si el DOM cambia, la colección se actualiza sola automáticamente. Retornada por métodos `getElementsBy...`.
* **NodeList**: Generalmente estática (como una foto del momento exacto en que pediste los datos). Retornada por `querySelectorAll`. Las NodeList modernas sí tienen `.forEach()`.
* **Array**: Verdadero Array con todos los métodos (`.map()`, `.filter()`, `.reduce()`, etc.).

```javascript
// HTMLCollection
const divs = document.getElementsByClassName('box');
console.log(divs.length); // 3

// Si añado un div con clase 'box', divs.length cambia automáticamente
document.body.innerHTML += '<div class="box"></div>';
console.log(divs.length); // 4 (¡se actualiza solo!)

// NodeList (estática)
const nodelist = document.querySelectorAll('.box');
console.log(nodelist.length); // 4
document.body.innerHTML += '<div class="box"></div>';
console.log(nodelist.length); // 4 (no cambió)
```

***

### 2.4. Conversión a Array: `Array.from()` y Spread Operator

Para usar toda la potencia de los métodos de Array que aprendiste en el [Tema 13](../t13-javascript-arrays-y-objetos-avanzados/) (`map`, `filter`, `reduce`), debes convertir estas colecciones a Arrays verdaderos.

#### **Opción 1: `Array.from()` (Recomendada)**

```javascript
const botones = document.querySelectorAll('.btn');
const botonesArray = Array.from(botones);

// Ahora sí podemos usar map, filter, etc.
const textos = botonesArray.map(btn => btn.textContent);
```

#### **Opción 2: Spread Operator `[...]`**

```javascript
const divs = document.getElementsByTagName('div');
const divsArray = [...divs];

const alturas = divsArray.map(div => div.offsetHeight);
```

***

### 2.5. Selectores CSS avanzados en JavaScript

Gracias a `querySelector`, puedes usar lógica CSS avanzada para seleccionar elementos sin añadir clases extra:

```javascript
// Seleccionar inputs de tipo texto
const inputsTexto = document.querySelectorAll('input[type="text"]');

// Seleccionar el primer elemento de lista que sea impar
const itemImpar = document.querySelector('li:nth-child(odd)');

// Seleccionar elementos que NO tengan una clase
const noActivos = document.querySelectorAll('.usuario:not(.active)');

// Seleccionar todos menos el último
const items = document.querySelectorAll('li:not(:last-child)');

// Seleccionar hijos directos
const hijosDirectos = document.querySelectorAll('.padre > .hijo');
```

***

### Resumen del Capítulo

La selección de elementos es el primer paso para manipular el DOM. Usa `querySelector` y `querySelectorAll` para el 95% de tus necesidades por su flexibilidad con selectores CSS. Recuerda siempre que lo que devuelven no son Arrays puros; a menudo necesitarás usar `Array.from()` o el operador spread `[...]` para manipularlos cómodamente.

#### **💡 Conceptos Clave:**

* **querySelector**: Selecciona el primer elemento que coincida
* **querySelectorAll**: Selecciona todos los elementos que coincidan (retorna `NodeList`)
* **getElementById, getElementsByClassName, getElementsByTagName**: Métodos clásicos
* **HTMLCollection**: Colección "viva" que se actualiza con cambios en el DOM
* **NodeList**: Colección estática (fotografía del DOM en el momento de la selección)
* **Array.from() y spread \[...]**: Convierte colecciones a Arrays verdaderos
* **Selectores CSS**: Puedes usar toda la potencia de CSS en JavaScript

#### **🤔 Preguntas de Reflexión:**

1. ¿Cuál es la diferencia entre `querySelector` y `getElementById`?
2. ¿Por qué querySelectorAll devuelve una NodeList y no un Array?
3. ¿Cuál es la diferencia entre una HTMLCollection y una NodeList?
4. ¿Cómo convertirías una NodeList a un Array para usar `.map()`?
5. Escribe un selector CSS avanzado que encuentre todos los botones dentro de un formulario.
6. ¿Cuándo es importante entender que una HTMLCollection es "viva"?

***
