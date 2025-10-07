# Media Queries

**CSS3 Media Query** es la clave para un diseño **web responsive**. Las **Media Queries** le dicen al navegador como renderizar la página para determinados anchos del _viewport_.\
Por ejemplo, el siguiente código CSS le dice al navegador que el fondo del _body_ debe ponerse en color rojo para anchos de pantalla iguales o inferiores a 600 píxeles (smartphones):

```css
@media only screen and (max-width: 600px) {
  body {
    background-color: red;
  }
}
```

Así pues, para un diseño **web responsive** adecuado, deberemos añadir puntos de ruptura com el del ejemplo, que nos permitan alterar el comportamiento de nuestra web en función del tamaño de pantalla del dispositivo de navegación empleado. Aunque podemos definir los puntos de ruptura que nos plazcan, típicamente se emplean los siguientes:

```css
/* Extra small devices (phones, 600px and down) */
@media only screen and (max-width: 600px) {...}

/* Small devices (portrait tablets and large phones, 600px and up) */
@media only screen and (min-width: 600px) {...}

/* Medium devices (landscape tablets, 768px and up) */
@media only screen and (min-width: 768px) {...}

/* Large devices (laptops/desktops, 992px and up) */
@media only screen and (min-width: 992px) {...}

/* Extra large devices (large laptops and desktops, 1200px and up) */
@media only screen and (min-width: 1200px) {...}
```

Dentro de estos puntos de ruptura, deberemos definir nuestras clases de cuadrícula responsiva, a fin de establecer diferentes distribuciones de columnas en función del tamaño de la pantalla:

```css
/* Mobile First --> Default columns */
.col-1 {width: 8.33%;}
.col-2 {width: 16.66%;}
.col-3 {width: 25%;}
.col-4 {width: 33.33%;}
.col-5 {width: 41.66%;}
.col-6 {width: 50%;}
.col-7 {width: 58.33%;}
.col-8 {width: 66.66%;}
.col-9 {width: 75%;}
.col-10 {width: 83.33%;}
.col-11 {width: 91.66%;}
.col-12 {width: 100%;}

/* Small devices (portrait tablets and large phones, 600px and up) */
@media only screen and (min-width: 600px) {
  .col-sm-1 {width: 8.33%;}
  .col-sm-2 {width: 16.66%;}
  .col-sm-3 {width: 25%;}
  .col-sm-4 {width: 33.33%;}
  .col-sm-5 {width: 41.66%;}
  .col-sm-6 {width: 50%;}
  .col-sm-7 {width: 58.33%;}
  .col-sm-8 {width: 66.66%;}
  .col-sm-9 {width: 75%;}
  .col-sm-10 {width: 83.33%;}
  .col-sm-11 {width: 91.66%;}
  .col-sm-12 {width: 100%;}
}

/* Medium devices (landscape tablets, 768px and up) */
@media only screen and (min-width: 768px) {
  .col-md-1 {width: 8.33%;}
  .col-md-2 {width: 16.66%;}
  .col-md-3 {width: 25%;}
  .col-md-4 {width: 33.33%;}
  .col-md-5 {width: 41.66%;}
  .col-md-6 {width: 50%;}
  .col-md-7 {width: 58.33%;}
  .col-md-8 {width: 66.66%;}
  .col-md-9 {width: 75%;}
  .col-md-10 {width: 83.33%;}
  .col-md-11 {width: 91.66%;}
  .col-md-12 {width: 100%;}
}

/* Large devices (laptops/desktops, 992px and up) */
@media only screen and (min-width: 992px) {
  .col-lg-1 {width: 8.33%;}
  .col-lg-2 {width: 16.66%;}
  .col-lg-3 {width: 25%;}
  .col-lg-4 {width: 33.33%;}
  .col-lg-5 {width: 41.66%;}
  .col-lg-6 {width: 50%;}
  .col-lg-7 {width: 58.33%;}
  .col-lg-8 {width: 66.66%;}
  .col-lg-9 {width: 75%;}
  .col-lg-10 {width: 83.33%;}
  .col-lg-11 {width: 91.66%;}
  .col-lg-12 {width: 100%;}
}

/* Extra large devices (large laptops and desktops, 1200px and up) */
@media only screen and (min-width: 1200px) {
  .col-xl-1 {width: 8.33%;}
  .col-xl-2 {width: 16.66%;}
  .col-xl-3 {width: 25%;}
  .col-xl-4 {width: 33.33%;}
  .col-xl-5 {width: 41.66%;}
  .col-xl-6 {width: 50%;}
  .col-xl-7 {width: 58.33%;}
  .col-xl-8 {width: 66.66%;}
  .col-xl-9 {width: 75%;}
  .col-xl-10 {width: 83.33%;}
  .col-xl-11 {width: 91.66%;}
  .col-xl-12 {width: 100%;}
}
```

De esta forma, podríamos definir un layout adaptativo, en función si el dispositivo es un equipo de sobremesa, tablet o smartphone como el siguiente:

```html
    <!-- En este ejemplo no se requiere el empleo de contenedores <div class="row">, dado que todas las filas ocupan el 100% del ancho de la pantalla -->
    <!-- La cabecera siempre ocupa el 100% del ancho del viewport con independencia del tamaño de pantalla -->
    <header class="col-12">CABECERA</header>
    <!-- La primera sección lateral ocupa el 100% de la pantalla para dispositivos smartphone, 3 columnas en las tablets y 2 columnas en equipos de sobremesa -->
    <aside class="col-12 col-md-3 col-lg-2">LAT. 1</aside>
    <!-- La sección principal ocupa el 100% de la pantalla para dispositivos smartphone, 6 columnas en las tablets y 8 columnas en equipos de sobremesa -->
    <main class="col-12 col-md-6 col-lg-8">PRINCIPAL</main>
    <!-- La segunda sección lateral ocupa el 100% de la pantalla para dispositivos smartphone, 3 columnas en las tablets y 2 columnas en equipos de sobremesa -->
    <aside class="col-12 col-md-3 col-lg-2">LAT. 2</aside>
    <!-- El footer siempre ocupa el 100% del ancho del viewport con independencia del tamaño de pantalla -->
    <footer class="col-12">PIE</footer>
```

Las **Media Queries** también se pueden usar para cambiar el diseño de una página dependiendo de la orientación del navegador (especialmente útil para el caso de las tablets y smartphones). Así es posible tener un conjunto de propiedades CSS que solo se aplicarán cuando la ventana del navegador sea más ancha que su altura, lo que se denomina una orientación **landscape**. Veamos un ejemplo de cómo deberíamos definir los **Media Queries**:

```css
/* El color de fondo del body se pinta de color azul siempre que el ancho de la ventana sea superior a su altura */
@media only screen and (orientation: landscape) {
  body {
    background-color: blue;
  }
}
```

Para finalizar, comentar que si en nuestras **Media Queries** indicamos <mark style="color:blue;">**`min-device-width`**</mark> en lugar de <mark style="color:blue;">**`min-width`**</mark> o <mark style="color:blue;">**`max-device-width`**</mark> en lugar <mark style="color:blue;">**`max-width`**</mark>, se usará para la regla CSS el tamaño de pantalla del dispositivo con independencia del tamaño que en esos momentos muestre la pantalla del navegador. Lo normal no obstante es utilizar el tamaño de la ventana del navegador y no la del dispositivo.
