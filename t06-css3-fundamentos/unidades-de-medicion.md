# Unidades de Medición

CSS3 nos permite expresar los tamaños y medidas en distintas unidades de medición, algunas de ellas de tipo relativo y otras de tipo absoluto. En cualquier caso, la unidad de medición debe expresarse siempre a continuación del valor numérico sin espacios en blanco. Por ejemplo: **`10px`**, **`3%`**, **`1.4rem`**, ... Únicamente para el valor numérico **`0`** se permite omitir la unidad de medición.

#### Unidades Absolutas

Son unidades de tamaño fijo que no dependen de nada más, muy prácticas si se conoce el medio o la resolución exacta de salida. Se desaconseja en general su uso en diseños responsivos pues al ser fijas no se "_adaptan_" correctamente.

* <mark style="background-color:blue;">**px**</mark>: Nos permite expresar una medición en píxeles.
* <mark style="background-color:blue;">**cm**</mark>: Nos permite expresar una medición en centímetros.
* <mark style="background-color:blue;">**in**</mark>: Nos permite expresar una medición en pulgadas (1in = 96px = 2.54cm).
* <mark style="background-color:blue;">**pt**</mark>: Nos permite expresar una medición en puntos (1pt = 1/72 in).

#### Unidades Relativas

Son unidades cuyo valor es relativo al valor de otra propiedad de referencia. Su uso es esencial para garantizar un diseño responsivo.

* <mark style="background-color:orange;">**%**</mark>: Nos permite expresar un porcentaje de tamaño relativo respecto del elemento padre.
* <mark style="background-color:orange;">**em**</mark>: Nos permite expresar un tamaño relativo al tamaño de la fuente del elemento actual.
* <mark style="background-color:orange;">**rem**</mark>: Nos permite expresar un tamaño relativo al tamaño de la fuente del elemento `<`<mark style="color:green;">**`html`**</mark>`>`.
* <mark style="background-color:orange;">**vw**</mark>: Nos permite expresar un tamaño relativo al 1% del ancho del **viewport**.
* <mark style="background-color:orange;">**vh**</mark>: Nos permite expresar un tamaño relativo al 1% del alto del **viewport**.
* <mark style="background-color:orange;">**vmin**</mark>: Nos permite expresar un tamaño relativo al 1% del mínimo valor del **viewport**: 1vw o 1vh.
* <mark style="background-color:orange;">**vmax**</mark>: Nos permite expresar un tamaño relativo al 1% del máximo valor del **viewport**: 1vw o 1vh.

{% hint style="info" %}
**Viewport** se refiere al tamaño de la ventana del navegador. Siendo el ancho del viewport de 100vw y el alto de 100vh.
{% endhint %}
