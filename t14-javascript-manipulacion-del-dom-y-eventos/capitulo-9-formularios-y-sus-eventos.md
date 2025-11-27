# Capítulo 9: Formularios y sus Eventos

Los formularios son una de las formas principales de interacción entre usuario y aplicación. Este capítulo cubre cómo JavaScript manipula y responde a eventos de formularios.

### 9.1. Acceso a formularios y elementos

#### **Acceso por `document.forms`**

Todos los formularios de una página se acceden a través de `document.forms`.

```javascript
// document.forms es una HTMLCollection
console.log(document.forms);           // HTMLCollection [form, form]
console.log(document.forms[0]);        // Primer formulario
console.log(document.forms['login']);  // Formulario con name="login"

// Acceso a elementos dentro del formulario
const formulario = document.forms['login'];
console.log(formulario.email);         // Input con name="email"
console.log(formulario.password);      // Input con name="password"
```

#### **Acceso directo por querySelector**

La forma más recomendada es usar selectores CSS:

```html
<form id="mi-formulario">
    <input type="text" name="email" id="email">
    <input type="password" name="password">
    <button type="submit">Login</button>
</form>
```

```javascript
const formulario = document.querySelector('#mi-formulario');
const emailInput = formulario.querySelector('input[name="email"]');
const passwordInput = formulario.querySelector('input[name="password"]');
```

***

### 9.2. Eventos principales de formularios

#### **`submit`**

Se dispara cuando el usuario **envía el formulario** (presiona el botón submit o Enter en un input).

{% hint style="warning" %}
**¡Importante!**: Por defecto, el formulario se envía al servidor. Generalmente queremos **prevenir** este comportamiento con `preventDefault()`.
{% endhint %}

```javascript
const formulario = document.querySelector('#login');

formulario.addEventListener('submit', (evento) => {
    evento.preventDefault(); // Evitar envío al servidor
    
    const email = formulario.email.value;
    const password = formulario.password.value;
    
    console.log(`Email: ${email}, Password: ${password}`);
    // Aquí normalmente harías una petición fetch
});
```

#### **`input`**

Se dispara **cada vez que el usuario cambia el contenido** de un campo (más o menos tecla).

```javascript
const emailInput = document.querySelector('input[name="email"]');

emailInput.addEventListener('input', (evento) => {
    console.log("Valor actual:", evento.target.value);
    // Validación en tiempo real, búsqueda autocompletada, etc.
});
```

#### **`change`**

Se dispara cuando el usuario **termina de editar** un campo (pierde el foco).

```javascript
const emailInput = document.querySelector('input[name="email"]');

emailInput.addEventListener('change', (evento) => {
    console.log("Usuario terminó de editar:", evento.target.value);
    // Validación final, guardar en BD, etc.
});
```

#### **`focus` y `blur`**

* `focus`: El input **recibe el foco** (el usuario empieza a escribir en él)
* `blur`: El input **pierde el foco** (el usuario se va a otro campo)

```javascript
const emailInput = document.querySelector('input[name="email"]');

emailInput.addEventListener('focus', () => {
    emailInput.classList.add('focused');
});

emailInput.addEventListener('blur', () => {
    emailInput.classList.remove('focused');
});
```

***

### 9.3. `preventDefault()` en formularios

Cuando registres un listener en el evento `submit`, casi siempre necesitarás cancelar el envío por defecto.

```javascript
formulario.addEventListener('submit', (evento) => {
    evento.preventDefault(); // Cancela el envío HTTP
    
    // Tu lógica aquí (validación, fetch, etc.)
    console.log("Formulario NO se envió al servidor");
});
```

Sin `preventDefault()`, el navegador recargaría la página y enviaría el formulario al servidor (comportamiento clásico de HTML).

***

### 9.4. Lectura de valores

Cada tipo de input tiene formas diferentes de leer su valor.

#### **`input[type="text"]`, `textarea`**

```javascript
const input = document.querySelector('input[type="text"]');
console.log(input.value); // "Lo que escribió el usuario"

const textarea = document.querySelector('textarea');
console.log(textarea.value);
```

#### **`input[type="checkbox"]`**

```javascript
const checkbox = document.querySelector('input[type="checkbox"]');
console.log(checkbox.checked); // true o false
```

#### **`input[type="radio"]`**

```javascript
// Todos los radio buttons con el mismo name
const radios = document.querySelectorAll('input[name="genero"]');

// Encontrar cuál está seleccionado
const seleccionado = Array.from(radios).find(r => r.checked);
console.log(seleccionado.value);
```

#### **`select`**

```javascript
const select = document.querySelector('select');
console.log(select.value);           // Valor de la opción seleccionada
console.log(select.selectedOptions); // HTMLCollection de opciones seleccionadas
```

***

### 9.5. Objeto `FormData`: Procesamiento moderno

`FormData` es una interfaz moderna para recopilar datos de formularios de forma segura.

```html
<form id="formulario">
    <input type="text" name="nombre">
    <input type="email" name="email">
    <input type="checkbox" name="acepta">
    <button type="submit">Enviar</button>
</form>
```

```javascript
const formulario = document.querySelector('#formulario');

formulario.addEventListener('submit', (evento) => {
    evento.preventDefault();
    
    // Crear FormData desde el formulario
    const formData = new FormData(formulario);
    
    // Acceder a valores
    console.log(formData.get('nombre'));    // Valor del input nombre
    console.log(formData.get('email'));
    
    // Iterar sobre todos los datos
    for (let [clave, valor] of formData) {
        console.log(`${clave}: ${valor}`);
    }
    
    // Enviar al servidor con fetch
    fetch('/api/usuarios', {
        method: 'POST',
        body: formData
    })
    .then(r => r.json())
    .then(datos => console.log("Respuesta:", datos));
});
```

***

### 9.6. Patrón práctico: Validación en tiempo real

```html
<input type="email" id="email" placeholder="tu@email.com">
<span id="error" class="error"></span>
```

```javascript
const emailInput = document.querySelector('#email');
const errorSpan = document.querySelector('#error');

emailInput.addEventListener('input', (evento) => {
    const email = evento.target.value;
    const esValido = /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);
    
    if (esValido) {
        errorSpan.textContent = '';
        emailInput.classList.remove('error');
    } else {
        errorSpan.textContent = 'Email no válido';
        emailInput.classList.add('error');
    }
});
```

***

### Resumen del Capítulo

Los formularios son la interfaz principal para recopilar datos del usuario. JavaScript permite validar, transformar y procesar esos datos en tiempo real. Recuerda usar `preventDefault()` en el evento `submit` para evitar recargas de página innecesarias, y utiliza `FormData` para un manejo moderno y seguro de datos.

#### **💡 Conceptos Clave:**

* **submit**: Evento al enviar el formulario
* **input**: Se dispara al cambiar contenido (cada tecla)
* **change**: Se dispara al terminar de editar
* **focus/blur**: Recibir y perder el foco
* **preventDefault()**: Evitar el envío por defecto
* **Lectura de valores**: .value, .checked según el tipo
* **FormData**: Interfaz moderna para datos de formularios
* **Validación en tiempo real**: Feedback inmediato al usuario

#### **🤔 Preguntas de Reflexión:**

1. ¿Cuál es la diferencia entre los eventos `input` y `change`?
2. ¿Cuándo necesitarías usar `preventDefault()` en un formulario?
3. ¿Cómo leerías el valor de un `<select>` con múltiples selecciones?
4. ¿Cuál es la ventaja de usar `FormData` en lugar de leer cada valor manualmente?
5. ¿Cómo validarías un email en tiempo real mientras el usuario escribe?
6. Crea un formulario con validación que solo permita enviar si los campos son válidos.

***
