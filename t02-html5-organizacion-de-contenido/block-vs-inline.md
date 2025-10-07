# Block vs Inline

Todo elemento HTML tiene asignado un valor por defecto de visualización en función de su tipo. Según dicho valor podemos clasificar los elementos HTML en dos grandes grupos:

* Elementos de tipo **block**: `<`<mark style="color:green;">**`address`**</mark>`>, <`<mark style="color:green;">**`article`**</mark>`>, <`<mark style="color:green;">**`aside`**</mark>`>, <`<mark style="color:green;">**`blockquote`**</mark>`>, <`<mark style="color:green;">**`canvas`**</mark>`>, <`<mark style="color:green;">**`dd`**</mark>`>, <`<mark style="color:green;">**`div`**</mark>`>, <`<mark style="color:green;">**`dl`**</mark>`>, <`<mark style="color:green;">**`dt`**</mark>`>, <`<mark style="color:green;">**`fieldset`**</mark>`>, <`<mark style="color:green;">**`figcaption`**</mark>`>, <`<mark style="color:green;">**`figure`**</mark>`>, <`<mark style="color:green;">**`footer`**</mark>`>, <`<mark style="color:green;">**`form`**</mark>`>, <`<mark style="color:green;">**`h1`**</mark>`>..<`<mark style="color:green;">**`h6`**</mark>`>, <`<mark style="color:green;">**`header`**</mark>`>, <`<mark style="color:green;">**`hr`**</mark>`>, <`<mark style="color:green;">**`li`**</mark>`>, <`<mark style="color:green;">**`main`**</mark>`>, <`<mark style="color:green;">**`nav`**</mark>`>, <`<mark style="color:green;">**`noscript`**</mark>`>, <`<mark style="color:green;">**`ol`**</mark>`>, <`<mark style="color:green;">**`p`**</mark>`>, <`<mark style="color:green;">**`pre`**</mark>`>, <`<mark style="color:green;">**`section`**</mark>`>, <`<mark style="color:green;">**`table`**</mark>`>, <`<mark style="color:green;">**`tfoot`**</mark>`>, <`<mark style="color:green;">**`ul`**</mark>`>, <`<mark style="color:green;">**`video`**</mark>`>`
* Elementos de tipo **inline**: `<`<mark style="color:green;">**`a`**</mark>`>, <`<mark style="color:green;">**`abbr`**</mark>`>, <`<mark style="color:green;">**`acronym`**</mark>`>, <`<mark style="color:green;">**`b`**</mark>`>, <`<mark style="color:green;">**`bdo`**</mark>`>, <`<mark style="color:green;">**`big`**</mark>`>, <`<mark style="color:green;">**`br`**</mark>`>, <`<mark style="color:green;">**`button`**</mark>`>, <`<mark style="color:green;">**`cite`**</mark>`>, <`<mark style="color:green;">**`code`**</mark>`>, <`<mark style="color:green;">**`dfn`**</mark>`>, <`<mark style="color:green;">**`em`**</mark>`>, <`<mark style="color:green;">**`i`**</mark>`>, <`<mark style="color:green;">**`img`**</mark>`>, <`<mark style="color:green;">**`input`**</mark>`>, <`<mark style="color:green;">**`kbd`**</mark>`>, <`<mark style="color:green;">**`label`**</mark>`>, <`<mark style="color:green;">**`map`**</mark>`>, <`<mark style="color:green;">**`object`**</mark>`>, <`<mark style="color:green;">**`output`**</mark>`>, <`<mark style="color:green;">**`q`**</mark>`>, <`<mark style="color:green;">**`samp`**</mark>`>,<`<mark style="color:green;">**`script`**</mark>`>, <`<mark style="color:green;">**`select`**</mark>`>, <`<mark style="color:green;">**`small`**</mark>`>, <`<mark style="color:green;">**`span`**</mark>`>, <`<mark style="color:green;">**`strong`**</mark>`>, <`<mark style="color:green;">**`sub`**</mark>`>, <`<mark style="color:green;">**`sup`**</mark>`>, <`<mark style="color:green;">**`textarea`**</mark>`>, <`<mark style="color:green;">**`time`**</mark>`>, <`<mark style="color:green;">**`tt`**</mark>`>, <`<mark style="color:green;">**`var`**</mark>`>`

La diferencia reside en que los elementos de tipo **block** no permiten que se alojen otros elementos a su lado, ni a izquierda ni a derecha, es decir reservan el 100% del ancho de la pantalla para ellos mismos, ocupen lo que ocupen, obligando a los elementos colindantes a _apilarse_ debajo de ellos. Por el contrario, los elementos de tipo **inline** si que permiten otros elementos a su lado, siempre y cuando sean de tipo **inline** también. Por esta razón, la mayoría de las etiquetas que alteran o modifican el significado del texto son de tipo **inline**.\
Además, un elemento de tipo **block** puede contener elementos de tipo **inline**, pero no a la inversa.\
Otra diferencia notable es la posibilidad de modificar ciertas propiedades de estilo como el ancho, alto y márgenes que se tratarán en temas posteriores vinculados a CSS3.

```html
 <body>
    ...
    <p>Los párrafos son de tipo bloque</p><p>No obstante las etiquetas de formato como <strong>strong</strong> o <mark>mark</mark> no lo son.</p>
    ...
</body>
```

<figure><img src="../.gitbook/assets/image (23).png" alt=""><figcaption><p>Renderizado del código anterior</p></figcaption></figure>

{% hint style="info" %}
La tipología de un elemento puede ser alterada mediante reglas CSS, es decir podemos convertir un elemento de tipo **block** en tipo **inline** y viceversa.
{% endhint %}

