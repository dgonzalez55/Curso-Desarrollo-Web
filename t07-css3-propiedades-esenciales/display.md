# Display

La propiedad <mark style="color:blue;">**`display`**</mark> permite especificar como se debe comportar el renderizado del elemento seleccionado. Esencialmente nos permite convertir elementos **inline** en elementos **block** y viceversa.

\
Su sintaxis es la siguiente:

```css
/* Convierte el elemento en un elemento de tipo block */
display: block;

/* Convierte el elemento en un elemento de tipo inline */
display: inline;

/* Convierte el elemento en un elemento de tipo inline-block */
display: inline-block;

/* Convierte el elemento en un elemento de tipo block dentro del modelo de layout Flexbox */
display: flex;

/* Convierte el elemento en un elemento de tipo inline dentro del modelo de layout Flexbox */
display: inline-flex;

/* Convierte el elemento en un elemento de tipo block dentro del modelo de layout CSS Grid*/
display: grid;

/* Convierte el elemento en un elemento de tipo inline dentro del modelo de layout CSS Grid */
display: inline-grid;
```

Los elementos de tipo **inline-block** se comportan como elementos de tipo **inline** pero admiten la definición de valores de ancho y alto.

{% hint style="info" %}
Existen muchos más tipos de display, puedes consultar la referencia completa en: [https://developer.mozilla.org/en-US/docs/Web/CSS/display](https://developer.mozilla.org/en-US/docs/Web/CSS/display)
{% endhint %}
