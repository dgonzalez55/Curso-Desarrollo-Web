# Pseudoelementos

Las pseudoelementos sirven para establecer estilos para determinadas partes de los elementos seleccionados, como por ejemplo dar un estilo específico a la primera letra o línea de un elemento, insertar un contenido previo o posterior al contenido del elemento seleccionado, etc.\


La sintaxi de un pseudoelemento es:

```css
selector::pseudoelemento {
  propiedad:valor;
}
```

A continuación repasaremos los pseudoelementos existentes.

{% hint style="info" %}
La sintaxis diferenciada entre pseudoelementos y pseudoclases es una de las novedades de **CSS3**, pues anteriormente en ambos casos se usaba un único "**:**" para separar la pseudoclase o pseudoelemento del selector.
{% endhint %}

### ::after

El pseudoelemento <mark style="color:purple;">**`::after`**</mark>permite insertar contenido tras el propio contenido del elemento seleccionado. A tal efecto, debe emplearse la propiedad `content` para especificar el contenido a insertar.

Veamos un ejemplo de aplicación:

```css
/* Inserta al final de cada párrafo una nota recordatorio */
p::after {
  content: " - Recuerda!";
  background-color: yellow;
  color: red;
  font-weight: bold;
}
```

### ::before

El pseudoelemento <mark style="color:purple;">**`::before`**</mark>permite insertar contenido previo al propio contenido del elemento seleccionado. A tal efecto, debe emplearse la propiedad `content` para especificar el contenido a insertar.

Veamos un ejemplo de aplicación:

```css
/* Inserta al principio de cada párrafo una nota para leer el mismo */
p::before {
  content: "Lee esto: ";
}
```

### ::first-letter

El pseudoelemento <mark style="color:purple;">**`::first-letter`**</mark>permite aplicar un estilo distintivo a la primera letra del contenido del elemento seleccionado.

Veamos un ejemplo de aplicación:

```css
/* Incrementa el tamaño de la primera letra de cada párrafo y le cambia el color a rojo */
p::first-letter {
  font-size: 200%;
  color: red;
}
```

{% hint style="warning" %}
Este pseudoelemento solo se puede utilizar en elementos de tipo **block**.
{% endhint %}

### ::first-line

El pseudoelemento <mark style="color:purple;">**`::first-line`**</mark> permite aplicar un estilo distintivo a la primera línea de texto del contenido del elemento seleccionado.

Veamos un ejemplo de aplicación:

```css
/* Establece el color de la fuente en rojo para la primera línea de texto de los párrafos */
p::first-line {
  color: red;
}
```

{% hint style="warning" %}
Este pseudoelemento solo se puede utilizar en elementos de tipo **block**.
{% endhint %}

### ::selection

El pseudoelemento <mark style="color:purple;">**`::selection`**</mark> permite aplicar un estilo distintivo a la porción del elemento seleccionado que el usuario haya seleccionado.

Veamos un ejemplo de aplicación:

```css
/* Establece el color de la fuente en rojo y el fondo en amarillo para la selección del usuario */
::selection {
  color: red;
  background: yellow;
}
```

{% hint style="warning" %}
Únicamente se pueden modificar las propiedades **color**, **background**, **cursor** y **outline** mediante el uso de este pseudoelemento.
{% endhint %}
