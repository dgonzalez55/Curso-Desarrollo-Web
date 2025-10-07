# Sintaxis Reglas CSS

La sintaxis de las reglas CSS es muy simple y obedece al siguiente esquema:

```css
selector {propiedad: valor;}
```

Los tres elementos básicos que conforman una regla CSS son:

* **Selector**: Indica a qué elemento o conjunto de elementos se deben aplicar las reglas CSS que contiene en su interior.
* **Propiedad**: Es la palabra clave que define la propiedad o cualidad cuya presentación deseamos alterar. Existen un conjunto finito de propiedades que podemos consultar en la [referencia oficial del W3C](https://www.w3.org/Style/CSS/all-properties.en.html)
* **Valor**: El valor que debe tomar la propiedad en cuestión.

Un fichero CSS se constituye así pues por un conjunto ordenado de reglas CSS.

```css
/* Esto sería un comentario en CSS */
  selector1 {
    propiedad1: valor1;
    propiedad2: valor2;
    ...
    propiedadN: valorN;
  }
  selector2 {
    propiedad1: valor1;
    propiedad2: valor2;
    ...
    propiedadN: valorN;
  }
   ...
  selectorN {
    propiedad1: valor1;
    propiedad2: valor2;
    ... 
    propiedadN: valorN;
  }
```

Sirva el siguiente código a modo de ejemplo de hoja de estilo en la que aplicaríamos negrita y cursiva al texto de todos los párrafos (`<`<mark style="color:green;">**`p`**</mark>`>`) del documento:

```css
p {
  font-weight: bold;
  font-style: italic;
}
```

Suponiendo que las anteriores reglas de estilo se aplicaran al siguiente código HTML:

```html
<p>Hola maese LeGon!</p>
```

El resultado sería:

_**`Hola maese LeGon!`**_

En este ejemplo hemos incluído únicamente las propiedades: <mark style="color:blue;">**`font-weight`**</mark> y <mark style="color:blue;">**`font-style`**</mark> dentro de nuestro selector: <mark style="color:purple;">**`p`**</mark>, pero podríamos incluir todas las que fuesen necesarias.

{% hint style="warning" %}
No te olvides el caracter "**:**" tras indicar el nombre de la propiedad ni el caracter "**;**" tras asignarle su correspondiente valor. La sintaxis es simple pero no admite olvidos.
{% endhint %}
