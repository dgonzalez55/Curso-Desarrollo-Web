# Propiedades para elementos

### Orden

La propiedad <mark style="color:blue;">**`order`**</mark> permite establecer el orden en el que aparecen los elementos flexibles.\
La propiedad solo admite valores enteros (ya sean positivos o negativos) y el **valor por defecto es 0**.

Veamos algunos ejemplos de uso:

```css
/* Invertimos el orden de los elementos flexItem1 y flexItem2 */
#flexItem1{
  order: 2;
}
#flexItem2{
  order: 1;
}
#flexItem3{
  order: 3;
}
```

{% embed url="https://cdpn.io/dgonzalez55/fullpage/NWPJQGR?anon=true&view=fullpage" %}

{% hint style="danger" %}
Si modificas el orden de un elemento flexible, debes considerar los valores por defecto de los restantes (0)
{% endhint %}

### Crecimiento

La propiedad <mark style="color:blue;">**`flex-grow`**</mark> permite establecer el grado de crecimiento de un elemento flexible si se requiere que éste crezca. Por ejemplo, si todos los elementos flexibles tienen valor 1, eso significa que el espacio libre disponible en el contenedor se repartirá uniformemente entre todos ellos, por el contrario, si uno de los elementos tiene un valor de 2, dicho elemento tomará el doble de espacio libre que el resto.\
La propiedad solo admite valores positivos y **su valor por defecto es 0**.

Veamos algunos ejemplos de uso:

```css
/* El flexItem1, crece el doble que los demás */
#flexItem1{
  flex-grow: 2;
}
#flexItem2{
  flex-grow: 1;
}
#flexItem3{
  flex-grow: 1;
}
```

{% embed url="https://cdpn.io/dgonzalez55/fullpage/GRgLpJB?anon=true&view=fullpage" %}

### Decrecimiento

La propiedad <mark style="color:blue;">**`flex-shrink`**</mark> permite establecer el grado de decrecimiento de un elemento flexible si se requiere que éste se de reduzca. Su funcionamiento es análogo al visto en la propiedad <mark style="color:blue;">**`flex-grow`**</mark>.\
La propiedad solo admite valores positivos y **su valor por defecto es 1**.

Veamos algunos ejemplos de uso:

```css
/* Todos los elementos se encogen proporcionalmente para caber en el contenedor flexible */
#flexItem1{
  flex-shrink: 1;
}
#flexItem2{
  flex-shrink: 1;
}
#flexItem3{
  flex-shrink: 1;
}
```

{% embed url="https://cdpn.io/dgonzalez55/fullpage/mdygeRz?anon=true&view=fullpage" %}

### Tamaño Base

La propiedad <mark style="color:blue;">**`flex-basis`**</mark> permite establecer el tamaño predeterminado de un elemento flexible antes de que se distribuya el espacio sobrante. Su valor puede ser una medida (por ejemplo, 20%, 5rem, etc.) o la palabra clave <mark style="color:orange;">**`auto`**</mark>, en cuyo caso, se establece el tamaño base en función del valor de las propiedades <mark style="color:blue;">**`width`**</mark> y/o <mark style="color:blue;">**`height`**</mark>.\
El **valor por defecto es&#x20;**<mark style="color:orange;">**`auto`**</mark>.

Veamos algunos ejemplos de uso:

```css
/* El elemento flexible 2 tiene un tamaño base de 160px, independientemente de lo que se establezca en las propiedades width o height, el resto de elementos respetan el ancho/alto configurado */
#flexItem1{
  flex-basis: auto;
}
#flexItem2{
  flex-basis: 160px;
}
#flexItem3{
  flex-basis: auto;
}
```

{% embed url="https://cdpn.io/dgonzalez55/fullpage/YzPMqrZ?anon=true&view=fullpage" %}

{% hint style="warning" %}
Si se establece un valor diferente de **auto**, lo que indiquen las propiedades **width** y/o **height** se ignorará.
{% endhint %}

### Tipo Flexible (Método abreviado)

La propiedad <mark style="color:blue;">**`flex`**</mark> es un método abreviado que permite establecer el tamaño base, el grado de crecimiento y de decrecimiento de un elemento flexible.\
El tamaño base se corresponde con la propiedad <mark style="color:blue;">**`flex-basis`**</mark>, el grado de crecimiento con la propiedad <mark style="color:blue;">**`flex-grow`**</mark> y el grado de decrecimiento con la propiedad <mark style="color:blue;">**`flex-shrink`**</mark>.\
Su sintaxis es la siguiente, considerando los dos últimos parámetros como opcionales:

```css
flex: crecimiento decrecimiento base;
```

A continuación, se presentan algunos ejemplos de uso:

```css
/* El elemento flexible se redimensionará con un factor de x2 respecto los otros elementos si sobra espacio y si faltase se intentaría encajar con un factor x1 */
.flexItem1{
  flex: 2;
}
/* El elemento flexible no se redimensionará y su tamaño base se establece en 100px */
.flexItem2{
  flex: 0 0 100px;
}
```

{% hint style="info" %}
Es mejor utilizar este método abreviado que sus propiedades individualmente, ya que en caso de no indicar todos los valores, los restantes se configurarán de manera inteligente
{% endhint %}

### Alineación eje transversal específica

La propiedad **`align-self`** permite establecer una alineación específica para el elemento flexible distinta de la definida de manera genérica por la propiedad <mark style="color:blue;">**`align-items`**</mark>.\
Las palabras reservadas que se admiten como posibles valores para la propiedad son las siguientes:

* <mark style="color:orange;">**`stretch`**</mark> : El elemento se redimensiona para rellenar el contenedor en la dimensión transversal.
* <mark style="color:orange;">**`flex-start`**</mark> : El elemento se alinea hacia el inicio del eje transversal.
* <mark style="color:orange;">**`flex-end`**</mark> : El elemento se alinea hacia el final del eje transversal.
* <mark style="color:orange;">**`center`**</mark> : El elemento se alinea hacia el centro de la fila o columna.
* <mark style="color:orange;">**`baseline`**</mark> : El elemento se alinea alrededor de la línea base.

Veamos un ejemplo de uso:

{% embed url="https://cdpn.io/dgonzalez55/fullpage/VwYNjZr?anon=true&view=fullpage" %}
