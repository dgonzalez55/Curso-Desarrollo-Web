# Propiedades para contenedores

### Dirección

La propiedad <mark style="color:blue;">**`flex-direction`**</mark> permite establecer el eje principal, definiendo así la dirección en la que se colocan los elementos flexibles dentro del contenedor. Mediante esta propiedad pues, indicaremos si los elementos se distribuyen mediante una fila o mediante una columna, así como la dirección de las mismas.\
Las palabras reservadas que se admiten como posibles valores para la propiedad son las siguientes:

* <mark style="color:orange;">**`row`**</mark> : Los elementos se distribuyen en fila de izquierda a derecha. Es el valor por defecto.
* <mark style="color:orange;">**`row-reverse`**</mark> : Los elementos se distribuyen en fila pero en sentido opuesto, de derecha a izquierda.
* <mark style="color:orange;">**`column`**</mark> : Los elementos se distribuyen en columna de arriba a abajo.
* <mark style="color:orange;">**`column-reverse`**</mark> : Los elementos se distribuyen en columna pero en sentido opuesto, de abajo a arriba.

Veamos algunos ejemplos de uso:

```css
/* Los elementos se distribuirán en columna de arriba a abajo */
.flexcontainerCol{
  display: flex;
  flex-direction: column;
}
/* Los elementos se distribuirán en fila de derecha a izquierda */
.flexcontainerRowRev{
  display: flex;
  flex-direction: row-reverse;
}
```

{% embed url="https://cdpn.io/dgonzalez55/fullpage/eYmXxBw?anon=true&view=fullpage" %}

### Ajuste

La propiedad <mark style="color:blue;">**`flex-wrap`**</mark> permite establecer si los elementos flexibles deben ajustarse en una única línea o columna, o si por el contrario se deben ajustar según sea necesario en base al espacio disponible.\
Las palabras reservadas que se admiten como posibles valores para la propiedad son las siguientes:

* <mark style="color:orange;">**`nowrap`**</mark> : Los elementos se distribuyen entorno a una única fila o columna. Es el valor por defecto.
* <mark style="color:orange;">**`wrap`**</mark> : Los elementos se distribuyen en múltiples files de arriba a abajo o en múltiples columnas de izquierda a derecha.
* <mark style="color:orange;">**`wrap-reverse`**</mark> : Los elementos se distribuyen múltiples filas o columnas, pero en sentido inverso.

Veamos algunos ejemplos de uso:

```css
/* Los elementos se distribuirán en múltiples columnas de arriba a abajo */
.flexcontainerCol{
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
}
/* Los elementos se distribuirán en múltiples fila de derecha a izquierda y de abajo a arriba */
.flexcontainerRowRev{
  display: flex;
  flex-direction: row-reverse;
  flex-wrap: wrap-reverse;
}
```

{% embed url="https://cdpn.io/dgonzalez55/fullpage/abzMrxB?anon=true&view=fullpage" %}

### Flujo (Método abreviado)

La propiedad <mark style="color:blue;">**`flex-flow`**</mark> es un método abreviado que permite establecer la dirección y ajuste de los elementos flexibles dentro de un contenedor.\
La dirección se corresponde con la propiedad <mark style="color:blue;">**`flex-direction`**</mark> y el ajuste con la propiedad <mark style="color:blue;">**`flex-wrap`**</mark>.\
Su sintaxis es la siguiente:

```css
flex-flow: direccion ajuste;
```

A continuación, se presentan algunos ejemplos de uso:

```css
/* Los elementos se distribuirán en una única columna de arriba a abajo */
.flexcontainerCol{
  display: flex;
  flex-flow: column nowrap;
}
/* Los elementos se distribuirán en múltiples filas de derecha a izquierda y de arriba a abajo*/
.flexcontainerRowRev{
  display: flex;
  flex-flow: row-reverse wrap;
}
```

### Alineación eje principal

La propiedad <mark style="color:blue;">**`justify-content`**</mark> permite establecer la alineación de los elementos flexibles a lo largo del eje principal. Ayuda a distribuir el espacio libre que queda cuando todos los elementos flexibles han alcanzado su tamaño máximo. También ejerce cierto control sobre la alineación de los elementos cuando estos sobrepasan la línea o columna.\
Las palabras reservadas que se admiten como posibles valores para la propiedad son las siguientes:

* <mark style="color:orange;">**`flex-start`**</mark> : Los elementos se alinean hacia el inicio de la fila o columna. Es el valor por defecto.
* <mark style="color:orange;">**`flex-end`**</mark> : Los elementos se alinean hacia el final de la fila o columna.
* <mark style="color:orange;">**`center`**</mark> : Los elementos se alinean hacia el centro de la fila o columna.
* <mark style="color:orange;">**`space-between`**</mark> : Los elementos se alinean uniformemente en la fila o columna. El primer elemento se posiciona al inicio de la fila/columna y el último al final de la fila/columna.
* <mark style="color:orange;">**`space-around`**</mark> : Los elementos se alinean uniformemente en la fila o columna manteniendo el mismo espaciado entre ellos.
* <mark style="color:orange;">**`space-evenly`**</mark> : Similar al anterior pero agregando que el espaciado entre dos elementos debe ser idéntico.

\
Veamos algunos ejemplos de uso:

{% embed url="https://cdpn.io/dgonzalez55/fullpage/xxbBoEL?anon=true&view=fullpage" %}

### Alineación eje transversal

La propiedad <mark style="color:blue;">**`align-items`**</mark> permite establecer la alineación de los elementos flexibles a lo largo del eje transversal. Viene a ser la versión de la propiedad <mark style="color:blue;">**`justify-content`**</mark> pero para el eje transversal.\
Las palabras reservadas que se admiten como posibles valores para la propiedad son las siguientes:

* <mark style="color:orange;">**`stretch`**</mark> : Los elementos se redimensionan para rellenar el contenedor en la dimensión transversal. Es el valor por defecto.
* <mark style="color:orange;">**`flex-start`**</mark> : Los elementos se alinean hacia el inicio del eje transversal.
* <mark style="color:orange;">**`flex-end`**</mark> : Los elementos se alinean hacia el final del eje transversal.
* <mark style="color:orange;">**`center`**</mark> : Los elementos se alinean hacia el centro de la fila o columna.
* <mark style="color:orange;">**`baseline`**</mark> : Los elementos se alinean alrededor de la línea base.

\
Veamos algunos ejemplos de uso:

{% embed url="https://cdpn.io/dgonzalez55/fullpage/Baybgwg?anon=true&view=fullpage" %}

### Alineación eje transversal (múltiple)

La propiedad <mark style="color:blue;">**`align-content`**</mark> permite establecer la alineación de los elementos flexibles a lo largo del eje transversal cuando existe espacio sobrante. Su funcionamiento es similar al de la propiedad <mark style="color:blue;">**`justify-content`**</mark> pero para el eje transversal y <mark style="background-color:orange;">**siempre que exista más de una fila de elementos flexibles**</mark>.\
Las palabras reservadas que se admiten como posibles valores para la propiedad son las siguientes:

* <mark style="color:orange;">**`flex-start`**</mark> : Las filas de elementos se compactan hacia el inicio del eje transversal.
* <mark style="color:orange;">**`flex-end`**</mark> : Las filas de elementos se compactan hacia el final del eje transversal.
* <mark style="color:orange;">**`center`**</mark> : Las filas de elementos se compactan hacia el centro del eje transversal.
* <mark style="color:orange;">**`space-between`**</mark> : Las filas de elementos se alinean uniformemente a lo largo del eje transversal. El primer elemento se posiciona al inicio del eje y el último al final.
* <mark style="color:orange;">**`space-around`**</mark> : Las filas de elementos se alinean uniformemente a lo largo del eje transversal pero manteniendo el mismo espaciado entre ellas. El primer elemento se posiciona al inicio del eje y el último al final.
* <mark style="color:orange;">**`stretch`**</mark> : Las filas de elementos se redimensionan para ocupar todo el contenedor. Es el valor por defecto.

\
Veamos algunos ejemplos de uso:

{% embed url="https://cdpn.io/dgonzalez55/fullpage/PowLrar?anon=true&view=fullpage" %}
