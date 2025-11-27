# Fondo

### Color

La propiedad <mark style="color:blue;">**`background-color`**</mark> permite establecer el color del fondo del elemento seleccionado.

\
La sintaxis que se sigue es la siguiente:

```css
background-color: color;
```

Naturalmente el valor de color que podemos asignar a la propiedad es el mismo que si se tratará de la propiedad <mark style="color:blue;">**`color`**</mark>.

{% hint style="info" %}
Puedes consultar la lista correspondiente a los colores predefinidos en [https://www.w3schools.com/colors/colors\_names.asp](https://www.w3schools.com/colors/colors_names.asp)
{% endhint %}

### Imagen de Fondo

#### Añadir imagen de fondo

La propiedad <mark style="color:blue;">**`background-image`**</mark> permite especificar una o más imágenes a utilizar de fondo para el elemento seleccionado. Por defecto la imagen se ubicará a partir de la esquina superior izquierda y se repetirá, estilo mosaico, para poder cubrir por completo el elemento. Su sintaxis es la siguiente:

```css
background-image: url("IMAGE-PATH-#1"), url("IMAGE-PATH-#2"), ... url("IMAGE-PATH-#N");
```

Veamos algunos posibles ejemplos de uso:

```css
body {
  /* Se establecen dos imágenes para el fondo de la página web. */
  background-image: url("img_tree.gif"), url("paper.gif");
  /* Se indica un color de fondo para que sea utilizado en caso de que las imágenes de fondo no estén disponibles */
  background-color: #cccccc;
}

#caja {
  /* Se indica la imagen "bgdesert.jpg" ubicada en la carpeta "/img" como imagen de fondo del elemento caja */
  background-image: url("./img/bgdesert.jpg");
}
```

{% hint style="info" %}
El tamaño del fondo de un elemento incluye el margen interior (padding) y el grosor del borde (border)
{% endhint %}

#### Repetir imagen de fondo

La propiedad <mark style="color:blue;">**`background-repeat`**</mark> permite indicar el comportamiento en la repetición de la imagen establecida de fondo.\
A continuación, se enumeran los posibles valores para dicha propiedad:

* <mark style="color:orange;">**`no-repeat`**</mark> : La imagen no se repite y puede que no se cubra la totalidad del fondo.
* <mark style="color:orange;">**`repeat`**</mark> : La imagen se repite vertical y horizontalmente y puede producir que queden imágenes "cortadas". Es el comportamiento por defecto.
* <mark style="color:orange;">**`repeat-x`**</mark> : La imagen se repite únicamente horizontalmente y puede que no se cubra la totalidad del fondo.
* <mark style="color:orange;">**`repeat-y`**</mark> : La imagen se repite únicamente verticalmente y puede que no se cubra la totalidad del fondo.
* <mark style="color:orange;">**`space`**</mark> : La imagen se repite vertical y horizontalmente, pero organizándose mediante espacios en blanco de manera que no queden imágenes "cortadas".
* <mark style="color:orange;">**`round`**</mark> : Idéntico al anterior, pero redimensionando las imágenes en lugar de añadir espacios en blanco.

Veamos algunos posibles ejemplos de uso:

```css
body {
  background-image: url("paper.gif");
  /* La imagen de fondo no se repite */
  background-repeat: no-repeat;
}

#caja {
  background-image: url("./img/bgdesert.jpg");
  /* La imagen de fondo se repite únicamente horizontalmente */
  background-repeat: repeat-x;
}
```

#### Posicionar imagen de fondo

La propiedad <mark style="color:blue;">**`background-position`**</mark> permite indicar el punto de inicio de la imagen establecida de fondo. Por defecto la imagen se posiciona a partir de la esquina superior izquierda. Su sintaxis es la siguiente:

```css
/* valorX: coordenada horizontal, valorY: coordenada vertical */
background-position: valorX valorY;
```

Es posible emplear como valores las palabras reservadas: <mark style="color:orange;">**top**</mark>, <mark style="color:orange;">**right**</mark>, <mark style="color:orange;">**bottom**</mark>, <mark style="color:orange;">**left**</mark> y <mark style="color:orange;">**center**</mark>. En caso de solo indicar un valor, el otro tomará el valor de <mark style="color:orange;">**center**</mark> que se corresponde al valor de 50%.

Veamos algunos posibles ejemplos de uso:

```css
/* Fondo sin repetición centrado horizontalmente y alineado en la posición superior. */
body {
  background-image: url('w3css.gif');
  background-repeat: no-repeat;
  background-position: center top;
}

/* Fondo sin repetición y centrado */
#caja {
  background-image: url("./img/bgdesert.jpg");
  background-repeat: no-repeat;
  background-position: 50% 50%;
}
```

#### Fijar imagen de fondo

La propiedad <mark style="color:blue;">**`background-attachment`**</mark> permite indicar si la imagen establecida como fondo está fijada o debe deslizarse con el scroll de la página. Por defecto la imagen permite el scroll. A continuación, se enumeran los posibles valores para dicha propiedad:

* <mark style="color:orange;">**`scroll`**</mark> : La imagen de fondo se desliza junto con la página (scroll). Es el valor por defecto.
* <mark style="color:orange;">**`fixed`**</mark> : La imagen de fondo no se desliza junto con la página, sino que está fijada su posición de pantalla.
* <mark style="color:orange;">**`local`**</mark> : La imagen de fondo se desliza junto con el contenido del elemento (no de la página).

\
Veamos algunos posibles ejemplos de uso:

```css
/* Fondo sin repetición que se desliza junto con la página. */
body {
  background-image: url("img_tree.gif");
  background-repeat: no-repeat;
  background-attachment: scroll;
}

/* Fondo sin repetición fijado y que por tanto no se desliza. */
#caja {
  /* Fondo sin repetición y centrado */
  background-image: url("./img/bgdesert.jpg");
  background-repeat: no-repeat;
  background-attachment: fixed;
}
```

{% hint style="info" %}
Existe un efecto muy utilizado en la maquetación web que resulta muy vistoso y que se conoce como efecto **parallax**. Dicho efecto crea una ilusión de profundidad 3D gracias a fijar un fondo de imagen a su contenedor, generalmente una sección o apartado de la web. Al realizarse scroll sobre la página, el contenedor se desliza con la página y dado que la imagen de su fondo está fijada, da la sensación de que el fondo se mueve en sentido opuesto.
{% endhint %}

#### Redimensionar imagen de fondo

La propiedad <mark style="color:blue;">**`background-size`**</mark> permite indicar el tamaño de la imagen empleada como fondo. Por defecto la imagen se muestra en su tamaño original (valor <mark style="color:orange;">**`auto`**</mark>). A continuación, se enumeran las palabras clave que se pueden emplear como valores de dicha propiedad:

* <mark style="color:orange;">**`auto`**</mark> : La imagen de fondo se muestra en su tamaño original. Es el valor por defecto.
* <mark style="color:orange;">**`cover`**</mark> : La imagen de fondo se redimensiona para ocupar todo el elemento contenedor, incluso si ello implica que la imagen se corte. <mark style="background-color:yellow;">**Mantiene el**</mark><mark style="background-color:yellow;">**&#x20;**</mark>_<mark style="background-color:yellow;">**aspect ratio**</mark>_<mark style="background-color:yellow;">**.**</mark>
* <mark style="color:orange;">**`contain`**</mark> : La imagen de fondo se redimensiona para garantizar que es completamente visible, aunque ello implique no rellenar todo el elemento contenedor. <mark style="background-color:yellow;">**Mantiene el**</mark><mark style="background-color:yellow;">**&#x20;**</mark>_<mark style="background-color:yellow;">**aspect ratio**</mark>_<mark style="background-color:yellow;">**.**</mark>

Adicionalmente su sintaxis permite especificar su tamaño de manera precisa mediante valores numéricos:

```css
/* Si solo se indica el valorAncho, se considera el valorAlto = auto */
background-size: valorAncho valorAlto;
```

Veamos algunos posibles ejemplos de uso:

```css
/* Fondo redimensionado para cubrir la totalidad de la página y sin necesidad de mantener el aspect ratio (se verá la imagen completa) */
body {
  background-image: url("img_tree.gif");
  background-repeat: no-repeat;
  background-size: 100% 100%;
}

/* Fondo redimensionado para cubrir la totalidad del contenedor manteniendo su aspect ratio, aunque puede que no se vea completamente */
#caja {
  background-image: url("./img/bgdesert.jpg");
  background-repeat: no-repeat;
  background-size: cover;
}
```

### Método abreviado: <mark style="color:blue;">**`background`**</mark>

La propiedad <mark style="color:blue;">**`background`**</mark> es un método abreviado que permite establecer el **color**, **imagen**, **repetición**, **fijación** y **posición** del fondo del elemento seleccionado mediante una única asignación.\
El color se corresponde con la propiedad <mark style="color:blue;">**`background-color`**</mark>, la imagen con la propiedad <mark style="color:blue;">**`background-image`**</mark>, la repetición con la propiedad <mark style="color:blue;">**`background-repeat`**</mark>, la fijación con la propiedad <mark style="color:blue;">**`background-attachment`**</mark> y la posición con la propiedad <mark style="color:blue;">**`background-position`**</mark>.<br>

Su sintaxis es la siguiente:

```css
background: color image repeat attachment position;
```

No importa si alguno de los valores de las respectivas propiedades no aparezca, siempre y cuando se mantenga el orden indicado. A continuación, se presentan algunos ejemplos de uso:

```css
/* Fondo de imagen con color de respaldo, sin repetición, centrado y fijado */
body {
  background: #ffffff url("cabra.jpg") no-repeat fixed center;
}
/* Fondo de imagen con repetición (x e y) y scroll, centrado en su límite inferior */
div {
  background: url("vaca.png") bottom center;
}
```
