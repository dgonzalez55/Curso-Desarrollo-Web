# Texto

### Color

La propiedad <mark style="color:blue;">**`color`**</mark> permite establecer el color del texto.\
Es posible asignar el valor de color de múltiples formas, incluyendo la posibilidad de indicar el nivel de transparencia (canal _alpha_). A continuación, se muestran a modo de ejemplo las más relevantes:

<pre class="language-css"><code class="lang-css"><strong>/* Color mediante palabras clave reservadas */
</strong>h1 {
  color: red;
}
/* Color mediante notación hexadecimal (RGB) */
h2 {
  color: #123456;
}
/* Color mediante función rgb y valores decimales */
p {
  color: rgb(24,115,34);
}
/* Color con canal alpha mediante función rgba y valores decimales.
   El valor alpha va de 0 (transparente) a 1 (opaco).
*/
p span {
  color: rgba(0,0,0,0.25);
}
</code></pre>

### Tipografía

La propiedad <mark style="color:blue;">**`font-family`**</mark> permite establecer tipografía de la fuente del texto.\
Es posible indicar varias fuentes, de manera que si la primera indicada no estubiese disponible en el sistema, se utilizase la siguiente de la lista. La sintaxis que se sigue es la siguiente:

```css
font-family: [font1], [font2], [font3], ... ;
```

A continuación, mostramos algunos ejemplos de uso:

```css
/* Indicamos que la fuente a utilizar debe ser de la familia "serif" */
h1 {
  font-family: serif;
}
/* Indicamos que debe utilizarse una fuente "Arial", si no fuese posible "Times New Roman" y sino alguna de la familia "sans-serif" */
a {
  font-family: Arial, "Times New Roman", sans-serif;
}
/* Indicamos que la fuente a utilizar debe ser de la familia "monospace" como la "Courier New" */
p {
  font-family: monospace;
}
```

### Tamaño

La propiedad <mark style="color:blue;">**`font-size`**</mark> permite establecer el tamaño del texto.\
Es posible indicar el tamaño en unidades relativas o absolutas:

* Para indicar el tamaño en unidades absolutas se utilizan las siguientes palabras clave ordenadas de menor a mayor tamaño: <mark style="background-color:yellow;">**xx-small**</mark>, <mark style="background-color:yellow;">**x-small**</mark>, <mark style="background-color:yellow;">**small**</mark>, <mark style="background-color:yellow;">**medium**</mark>, <mark style="background-color:yellow;">**large**</mark>, <mark style="background-color:yellow;">**x-large**</mark>, <mark style="background-color:yellow;">**xx-large**</mark>. También puede emplearse como es lógico una unidad de tamaño absoluto como _<mark style="color:purple;">**px**</mark>_, _<mark style="color:purple;">**cm**</mark>_, ...
* Para indicar el tamaño del texto en unidades relativas se pueden utilizar las siguientes palabras clave: <mark style="background-color:yellow;">**smaller**</mark> y <mark style="background-color:yellow;">**larger**</mark>, cuyo efecto es reducir o ampliar el tamaño de la fuente en cuestión respecto la su elemento _padre_ (contenedor). Trabajando en unidades de tamaño relativas también es posible emplear un <mark style="color:purple;">**%**</mark> para indicar el porcentaje exacto de tamaño respecto el elemento _padre_, o usar unidades como _<mark style="color:purple;">**em**</mark>_.

A continuación, mostramos algunos ejemplos de uso:

```css
/* Indicamos un tamaño de fuente extra-exta grande */
h1 {
  font-size: xx-large;
}
/* Indicamos que el tamaño de la fuente del anchor debe ser menor que el del elemento contenedor */
a {
  font-size: smaller;
}
/* Indicamos que el tamaño de la fuente es un 125% respecto el tamaño de la fuente del elemento contenedor */
p {
  font-size: 125%;
}
/* Indicamos que el tamaño de la fuente es de 15 píxeles */
p span {
  font-size: 15px;
}
```

### Grosor

La propiedad <mark style="color:blue;">**`font-weight`**</mark> permite establecer el grosor de la fuente del texto. Es posible indicar el grosor mediante las siguientes palabras clave ordenadas de menor a mayor grosor: <mark style="background-color:yellow;">**lighter**</mark>, <mark style="background-color:yellow;">**normal**</mark>, <mark style="background-color:yellow;">**bold**</mark>, <mark style="background-color:yellow;">**bolder**</mark>. También se puede graduar el grosor mediante una escala de valores numéricos del **100** al **900**, siendo 100 el valor del trazo más fino y 900 el valor para el trazo más grueso.

A continuación, mostramos algunos ejemplos de uso:

```css
/* Indicamos un grosor normal (por defecto) */
h1 {
  font-weight: normal;
}
/* Indicamos un grosor de negrita */
a {
  font-weight: bold;
}
/* Indicamos el mínimo grosor posible. */
p {
  font-weight: 100;
}
```

### Estilo

La propiedad <mark style="color:blue;">**`font-style`**</mark> permite establecer el estilo de la fuente del texto. Es posible indicar hasta tres estilos diferentes con las palabras clave: <mark style="background-color:yellow;">**normal**</mark>, <mark style="background-color:yellow;">**italic**</mark> y <mark style="background-color:yellow;">**oblique**</mark>.

A continuación, mostramos algunos ejemplos de uso:

```css
/* Indicamos un estilo normal (por defecto) */
h1 {
  font-style: normal;
}
/* Indicamos un estilo de cursiva */
a {
  font-style: italic;
}
/* Indicamos un estilo similar a cursiva pero más pronunciado. */
p {
  font-style: oblique;
}
```

### Método abreviado: <mark style="color:blue;">**`font`**</mark>

La propiedad <mark style="color:blue;">**`font`**</mark> es un método abreviado que permite establecer la **tipografía**, **tamaño**, **estilo** y **grosor** de la fuente del elemento seleccionado mediante una única asignación.\
La tipografía se corresponde con la propiedad <mark style="color:blue;">**`font-family`**</mark>, el tamaño con la propiedad <mark style="color:blue;">**`font-size`**</mark>, el estilo con la propiedad <mark style="color:blue;">**`font-style`**</mark> y el grosor con la propiedad <mark style="color:blue;">**`font-weight`**</mark>.\
Su sintaxis es la siguiente:

```css
font: estilo grosor tamaño tipografía;
```

A continuación, se presentan algunos ejemplos de uso:

```css
/* Fuente Courier New, negrita y extra extra grande */
h1 {
  font: bold xx-large "Courier New", monospace;
}
/* Fuente Times New Roman en cursiva y tamaño pequeño */
p {
  font: italic normal small "Times New Roman", sans-serif;
}
```

### Decoración

La propiedad <mark style="color:blue;">**`text-decoration`**</mark> permite establecer la decoración del texto del elemento mediante una línea de: subrayado, tachado, etc. Es en realidad un método abreviado de las propiedades <mark style="color:blue;">**`text-decoration-line`**</mark>, <mark style="color:blue;">**`text-decoration-color`**</mark> y <mark style="color:blue;">**`text-decoration-style`**</mark>. A diferencia de otros métodos abreviados, el uso de esta propiedad obliga a indicar como mínimo el valor para <mark style="color:blue;">**`text-decoration-line`**</mark>, pues el resto no tendrían sentido por sí solos.\
Su sintaxis es:

```css
text-decoration: text-decoration-line text-decoration-color text-decoration-style
```

Los posibles valores para <mark style="color:blue;">**`text-decoration-line`**</mark> son:

* <mark style="color:orange;">**`none`**</mark> : Sin línea de decoración. Valor por defecto.
* <mark style="color:orange;">**`underline`**</mark> : Subrayado.
* <mark style="color:orange;">**`overline`**</mark> : _Subrayado superior_.
* <mark style="color:orange;">**`line-through`**</mark> : Tachado.

\
Los posibles valores para <mark style="color:blue;">**`text-decoration-color`**</mark>, como resulta lógico, pasan por el uso de cualquier color CSS.\
\
Los posibles valores para <mark style="color:blue;">**`text-decoration-style`**</mark> son:

* <mark style="color:orange;">**`double`**</mark> : Se muestra una línea doble de decoración.
* <mark style="color:orange;">**`dotted`**</mark> : Se muestra una línea de decoración elaborada mediante puntos.
* <mark style="color:orange;">**`dashed`**</mark> : Se muestra una línea de decoración elaborada mediante guíones.
* <mark style="color:orange;">**`wavy`**</mark> : Se muestra una línea de decoración elaborada mediante una ondulación.
* <mark style="color:orange;">**`solid`**</mark> : Se muestra una única línea de decoración. Valor por defecto.

\
Cabe señalar que es posible indicar más de una línea de decoración para un mismo elemento.\
Veamos ahora algunos ejemplos de uso:

```css
h1 {
  text-decoration: underline red wavy;
}

h2 {
  text-decoration: line-through dotted;
}

h3 {
  text-decoration: underline blue double;
}

h4 {
  text-decoration: underline overline;
}
```

{% hint style="warning" %}
Esta propiedad habitualmente se usa para eliminar la decoración que por defecto los navegadores añaden a los hiperenlaces. Para hacerlo, basta con indicar <mark style="color:blue;">**text-decoration**</mark>: <mark style="color:orange;">**none**</mark>;
{% endhint %}

### Transformación

La propiedad <mark style="color:blue;">**`text-transform`**</mark> permite establecer algunas transformaciones de mayúsculas-minúsculas al texto del elemento seleccionado.\
Las palabras reservadas que se admiten como posibles valores para la propiedad son:

* <mark style="color:orange;">**`uppercase`**</mark> : Transforma todos los caracteres del texto a mayúsculas.
* <mark style="color:orange;">**`lowercase`**</mark> : Transforma todos los caracteres del texto a minúsculas.
* <mark style="color:orange;">**`capitalize`**</mark> : Transforma el primer caracter de cada palabra a mayúsculas.
* <mark style="color:orange;">**`none`**</mark> : Sin transformación alguna.

Veamos algunos ejemplos de uso:

```css
div.a {
  text-transform: uppercase;
}

div.b {
  text-transform: lowercase;
}

div.c {
  text-transform: capitalize;
}
```
