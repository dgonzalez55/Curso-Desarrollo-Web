# Atributos globales

Aunque la mayoría de los elementos estructurales tienen un propósito implícito que se refleja en sus nombres, esto no significa que se deban usar solo una vez en el mismo documento. Por ejemplo, algunos elementos como `<`<mark style="color:green;">**`section`**</mark>`>` y `<`<mark style="color:green;">**`aside`**</mark>`>` se pueden utilizar muchas veces para representar diferentes partes de la estructura, y otros como `<`<mark style="color:green;">**`div`**</mark>`>` son implementados de forma repetida para separar contenido dentro de secciones. Por esta razón, HTML define atributos globales que podemos usar para asignar identificadores personalizados a cada elemento. La asignación de estos atributos será crucial para las labores de definición de estilos mediante las reglas CSS.<br>

Veamos los atributos globales básicos:

* **id**: Nos permite asignar un identificador único a un elemento y dentro de una misma página HTML no deberíamos tener más de un elemento con el mismo valor asignado. Vendría a ser el equivalente al DNI para los elementos HTML.
* **class**: Nos permite asignar el mismo identificador a un grupo de elementos. Vendría a ser el equivalente a una tarjeta de socio (_Club Super3, Club Carrefour, ..._) para los elementos HTML.

El atributo **id** identifica elementos independientes con un valor único, mientras que el valor del atributo **class** se puede duplicar para asociar elementos con características similares. Por ejemplo, si tenemos dos o más elementos `<`<mark style="color:green;">**`section`**</mark>`>` que necesitamos diferenciar entre sí, podemos asignar el atributo id a cada uno con valores diferentes que declaran sus propósitos.

```html
 <body>
   ...
      <section id="ciclosuperior">Información sobre los Ciclos Formativos de Grado Superior</section>
      <section id="ciclomedio">Información sobre los Ciclos Formativos de Grado Medio</section>
   ...
</body>
```

El ejemplo presenta dos elementos `<`<mark style="color:green;">**`section`**</mark>`>` para separar los apartados que tratan los ciclos formativos de grado superior de los de grado medio. Debido a que el contenido de estos elementos es diferente, requieren distintos estilos y, por lo tanto, tenemos que identificarlos con diferentes valores. El primer elemento `<`<mark style="color:green;">**`section`**</mark>`>` se ha identificado con el valor "ciclosuperior" y el segundo elemento con el valor "ciclomedio". Por otro lado, si lo que necesitamos es identificar un grupo de elementos con características similares, podemos usar el atributo **class**.\
\
El siguiente ejemplo divide el contenido de una sección con elementos `<`<mark style="color:green;">**`div`**</mark>`>`. Debido a que todos tienen un contenido similar, compartirán los mismos estilos y, por lo tanto, deberíamos identificarlos con el mismo valor (todo son de la misma clase).

```html
 <body>
   ...
      <section>
         <div class="pelis">Matrix</div>
         <div class="pelis">Pulp Fiction</div>
         <div class="pelis">El Club de la Lucha</div>
         <div class="pelis">El Caballero Oscuro</div>
         ...
      </section>
   ...
</body>
```

El ejemplo presenta un único elemento `<`<mark style="color:green;">**`section`**</mark>`>` con el que representamos el contenido principal del documento, pero hemos creado varias divisiones con elementos `<`<mark style="color:green;">**`div`**</mark>`>` para organizar el contenido. Debido a que estos elementos se han identificado con el atributo **class** y el valor "pelis", cada vez que accedemos o modificamos elementos referenciando la clase libros, todos estos elementos se ven afectados.

{% hint style="warning" %}
Los valores asignados a los atributos **id** y **class** son arbitrarios. Puedes asignarles cualquier valor que desees, siempre y cuando no incluyas ningún espacio en blanco (el atributo **class** utiliza espacios para asignar múltiples clases a un mismo elemento). Así mismo, para mantener el sitio web compatible con todos los navegadores, deberías usar solo letras y números, siempre comenzar con una letra y evitar caracteres especiales.
{% endhint %}
