# Capítulo 2: La Trinidad del Desarrollo Web Frontend

Ningún pintor domina su arte usando solo un color; necesita una paleta completa de colores trabajando juntos en armonía. Así, una persona desarrolladora frontend no domina su arte con solo JavaScript: necesita comprender cómo HTML, CSS y JavaScript colaboran para crear experiencias web completas. Aunque hoy en día frameworks y arquitecturas basadas en componentes son fundamentales, la base sigue siendo esta trinidad. Este capítulo explora la relación entre las tecnologías clásicas y cómo JavaScript potencia las capacidades de HTML y CSS en 2025.

***

### 2.1. HTML, CSS y JavaScript: Roles complementarios

Para comprender JavaScript en contexto, aclaremos el rol de cada tecnología en la actualidad:

#### **HTML: La Estructura**

HTML (HyperText Markup Language) define la **estructura semántica** del contenido. Es el esqueleto de la web:

```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <meta charset="UTF-8">
    <title>Mi Página Web</title>
  </head>
  <body>
    <header>
      <h1>Bienvenido</h1>
    </header>
    <main>
      <p>Este es el contenido principal.</p>
      <button id="miBoton">Haz clic</button>
    </main>
    <footer>
      <p>Pie de página</p>
    </footer>
  </body>
</html>
```

**Responsabilidades de HTML:**

* Definir elementos semánticos (encabezados, listas, formularios…)
* Estructurar el contenido de forma lógica
* Proporcionar accesibilidad con etiquetas semánticas
* Cargar recursos (scripts, hojas de estilo, imágenes...)

***

#### **CSS: La Presentación**

CSS (Cascading Style Sheets) determina cómo **luce** el contenido. Es la “ropa” de la página. En 2025 es común el uso de variables CSS (`custom properties`), media queries modernas y diseño responsivo avanzado.

```css
:root {
--color-principal: #007bff;
--color-hover: #0056b3;
}
body {
font-family: Arial, sans-serif;
background-color: #f5f5f5;
}
button {
background-color: var(--color-principal);
color: white;
padding: 10px 20px;
border: none;
border-radius: 5px;
cursor: pointer;
transition: background-color 0.3s ease;
}
button:hover {
background-color: var(--color-hover);
}

```

**Responsabilidades de CSS:**

* Estilos visuales, fuentes y colores
* Maquetación y posicionamiento
* Animaciones y transiciones declarativas
* Responsive design y temas gracias a `custom properties` (variables CSS)

***

#### **JavaScript: La Interactividad**

JavaScript es el **cerebro** de la página. Permite responder a eventos y modificar dinámicamente estructura y estilos del documento. Aunque el desarrollo moderno tiende a la modularidad y los frameworks, dominar la manipulación básica sigue siendo esencial.

```javascript
// Seleccionar el botón
const miBoton = document.getElementById('miBoton');
miBoton.addEventListener('click', () => {
console.log('¡El botón fue pulsado!');
// Añadir contenido dinámico
document.querySelector('main').innerHTML += '<p>Nuevo párrafo añadido dinámicamente</p>';
// Cambiar una variable CSS de forma moderna
document.documentElement.style.setProperty('--color-principal', '#ff6b6b');
});

```

**Responsabilidades de JavaScript:**

* Gestionar eventos del usuario
* Manipular el DOM (Document Object Model)
* Realizar validaciones y lógica de negocio
* Hacer peticiones asíncronas a servidores (`fetch`, APIs)
* Animar elementos y modificar variables CSS

***

### 2.2. Integración de JavaScript con HTML

#### **La mejor práctica actual: `<script type="module">`**

En 2025, la recomendación general es cargar los scripts JavaScript como módulos ES6 usando la etiqueta:

```html
<script type="module" src="app.js"></script>
```

**Ventajas:**

* Permite import/export de módulos ("import ... from ...")
* El script se ejecuta de forma diferida automáticamente (`defer` por defecto)
* El código está mejor aislado y es más mantenible
* Se puede ubicar el `<script>` en el `<head>` si se desea, o al final del `<body>`, pero ya no es necesario “esconderlo” para rendimiento

**Ejemplo básico con módulos:**

```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <meta charset="UTF-8">
    <title>Aplicación Módulos</title>
    <script type="module" src="app.js"></script>
  </head>
  <body>
    <button id="miBoton">Haz clic</button>
  </body>
</html>
```

Y en `app.js`:

```javascript
document.getElementById('miBoton').addEventListener('click', () => {
alert('¡Hola desde un módulo ECMAScript!');
});

```

***

#### Otras formas (válidas, pero menos recomendadas para código moderno)

* **Script inline**: `<button onclick="alert('Hola')">Haz clic</button>`\
  (Solo para ejemplos muy pequeños o landing pages)
* **Script tradicional**: `<script src="..."></script>`\
  Solo si necesitas asegurar compatibilidad con navegadores muy antiguos.

***

#### **¿Por qué se emplea `type="module"`?**

* Los módulos permiten importar/exportar funciones, clases y constantes entre archivos JS.
* Se ejecutan de forma deferida, evitando bloqueos en el parseo HTML.
* Fomentan la reutilización y la organización del código.

***

### 2.3. Integración de JavaScript con CSS

#### **Modificar estilos mediante variables CSS**

Además de manipular clases CSS con `classList`, cabe reseñar que hoy en día es habitual la manipulación de variables CSS directamente desde JS:

```javascript
// Cambiar tema dinámicamente
document.documentElement.style.setProperty('--color-principal', '#6610f2');
```

#### **Modificar estilos mediante clases CSS (Recomendado)**

No obstante, la práctica recomendada sigue siendo modificar clases CSS para activar estilos que ya se definieron en la hoja de estilos:

```javascript
// Agregar una clase
element.classList.add('activo');
// Quitar una clase
element.classList.remove('oculto');
// Alternar una clase
element.classList.toggle('otro-estado');
```

#### **Modificar estilos inline (No recomendado -&#x20;**_**Legacy**_**)**

```javascript
const elemento = document.getElementById('miElemento');

// Cambiar un estilo específico
elemento.style.backgroundColor = 'blue';
elemento.style.fontSize = '20px';
elemento.style.display = 'none'; // Ocultar
```

#### **Ventajas de usar clases CSS sobre estilos inline:**

| Aspecto                 | Estilos Inline       | Clases CSS                       |
| ----------------------- | -------------------- | -------------------------------- |
| **Mantenibilidad**      | Difícil, disperso    | Centralizado y limpio            |
| **Reutilización**       | Pobre                | Máxima                           |
| **Especificidad**       | Alta, poco flexible  | Controlada                       |
| **Rendimiento**         | Menor                | CSS más eficiente                |
| **Separación de roles** | JavaScript para todo | CSS para estilos, JS para lógica |

***

### 2.4. El flujo de carga de una página web

Entender el flujo de carga es crucial para optimizar rendimiento y evitar errores comunes:

1. **El navegador solicita y parsea el HTML**\
   El DOM se construye elemento a elemento.
2. **Descarga recursos externos:**\
   CSS, imágenes y JS mediante etiquetas `<link>`, `<img>` y `<script>`.
3. **Ejecución de scripts:**\
   Con `type="module"`, los scripts se ejecutan diferidos automáticamente después de parsear el documento.
4. **Renderizado**\
   El navegador pinta la página.
5. **Eventos**\
   Ya puedes interactuar: los listeners JS funcionan sobre elementos del DOM.

{% hint style="danger" %}
**¡Cuidado!**\
Si intentas acceder a un elemento antes de que exista en el DOM, obtendrás `null`. Por eso, los scripts modernos usan módulos o esperan al evento `DOMContentLoaded` (pero con módulos ya no suele ser necesario).

{% hint style="success" %}
**Soluciones:**

* Colocar `<script type="module">` en el `<head>`, ya que se difiere automáticamente.
* Usar el atributo `defer` si no usas módulos.
* O escuchar el evento `DOMContentLoaded`:

```javascript
document.addEventListener('DOMContentLoaded', () => {
/* Tu código */
});

```
{% endhint %}
{% endhint %}

***

### 2.5. Ejemplo integrado: aplicación web simple

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Contador Interactivo</title>
    <script type="module" src="contador.js"></script>
    <style>
        :root {
            --color-up: #2ecc71;
            --color-down: #e74c3c;
            --color-zero: #667eea;
        }
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            max-width: 500px;
            margin: 50px auto;
            padding: 20px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            border-radius: 10px;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
        }
        .contador-container {
            background: white;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        .numero {
            font-size: 48px;
            font-weight: bold;
            color: var(--color-zero);
            text-align: center;
            margin: 20px 0;
        }
        .positivo { color: var(--color-up); }
        .negativo { color: var(--color-down); }
        .botones { display: flex; gap: 10px; margin-bottom: 20px; }
        button { flex: 1; padding: 12px; font-size: 16px; border: none; border-radius: 5px; cursor: pointer; font-weight: bold; }
        .btn-decrementar { background-color: #e74c3c; color: white; }
        .btn-incrementar { background-color: #2ecc71; color: white; }
        .btn-reiniciar { width: 100%; background-color: #95a5a6; color: white; }
        .info { text-align: center; color: #7f8c8d; font-size: 14px; margin-top: 20px; }
    </style>
</head>
<body>
    <h1>Contador Interactivo</h1>
    <div class="contador-container">
        <div class="numero" id="contador">0</div>
        <div class="botones">
            <button class="btn-decrementar" id="btnDecrementar">Decrementar</button>
            <button class="btn-incrementar" id="btnIncrementar">Incrementar</button>
        </div>
        <button class="btn-reiniciar" id="btnReiniciar">Reiniciar</button>
        <div class="info">
            <p>Haz clic en los botones para cambiar el número</p>
        </div>
    </div>
</body>
</html>
```

Y en `contador.js`:

```javascript
let contador = Number(localStorage.getItem('contador')) || 0;
const elementoContador = document.getElementById('contador');
const btnIncrementar = document.getElementById('btnIncrementar');
const btnDecrementar = document.getElementById('btnDecrementar');
const btnReiniciar = document.getElementById('btnReiniciar');

function actualizarPantalla() {
elementoContador.textContent = contador;
elementoContador.className = 'numero';
if (contador > 0) elementoContador.classList.add('positivo');
else if (contador < 0) elementoContador.classList.add('negativo');
localStorage.setItem('contador', contador);
}

btnIncrementar.addEventListener('click', () => {
contador++;
actualizarPantalla();
});
btnDecrementar.addEventListener('click', () => {
contador--;
actualizarPantalla();
});
btnReiniciar.addEventListener('click', () => {
contador = 0;
actualizarPantalla();
});

actualizarPantalla();

```

Este ejemplo integra estructura (HTML), presentación (CSS y variables), lógica y persistencia de estado (JS moderno + `localStorage`).

***

### Resumen del Capítulo

La trinidad frontend sigue vigente, pero sus buenas prácticas han evolucionado:\
**HTML** estructura el contenido semánticamente.\
**CSS** define estilos, layouts y temas, usando variables modernas.\
**JavaScript** añade lógica, interactividad y manipula tanto el DOM como las variables CSS; además, a día de hoy se usa casi siempre con `type="module"` para organizar el código y aprovechar los módulos nativos de ECMAScript.

***

#### 💡 Conceptos clave 2025

* **HTML** = Estructura y semántica
* **CSS** = Presentación visual, responsividad, variables
* **JavaScript** = Interactividad y lógica modular
* **Mejor práctica**: siempre que puedas, usa `<script type="module">`
* **Flujo de carga**: los scripts módulo modernos no bloquean el render
* **Manipulación DOM + CSS**: prioriza clases CSS y variables sobre estilos inline

#### 🤔 Preguntas de reflexión

1. ¿Por qué hoy se prefiere usar `type="module"` al cargar JavaScript?
2. ¿Qué ventajas aporta diseñar estilos con clases y variables frente a estilos “en línea”?
3. ¿Qué sucede si accedes a un elemento HTML desde JS antes de parsear el DOM?
4. ¿Cómo limitarías el rango del contador para evitar valores extremos?
5. ¿Cómo lograrías que el valor del contador no se pierda tras recargar la página?
