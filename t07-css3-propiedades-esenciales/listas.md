# Listas

### Tipo de Marcador

La propiedad <mark style="color:blue;">**`list-style-type`**</mark> permite establecer el marcador que se usará para señalar el item de una lista.\
Las palabras reservadas que se admiten como posibles valores para la propiedad son múltiples, destacando los siguientes:

* <mark style="color:orange;">**`disc`**</mark> : Círculo relleno. Valor por defecto de las listas no ordenadas.
* <mark style="color:orange;">**`circle`**</mark> : Círculo sin rellenar.
* <mark style="color:orange;">**`none`**</mark> : Sin símbolo marcador.
* <mark style="color:orange;">**`square`**</mark> : Cuadrado relleno.
* <mark style="color:orange;">**`decimal`**</mark> : El marcador es un número decimal. Valor por defecto de las listas ordenadas.
* <mark style="color:orange;">**`decimal-leading-zero`**</mark> : El marcador es un número decimal con un zero delante.
* <mark style="color:orange;">**`lower-latin`**</mark> : El marcador es una letra del alfabeto latino en mínuscula.
* <mark style="color:orange;">**`upper-latin`**</mark> : El marcador es una letra del alfabeto latino en mayúscula.
* <mark style="color:orange;">**`lower-roman`**</mark> : El marcador es un número romano en minúsculas.
* <mark style="color:orange;">**`upper-roman`**</mark> : El marcador es un número romano en mayúsculas.

Veamos algunos ejemplos de uso:

```css
ul.a {list-style-type: circle;}
ul.b {list-style-type: square;}
ol.c {list-style-type: upper-roman;}
ol.d {list-style-type: lower-latin;}
```

Ejemplo de lista con <mark style="color:blue;">**`list-style-type`**</mark>`:`` `<mark style="color:orange;">**`circle`**</mark>`;`

<img src="../.gitbook/assets/image (16).png" alt="" data-size="original">

Ejemplo de lista con <mark style="color:blue;">**`list-style-type`**</mark>`:`` `<mark style="color:orange;">**`square`**</mark>`;`

![](<../.gitbook/assets/image (9).png>)

Ejemplo de lista con <mark style="color:blue;">**`list-style-type`**</mark>`:`` `<mark style="color:orange;">**`upper-roman`**</mark>`;`

![](<../.gitbook/assets/image (1).png>)

Ejemplo de lista con <mark style="color:blue;">**`list-style-type`**</mark>`:`` `<mark style="color:orange;">**`lower-latin`**</mark>`;`

![](<../.gitbook/assets/image (6).png>)

### Posición del Marcador

La propiedad <mark style="color:blue;">**`list-style-position`**</mark> permite establecer la posición del marcador respecto el ítem de la lista.\
Las palabras reservadas que se admiten como posibles valores para la propiedad son :

* <mark style="color:orange;">**`inside`**</mark> : El marcador se encuentra dentro del ítem de la lista.
* <mark style="color:orange;">**`outside`**</mark> : El marcador se encuentra fuera del ítem de la lista. Es el valor por defecto de la propiedad.

Veamos algunos ejemplos de uso:

```css
ul.a {
  list-style-position: outside;
}

ul.b {
  list-style-position: inside;
}
```

Ejemplo de lista con <mark style="color:blue;">**`list-style-position`**</mark>`:`` `<mark style="color:orange;">**`outside`**</mark>`;` (se pintan los bordes de los elementos de la lista para ver el efecto):

![](<../.gitbook/assets/image (5).png>)

Ejemplo de lista con <mark style="color:blue;">**`list-style-position`**</mark>`:`` `<mark style="color:orange;">**`inside`**</mark>`;` (se pintan los bordes de los elementos de la lista para ver el efecto):

![](<../.gitbook/assets/image (8).png>)

### Imagen para el Marcador

La propiedad <mark style="color:blue;">**`list-style-image`**</mark> permite establecer la imagen que se utilizará como marcador del ítem de la lista.\
El valor por defecto para esta propiedad es <mark style="color:orange;">**`none`**</mark>, lo que significa que no se usa ninguna imagen personalizada. La sintaxis para esta propiedad es la siguiente:

```css
 list-style-image: url('RUTA_DE_LA_IMAGEN');
```

Veamos algunos ejemplos de uso:

```css
ul {
  list-style-image: url('https://cdn4.iconfinder.com/data/icons/fugue/icon_shadowless/open-source.png');
}
```

![](<../.gitbook/assets/image (13).png>)

### Tipo de Lista (Método Abreviado)

La propiedad <mark style="color:blue;">**`list-style`**</mark> es un método abreviado que permite establecer el tipo, posición, e imagen del marcador para la lista seleccionada mediante una única asignación.\
El tipo se corresponde con la propiedad <mark style="color:blue;">**`list-style-type`**</mark>, la posición con la propiedad <mark style="color:blue;">**`list-style-position`**</mark> y la imagen con la propiedad <mark style="color:blue;">**`list-style-image`**</mark>.\
Su sintaxis es la siguiente:

```css
list-style: tipo posición imagen;
```

A continuación, se presentan algunos ejemplos de uso:

```css
/* Se establece un marcador de tipo cuadrado, ubicado dentro del ítem de la lista y cuya imagen se encuentra en el fichero local sqpurple.gif */
ul.a {
  list-style: square inside url("sqpurple.gif");
}
/* Se establece un marcador de tipo circular y ubicado fuera del ítem de la lista */
ul.b {
   list-style: circle outside;
}
```

