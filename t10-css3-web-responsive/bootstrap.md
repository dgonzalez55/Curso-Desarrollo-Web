# Bootstrap

### Introducción

**Bootstrap** es la biblioteca de componentes de front-end web más popular del mundo, diseñada para la creación de proyectos **web responsive** en base al paradigma **Mobile First**.\
El **framework de Bootstrap** incluye un completo kit de herramientas de código abierto para desarrollar mediante HTML, CSS y JS.\
\
Para empezar a utilizar **Bootstrap** en nuestra web, bastará con añadir la siguiente hoja de estilos:

```html
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-4bw+/aepP/YC94hEpVNVgiZdgIC5+VKNBQNGCHeKRQN+PtmoHDEXuppvnDJzQIu9" crossorigin="anonymous">
```

Y adicionalmente, las siguientes librerías JavaScript, aunque ello dependa de los componentes que utilicemos de la librería:

```html
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.1/dist/js/bootstrap.bundle.min.js" integrity="sha384-HwwvtgBNo3bZJJLYd8oVXjrBZt8cqVSpeBNS5n7C8IVInixGAoxmnlMuBnhbgrkm" crossorigin="anonymous"></script>
```

En el caso de empezar nuestra web desde 0, podemos optar simplemente por emplear la siguiente plantilla:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-4bw+/aepP/YC94hEpVNVgiZdgIC5+VKNBQNGCHeKRQN+PtmoHDEXuppvnDJzQIu9" crossorigin="anonymous">
    <title>Hello, world!</title>
  </head>
  <body>
    <h1>Hello, world!</h1>
    <!-- Bootstrap JS -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.1/dist/js/bootstrap.bundle.min.js" integrity="sha384-HwwvtgBNo3bZJJLYd8oVXjrBZt8cqVSpeBNS5n7C8IVInixGAoxmnlMuBnhbgrkm" crossorigin="anonymous"></script>
  </body>
</html>
```

Con ello, estaremos listo para usar **Bootstrap**, con la simplicidad que otorga el simple hecho de únicamente tener que añadir clases a nuestros elementos HTML para que estos adquieran una serie de estilos y comportamientos predefinidos sin tener que definir nosotros mismos la gran mayoría de reglas CSS.

{% hint style="info" %}
Consulta la web oficial del proyecto Bootstrap para mayor información: [Web oficial de Bootstrap](https://getbootstrap.com/)
{% endhint %}

### Primeros pasos con Bootstrap

**Bootstrap** es un framework muy extenso y cuyo aprendizaje en profundidad lleva su tiempo pero que puede empezar a utilizarse de manera muy simple mediante el uso de plantillas y temas preconfigurados.\
Esencialmente el framework nos proporciona un conjunto de clases que utilizadas de forma adecuada permiten lograr un acabado profesional sin tener que estar constantemente recurriendo a la definición de reglas CSS. Por ejemplo, si deseamos que nuestro header no tenga <mark style="color:blue;">**`margin`**</mark> pero si algo de <mark style="color:blue;">**`padding`**</mark>bastará con el siguiente código HTML:

```html
<header class="m-0 p-2">...</header>
```

La clase <mark style="color:purple;">**m-0**</mark> que define Bootstrap implica un valor de <mark style="color:blue;">**`margin`**</mark>`=`<mark style="color:orange;">**`0`**</mark>`;`, mientras que la clase <mark style="color:purple;">**p-2**</mark> implica un valor de <mark style="color:blue;">**`padding`**</mark>`=`<mark style="color:orange;">**`0.5rem`**</mark>`;`. De manera análoga existen clases para definir márgenes y rellenos específicos para determinados tamaño de viewport, así como encontramos ya predefinidas todas las clases necesarias para nuestro diseño responsivo basado en una cuadrícula de 12 columnas.

La manera más simple y natural de empezar a familiarizarnos con las clases que nos proporciona bootstrap y sus efectos sobre el diseño es consultando su extensa documentación oficial en: [https://getbootstrap.com/docs/5.3/getting-started/introduction/](https://getbootstrap.com/docs/5.3/getting-started/introduction/).\
Así como descargándonos algunas de las numerosas plantillas y temas gratuitos que podemos encontrar en páginas como: [https://startbootstrap.com](https://startbootstrap.com/).

De hecho, en la propia web del **W3C** encontramos tres temas para Bootstrap en su versión 3:

* [Bootstrap Theme "Simply Me"](https://www.w3schools.com/bootstrap/bootstrap_theme_me.asp)
* [Bootstrap Theme "Company"](https://www.w3schools.com/bootstrap/bootstrap_theme_company.asp)
* [Bootstrap Theme "The Band"](https://www.w3schools.com/bootstrap/bootstrap_theme_band.asp)

{% hint style="info" %}
Bootstrap ofrece también múltiples temas de calidad pero de pago a través de su sitio web oficial: [https://themes.getbootstrap.com](https://themes.getbootstrap.com/)
{% endhint %}
