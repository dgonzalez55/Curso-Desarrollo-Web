# Capítulo 3: Lectura y Modificación de Contenido

Una vez seleccionado un elemento, lo más común es querer **leer qué dice** o **cambiar su contenido**. Este capítulo explora las formas correctas de hacer esto de manera segura.

### 3.1. `textContent` vs `innerText`: Diferencias críticas

Ambas propiedades sirven para leer o escribir texto plano dentro de un elemento, pero tienen diferencias importantes que debes conocer.

* **`textContent`**: Devuelve **todo** el texto contenido en el nodo, incluyendo el de elementos ocultos (con CSS) y espacios de formato. Es más rápido y es el estándar.
* **`innerText`**: Tiene en cuenta los estilos CSS. Si un elemento está oculto (`display: none`), `innerText` no lo devolverá. Además, provoca un "reflow" (recalcular todo el diseño), por lo que es mucho más lento.

```javascript
// HTML: <h1>Bienvenido</h1>
const titulo = document.querySelector('h1');

// Leer
console.log(titulo.textContent); // "Bienvenido"

// Escribir (reemplaza el contenido)
titulo.textContent = "Nuevo Título";

// Si el elemento contiene HTML, textContent lo trata como texto literal
titulo.textContent = "<strong>Negrita</strong>";
// Resultado: el texto literal "<strong>Negrita</strong>" aparece en la página
```

{% hint style="success" %}
**Recomendación**: Usa `textContent` por defecto por rendimiento y simplicidad.
{% endhint %}

***

### 3.2. `innerHTML`: Insertando HTML (y sus riesgos)

`innerHTML` te permite leer o escribir el contenido como una cadena HTML. Esto significa que el navegador "parseará" la cadena y creará los elementos DOM correspondientes.

```javascript
const caja = document.querySelector('.caja');

// Leer HTML interno
console.log(caja.innerHTML); 
// "<p>Primer párrafo</p><p>Segundo párrafo</p>"

// Escribir HTML (se parsea y crea elementos)
caja.innerHTML = '<strong>Texto en negrita</strong> y <em>cursiva</em>';
```

{% hint style="danger" %}
&#x20;**El peligro crítico: XSS (Cross-Site Scripting)**

**Nunca uses `innerHTML` con datos que provengan de un usuario** (inputs, formularios, bases de datos no verificadas). Si insertas un `<script>` o event handlers, alguien podría ejecutar código malicioso en el navegador de tus usuarios.

```javascript
// ¡PELIGROSO! Nunca hagas esto:
const nombreUsuario = "<img src=x onerror='alert(\"Hackeado\")'>";
document.body.innerHTML = "Hola " + nombreUsuario; // Ejecuta el alert

// ¡PELIGROSO! Event handler incrustado:
document.body.innerHTML = "<button onclick='enviarDatos()'>Haz clic</button>";
```
{% endhint %}

#### **Regla de oro**:

* Usa `textContent` para datos de usuarios
* Usa `innerHTML` solo para HTML que **tú** escribiste y controlas completamente

***

### 3.3. Leer y modificar atributos

Los elementos HTML tienen atributos como `href`, `src`, `id`, `data-*`, etc.

* **`getAttribute('nombre')`**: Obtiene el valor del atributo.
* **`setAttribute('nombre', 'valor')`**: Cambia el valor.
* **`removeAttribute('nombre')`**: Elimina el atributo.
* **`hasAttribute('nombre')`**: Devuelve true/false si el atributo existe.

```javascript
const imagen = document.querySelector('img');

// Leer
console.log(imagen.getAttribute('src'));    // "foto.jpg"
console.log(imagen.getAttribute('alt'));    // "Mi foto"

// Escribir
imagen.setAttribute('src', 'nueva-foto.jpg');
imagen.setAttribute('alt', 'Descripción accesible');

// Verificar
if (imagen.hasAttribute('loading')) {
    console.log("Tiene lazy loading");
}

// Eliminar
imagen.removeAttribute('alt');
```

***

### 3.4. Propiedades directas: Acceso más cómodo

Muchos atributos estándar tienen su reflejo directo como **propiedad** en el objeto JavaScript del elemento. Esto es más cómodo que usar `getAttribute`.

```javascript
const input = document.querySelector('input');

// Forma con setAttribute
input.setAttribute('value', 'Hola');

// Forma con propiedad directa (más común)
input.value = 'Hola';
input.type = 'email';
input.placeholder = 'Tu email';

const link = document.querySelector('a');
link.href = 'https://google.com';
link.target = '_blank';

const imagen = document.querySelector('img');
imagen.src = 'nueva-foto.jpg';
imagen.alt = 'Descripción';
```

**Propiedad importante**: Las propiedades directas son **bidireccionales**. Si el usuario cambia un `<input>`, la propiedad `.value` refleja el cambio.

***

### 3.5. Data Attributes (dataset): Guardar datos personalizados

HTML5 introdujo los atributos `data-*` para que los desarrolladores podamos guardar información personalizada en las etiquetas sin ensuciar atributos estándar o depender de clases CSS.

HTML:

```html
<div id="usuario" data-id="123" data-rol="admin" data-fecha-registro="2023-11-20">
    Usuario
</div>
```

Acceso desde JavaScript (propiedad `dataset`):

```javascript
const userDiv = document.querySelector('#usuario');

// Leer (nota: guiones en HTML se convierten a camelCase)
console.log(userDiv.dataset.id);               // "123"
console.log(userDiv.dataset.rol);              // "admin"
console.log(userDiv.dataset.fechaRegistro);    // "2023-11-20"

// Escribir
userDiv.dataset.rol = 'superadmin';  // Actualiza el atributo HTML
userDiv.dataset.nuevoAtributo = 'valor';

// Leer todos
console.log(userDiv.dataset);
// { id: "123", rol: "superadmin", fechaRegistro: "2023-11-20", nuevoAtributo: "valor" }
```

Esta es una excelente forma de vincular tu lógica JS (Arrays de usuarios) con la representación visual en el DOM.

***

### Resumen del Capítulo

La lectura y modificación de contenido es una de las tareas más frecuentes al trabajar con el DOM. Recuerda usar `textContent` para texto seguro y `innerHTML` solo para contenido que controlas completamente. Los data-attributes son perfectos para vincular estados de JavaScript con elementos HTML.

#### **💡 Conceptos Clave:**

* **textContent**: Leer/escribir texto plano (seguro, rápido)
* **innerText**: Considera estilos CSS (lento, menos usado)
* **innerHTML**: Leer/escribir HTML completo (CUIDADO con XSS)
* **getAttribute/setAttribute**: Acceso general a atributos
* **Propiedades directas**: Acceso más cómodo a atributos estándar
* **data-attributes (dataset)**: Guardar datos personalizados en el HTML
* **XSS (Cross-Site Scripting)**: Riesgo de seguridad al insertar contenidos de usuario

#### **🤔 Preguntas de Reflexión:**

1. ¿Cuál es la diferencia entre `textContent` e `innerHTML`?
2. ¿Por qué no deberías usar `innerHTML` con datos de usuarios?
3. ¿Cuál es la ventaja de usar propiedades directas (`input.value`) sobre `getAttribute`?
4. ¿Cómo guardarías un ID de usuario en un elemento HTML sin contaminar el atributo `id`?
5. Crea un elemento `<div>` con varios `data-*` atributos y accede a ellos vía `dataset`.
6. ¿Cuál sería el riesgo si concatenas un nombre de usuario directamente en `innerHTML`?

***
