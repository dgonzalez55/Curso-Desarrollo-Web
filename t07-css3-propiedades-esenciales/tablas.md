# Tablas

### Colapso de Bordes

La propiedad <mark style="color:blue;">**`border-collapse`**</mark> permite establecer para una tabla la forma en que sus bordes deben colapsar.\
Las palabras reservadas que se admiten como posibles valores para la propiedad son:

* <mark style="color:orange;">**`separate`**</mark> : Los bordes están separados; cada celda muestra los suyos. Valor por defecto.
* <mark style="color:orange;">**`collapse`**</mark> : Los bordes se colapsan en un único borde cuando es posible (Las propiedades <mark style="color:blue;">**`empty-cells`**</mark> y <mark style="color:blue;">**`border-spacing`**</mark> no tienen efecto).

A continuación, se presentan algunos ejemplos de uso:

```css
/* Mostramos los bordes de la tabla */
table, td, th {
  border: 1px solid black;
}
/* Para la tabla 1, los bordes no deben colapsar */
#table1 {
  border-collapse: separate;
}

/* Para la tabla 2, los bordes se colapsan */
#table2 {
  border-collapse: collapse;
}
```

![](<../.gitbook/assets/image (20).png>)

### Margen entre celdas

La propiedad <mark style="color:blue;">**`border-spacing`**</mark> permite establecer el margen entre los bordes de celdas adyacentes, por lo que solo tiene sentido si los bordes se encuentran separados (sin colapsar).\
Las sintaxis de la propiedad es la siguiente:

```css
/* Se establece el mismo valor de distancia para los ejes horizontal y vertical */
 border-spacing: distancia;

/* Se establecen distintos valores de distancia para el eje horizontal y vertical */
 border-spacing: distHorizontal distVertical;
```

A continuación, se presentan algunos ejemplos de uso:

```css
/* Mostramos los bordes de la tabla */
table, td, th {
  border: 1px solid black;
}
/* Espaciado de 15px entre los bordes horizontales y verticales */
#table1 {
  border-collapse: separate;
  border-spacing: 15px;
}

/* Espaciado de 15px entre los bordes horizontales y de 50px para los verticales */
#table2 {
  border-collapse: separate;
  border-spacing: 15px 50px;
}
```

![](<../.gitbook/assets/image (12).png>)

### Posición del título

La propiedad <mark style="color:blue;">**`caption-side`**</mark> permite establecer la posición en la que aparece el título de la tabla.\
Las palabras reservadas que se admiten como posibles valores para la propiedad son:

* <mark style="color:orange;">**`top`**</mark> : El título aparece encima de la tabla. Valor por defecto.
* <mark style="color:orange;">**`bottom`**</mark> : El título aparece debajo de la tabla.

A continuación, se presentan algunos ejemplos de uso:

```css
/* Para la tabla 1 el título se muestra debajo de la tabla */
#table1 {
  caption-side: bottom;
}

/* Para la tabla 2 el título se muestra encima de la tabla */
#table2 {
  caption-side: top;
}
```

![](<../.gitbook/assets/image (25).png>)

### Celdas Vacías

La propiedad <mark style="color:blue;">**`empty-cells`**</mark> permite establecer si se deben o no mostrar los bordes para las celdas vacías de una tabla.\
Las palabras reservadas que se admiten como posibles valores para la propiedad son:

* <mark style="color:orange;">**`show`**</mark> : Se muestran los bordes para las celdas vacías. Valor por defecto.
* <mark style="color:orange;">**`hide`**</mark> : Se ocultan los bordes para las celdas vacías.

A continuación, se presentan algunos ejemplos de uso:

```css
/* Mostramos los bordes de la tabla */
table, td, th {
  border: 1px solid black;
}
/* Para la tabla 1, se ocultan los bordes de las celdas vacías */
#table1 {
  empty-cells: hide;
}

/* Para la tabla 2, se muestran los bordes de las celdas vacías */
#table2 {
  empty-cells: show;
}
```

![](<../.gitbook/assets/image (4).png>)

### Layout

La propiedad <mark style="color:blue;">**`table-layout`**</mark> permite establecer el algoritmo que se emplea en la organización de las celdas, filas y columnas.\
Las palabras reservadas que se admiten como posibles valores para la propiedad son:

* <mark style="color:orange;">**`auto`**</mark> : El ancho de la columna lo establece el contenido _irrompible' más ancho de sus celdas. <mark style="background-color:red;">Esto implica que el contenido de la tabla es el que define el</mark>_ <mark style="background-color:red;"></mark><mark style="background-color:red;">layout</mark>_._
* <mark style="color:orange;">**`fixed`**</mark> : El ancho de la tabla y las columnas se establece mediante el valor de la propiedad <mark style="color:orange;">**`width`**</mark> de la tabla y columnas o por el ancho total de la primera fila de celdas. El ancho de las restantes celdas no afectan al ancho de las columnas. En el caso de que no existan anchos definidos en la primera fila, el ancho de las columnas de divide equitativamente a lo largo de la tabla, con independencia de su contenido.

A continuación, se presentan algunos ejemplos de uso:

```css
/* Mostramos los bordes de la tabla */
table, td, th {
  border: 1px solid black;
}
/* Para la tabla 1 la distribución de las celdas será automática en base al contenido */
#table1 {
  table-layout: auto;
  width: 180px;
}

/* Para la tabla 2 la distribución de las celdas será fija en base al ancho (180 píxeles) */
#table2 {
  table-layout: fixed;
  width: 180px;

}
```

<figure><img src="../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

### Maquetación avanzada

{% hint style="info" %}
Consulta la guía del W3Schools para descubrir más trucos sobre maquetación avanzada de tablas: [https://www.w3schools.com/Css/css\_table.asp](https://www.w3schools.com/Css/css_table.asp)
{% endhint %}
