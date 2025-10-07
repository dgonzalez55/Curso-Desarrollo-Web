# Recomendaciones HTML5

Aunque los navegadores actuales pueden procesar casi cualquier documento, incluyendo aquellos con errores, es importante cumplir en lo posible las reglas de sintaxis que se recomiendan:

* Aunque los nombres de los elementos o etiquetas no son sensibles a mayúsculas o minúsculas, los escribiremos siempre en minúsculas. → **\<html>** y no _\<HTML>_ o _\<Html>_.
* Aunque los nombres de los atributos no son sensibles a mayúsculas o minúsculas, los escribiremos siempre en minúsculas. → \<html **lang**=es> y no \<html _LANG_=es>.
* Los valores de los atributos pueden ser sensibles a mayúsculas y minúsculas, por lo que los escribiremos cómo procedan.

{% hint style="danger" %}
En Linux <mark style="color:green;">\<img</mark> <mark style="color:blue;">src</mark>="<mark style="color:purple;">file1.png</mark>"<mark style="color:green;">></mark> no es lo mismo que <mark style="color:green;">\<img</mark> <mark style="color:blue;">src</mark>="<mark style="color:purple;">FILE1.png</mark>"<mark style="color:green;">></mark>
{% endhint %}

* Los nombres de las etiquetas no deben contener espacios en blanco → **\<html>** y no _\<h t m l >_.
* El valor de los atributos siempre se debería **entrecomillar**, aunque no sea obligatorio ni necesario en todos los casos. → `<html lang="es">` y no `<html lang=es>`.
* Todos los atributos deben tener un valor asignado → \<html **lang="es"**> y no \<html _lang_>
* En HTML se asume cualquier número de caracteres en blanco (espacios, intros o tabuladores) como un único caracter de espacio en blanco. Los exploradores los ignoran o destruyen, a no ser que se encuentren dentro de una etiqueta de preformateado.
* Las etiquetas que encierran contenido se deben cerrar siempre. → **\<html> … \</html>** y no **\<html> …**.
* Las etiquetas pueden anidarse, pero la primera que se cierra siempre es la última que se abrió (esquema LIFO). → `<p><em>este texto tiene mucho énfasis</em></p>` y no `<p><em> este texto tiene mucho énfasis</p></em>`
* En los comentarios de código no se deberían incluir los guiones dobles → `<!-- Es válido -->` y no `<!-- No es -- válido -->`
* Las etiquetas de tipo singleton pueden cerrarse añadiendo una / al final, aunque esto solo se debería realizar en el caso de XHTML. → `<br>` puede indicarse como `<br/>`.
* Todo el código debe estar siempre correctamente **indentado**, con al menos una separación o tabulación por nivel de anidamiento.
* Los exploradores omiten los elementos desconocidos, tanto etiquetas como atributos, pero no conviene añadir elementos que no sean contemplados por el estándar HTML5.

{% hint style="info" %}
El primer documento de tu página web debería ser un fichero llamado **index.html**, ya que es el que la mayoría de los servidores web buscan para designar la página principal o home del sitio que alojan.
{% endhint %}

Dado que en HTML existen caracteres reservados, se requiere utilizar códigos de referencia para incluirlos como contenido en nuestra página. Para indicar una referencia a un carácter especial se utiliza el **"&"** seguido de su **valor UNICODE** o del nombre asignado a dicha entidad y se termina con un **";"**. Veamos los principales caracteres protegidos existentes:

* `&lt;` → Menor que ‘<’
* `&gt;` → Mayor que ‘>’
* `&amp;` → Ampersand ‘&’
* `&nbsp;` → Espacio en blanco ‘ ‘
* `&quot;` → Comillas dobles ”

Además, se pueden utilizar también referencias a otros caracteres especiales, como por ejemplo:

* `&copy;` → Carácter de copyright.
* `&num;` → Hashtag ‘#’
* `&euro;` → Símbolo de euro ‘€’

Puedes consultar todas las referencias existentes que puedes utilizar en: [https://dev.w3.org/html5/html-author/charref](https://dev.w3.org/html5/html-author/charref)
