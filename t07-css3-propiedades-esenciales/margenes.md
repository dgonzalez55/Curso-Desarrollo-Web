# Márgenes

### Margen Interior

La propiedad <mark style="color:blue;">**`padding`**</mark> permite especificar el margen interior del elemento seleccionado, es decir, la distancia entre su contenido y su borde. Si se especifica su valor en **%**, dicho porcentaje es relativo al ancho del elemento contenedor. El <mark style="color:blue;">**`padding`**</mark> en los elementos de tipo **inline** desplaza los elementos adyacentes siempre que sea horizontal, mientras que si es vertical, no tiene ningún efecto de desplazamiento, pero puede suponer que el elemento sobrepase su contenedor (overflow). Para los elementos de tipo **block** e **inline-block**, ocasiona desplazamientos tanto en horizontal como en vertical.

\
Su sintaxis es la siguiente:

```css
/* Mismo margen interno para los 4 costados (superior, derecho, inferior, izquierdo) */
padding: size;

/* Margen interno diferenciado para los costados laterales y los superiores e inferiores */
padding: sizeVertical sizeLateral;

/* Margen interno diferenciado para cada uno de sus 4 costados */
padding: sizeTop sizeRight sizeBottom sizeLeft;

/* Margenes interiores diferenciados e indicados explícitamente */
padding-top: size;
padding-right: size;
padding-bottom: size;
padding-left: size;
```

Como se ha visto, las propiedades <mark style="color:blue;">**`width`**</mark> y <mark style="color:blue;">**`height`**</mark> no incluyen en su valor la suma de los tamaños del <mark style="color:blue;">**`padding`**</mark> ni del <mark style="color:blue;">**`border`**</mark>. Ello implica que si tenemos el siguiente código CSS:

```css
div {
  width: 200px;
  padding: 25px;
}
```

El ancho del elemento no sea de 200 píxeles como se podría pensar, sino de 250 píxeles (2 margenes internos laterales de 25 píxeles + 0 píxeles de borde). Para poder establecer mediante las las propiedades <mark style="color:blue;">**`width`**</mark> y <mark style="color:blue;">**`height`**</mark> unos valores que ya incluyan los márgenes interiores y el grosor del borde, es necesario añadir al elemento seleccionado la propiedad <mark style="color:blue;">**`box-sizing`**</mark> con valor <mark style="color:orange;">**`border-box`**</mark>.

```css
box-sizing: border-box;
```

Retomando el ejemplo anterior, si deseamos indicar que los elementos `<`<mark style="color:green;">**`div`**</mark>`>` tiene un ancho de 200 píxeles incluyendo márgenes internos y bordes, lo podríamos hacer así:

<pre class="language-css"><code class="lang-css"><strong>div {
</strong>  width: 200px;
  padding: 25px;
  box-sizing: border-box;
}
</code></pre>

El valor por defecto de la propiedad <mark style="color:blue;">**`box-sizing`**</mark> es: <mark style="color:orange;">**`content-box`**</mark>.

### Margen exterior

La propiedad <mark style="color:blue;">**`margin`**</mark> permite especificar el margen externo del elemento seleccionado, es decir, la distancia entre su borde y el resto de elementos adyacentes. Si se especifica su valor en **%**, dicho porcentaje es relativo al ancho del elemento contenedor. El <mark style="color:blue;">**`margin`**</mark> en los elementos de tipo **inline** desplaza los elementos adyacentes siempre que sea horizontal, mientras que si es vertical, no tiene ningún efecto de desplazamiento. Para los elementos de tipo **block** e **inline-block**, ocasiona desplazamientos tanto en horizontal como en vertical.\
Su sintaxis es la siguiente:

```css
/* Mismo margen externo para los 4 costados (superior, derecho, inferior, izquierdo) */
margin: size;

/* Margen externo diferenciado para los costados laterales y los superiores e inferiores */
margin: sizeVertical sizeLateral;

/* Margen externo diferenciado para cada uno de sus 4 costados */
margin: sizeTop sizeRight sizeBottom sizeLeft;

/* Márgenes externos diferenciados e indicados explícitamente */
margin-top: size;
margin-right: size;
margin-bottom: size;
margin-left: size;
```

Es posible indicar como valor de <mark style="color:blue;">**`margin`**</mark> la palabra clave <mark style="color:orange;">**`auto`**</mark>, en cuyo caso, el elemento seleccionado se centrará horizontalmente respecto de su elemento contenedor.

{% hint style="danger" %}
Los márgenes inferior y superior de los elementos **block** adyacentes pueden colapsar en un único margen correspondiente al valor más elevado entre el margen inferior del elemento antecesor y el margen superior del elemento predecesor.
{% endhint %}
