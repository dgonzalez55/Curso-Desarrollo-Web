# Elementos estructurales típicos

### Cabeceras: `<`<mark style="color:green;">`header`</mark>`>`

Este elemento define la cabecera introductoria de la página completa o la de sus elementos individuales como secciones, artículos, barras de navegación, paneles laterales, etc. Normalmente, contiene el nombre del sitio, su logo y la barra de navegación. Al tratarse de una cabecera se requiere que aparezca al principio de la página o del elemento que la contiene.

```html
 <body>
   <header>
     <h1>FPdeInformatica.es</h1>
   </header>
   ...
</body>
```

### Pies de página: `<`<mark style="color:green;">`footer`</mark>`>`

Este elemento define el pie de la página completa o la de sus elementos individuales como secciones, artículos, etc. Normalmente, contiene información sobre el autor, los derechos de propiedad intelectual e información de contacto. Puede contener también menús de navegación.

```html
<body>
  ...
  <footer>
    <p>Written by: David LeGon</p>
    <p>Información de contacto: <a href="mailto:dgonzalez@educem.com">dgonzalez@educem.com</a>.</p>
  </footer>
<body>
```

### Menús de navegación: `<`<mark style="color:green;">`nav`</mark>`>`

Este elemento contiene los enlaces de navegación de la página o portal web. Aunque lo habitual es encontrar un único menú de navegación, pueden añadirse tantos como sea necesario así como ubicarse dentro de distintos constructos, ya sean cabeceras, pies de página u otros.

```html
<body>
...
  <nav>
    <!-- Lista no numerada para organizar el menú -->
    <ul>
      <li><a href="#start">Inicio</a></li>
      <li><a href="#users">Opiniones</a></li>
      <li><a href="#about">Acerca de</a></li>
    </ul>
  </nav>
...
</body>
```

### Contenido Principal: `<`<mark style="color:green;">`main`</mark>`>`

Este elemento define una estructura que contiene el contenido principal del documento y por tanto el tema central de la página. Su propósito principal es facilitar la accesibilidad, ya que ayuda a que los screen readers y otras tecnologías asistenciales a que puedan identificar donde comienza el contenido principal de la página y donde termina. Una característica importante a tener en cuenta es que puede ser usado una sola vez por página.

Además debe considerarse que este elemento no puede encontrarse dentro de ninguna de las siguientes etiquetas: **<**<mark style="color:green;">**header**</mark>**>, <**<mark style="color:green;">**nav**</mark>**>, <**<mark style="color:green;">**article**</mark>**>, <**<mark style="color:green;">**section**</mark>**>, <**<mark style="color:green;">**aside**</mark>**> y <**<mark style="color:green;">**footer**</mark>**>**.

```html
<body>
...
  <main>
    <p>Contenido principal</p>
  </main>
...
</body>
```

### Artículos y Secciones: `<`<mark style="color:green;">`article`</mark>`>` y `<`<mark style="color:green;">`section`</mark>`>`

Mientras que la etiqueta `<`<mark style="color:green;">**`article`**</mark>`>` representa un artículo independiente, como el artículo de una revista, una entrada de un blog, un documento independiente, etc. la etiqueta `<`<mark style="color:green;">**`section`**</mark>`>` define una sección genérica, utilizada habitualmente para separar contenido temático, o para generar columnas o bloques que ayuden a organizar el contenido principal. Esto implica que si sacáramos un artículo fuera de la web, éste continuaría teniendo sentido, pues se trata de una estructura de datos independiente. Por el contrario, las secciones están estrechamente vinculadas al contexto y fuera de éste pierden total o parcialmente su significado. Habitualmente las secciones se encuentran contenidas en artículos u otras estructuras organizativas.

```html
<body>
...
  <article>
    <header>
      <h2>CES 2019</h2>
      <h3>Muestra de tecnología y electrónica de consumo</h3>
    </header>
    <section>
      <h4>Llegar allí</h4>
      <p>Realmente me fue complicado llegar a la feria dado el colapso del tráfico, así que a mitad de trayecto me bajé del taxi y continué a pie</p>
    </section>
    <section>
      <h4>Conferencias</h4>
      <p>Me apunté a varias conferencias el primer día, especialmente aquellas relacionadas con los equipos de...</p>
    </section>
    <footer>
      <p>Artículo escrito por maese LeGon</p>
    </footer>
  </article>
...
</body>
```

### Contenido Auxiliar / Paneles laterales: `<`<mark style="color:green;">`aside`</mark>`>`

Este elemento delimita un bloque que contiene información relacionada con el contenido principal pero que no es parte del mismo, como referencias a artículos o enlaces que apuntan a publicaciones anteriores. Habitualmente se utiliza para la creación de paneles laterales o _sidebars_.

```html
<body>
...
  <p>Algernon's flat is luxuriously and artistically furnished</p>
  <aside>
    <h3>Algernon Moncrieff</h3>
    <p>A wealthy bachelor who lives in a fashionable part of London. He has a good sense of humor and utter lack of respect for society.</p>
  </aside>
...
</body>
```

### Bloque Genérico: `<`<mark style="color:green;">`div`</mark>`>`

Este elemento define un bloque genérico y se utiliza cuando ningua de las demás etiquetas estructurales es adecuada para dicho contexto. De hecho se trata de una de las etiquetas más utilizadas en HTML ya que su uso es fundamental para la aplicación de estilos y reglas CSS a bloques genéricos de información.

```html
<body>
...
  <div>
    <p>Aquí dentro puede aparecer cualquier cosa</p>
  </div>
...
</body>
```
