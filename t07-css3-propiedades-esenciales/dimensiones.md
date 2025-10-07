# Dimensiones

### Ancho

La propiedad <mark style="color:blue;">**`width`**</mark> permite establecer el ancho de un elemento de tipo **block** e **inline-block**, pues <mark style="background-color:red;">**sobre los elementos de tipo inline no surte ningún efecto**</mark>. Conviene tener en cuenta además, que en el cómputo del ancho no se consideran el tamaño del borde ni de los márgenes interiores. A parte de poder indicar el valor concreto de ancho, es posible especificar como valor la palabra clave <mark style="color:orange;background-color:orange;">**`auto`**</mark>, cuyo caso el ancho se calcula automáticamente por el navegador (es el valor por defecto).

A continuación, se muestran algunos ejemplos de uso:

```css
/* El ancho de las imágenes será el 50% del ancho de su elemento contenedor (padre)
   No se mantiene aspect ratio.
 */
img { width: 50%; }

/* Ídentico al anterior, pero manteniendo el aspect ratio */
img.proporcional {
  width: 50%;
  height: auto;
}

/* Se específica un ancho concreto en píxeles para todos los div */
div { width: 500px; }
```

{% hint style="info" %}
Existen las propiedades <mark style="color:blue;">**min-width**</mark> y <mark style="color:blue;">**max-width**</mark> que permiten definir el mínimo y máximo que se permite asignar al ancho del elemento y que se emplean en diseño responsivo. El valor de estas propiedades sobreescribe el de width.
{% endhint %}

### Alto

La propiedad <mark style="color:blue;">**`height`**</mark> permite establecer el alto de un elemento de tipo **block** e **inline-block**, pues sobre los elementos de tipo **inline** no surte ningún efecto. Conviene tener en cuenta además, que en el cómputo del alto no se consideran el tamaño del borde ni de los márgenes interiores. A parte de poder indicar el valor concreto de alto, es posible especificar como valor la palabra clave <mark style="color:orange;">**`auto`**</mark>, cuyo caso el alto se ajusta para permitir mostrar correctamente el contenido del elemento. En caso de indicar un valor numérico y que el tamaño del contenido supere el del contenedor, este sobrepasará el mismo. Existe la propiedad <mark style="color:blue;">**`overflow`**</mark> que permite controlar precisamente como se gestionan estos casos en los que se sobrepasa el tamaño asignado.

A continuación, se muestran algunos ejemplos de uso:

```css
/* El alto de las imágenes será el 50% del height de su elemento contenedor (padre)
   No se mantiene aspect ratio.
 */
img { height: 50%; }

/* Ídentico al anterior, pero manteniendo el aspect ratio */
img.proporcional {
  width: auto;
  height: 50%;
}

/* Se específica un alto concreto en píxeles para todos los div y se especifica que en caso
   que el contenido sobrepase el div, dicho contenido debe ocultarse */
div { 
  height: 50px; 
  overflow: hidden;
}
```

{% hint style="info" %}
Existen las propiedades <mark style="color:blue;">**min-height**</mark> y <mark style="color:blue;">**max-height**</mark> que permiten definir el mínimo y máximo que se permite asignar al alto del elemento y que se emplean en diseño responsivo. El valor de estas propiedades sobreescribe el de height.
{% endhint %}
