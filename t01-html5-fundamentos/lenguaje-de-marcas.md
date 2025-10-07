# Lenguaje de marcas

HTML es un lenguaje de marcas, pero ¿qué entendemos por marcas? Una marca es esencialmente algo que añadimos sobre un documento para aportar información adicional sobre el mismo.

{% hint style="info" %}
El lenguaje **SGML** (_Standard Generalized Markup Language_), se publicó en 1986 y consiste en un metalenguaje que permite definir lenguajes de marcado. Se caracteriza por el uso de los caracteres “<” y “>” para la generación de las marcas y por especificar la sintaxis del documento que indica qué etiquetas están permitidas y dónde, mediante el **DTD** (_Document Type Definition_).
{% endhint %}

Existen muchas maneras de marcar un documento, pero HTML toma prestada la técnica del lenguaje SGML, el cuál utiliza los símbolos de menor que (“<”) y mayor que (“>”) para separar las distintas anotaciones del texto normal. Estas marcas son lo que denominaremos etiquetas en nuestro lenguaje HTML. Por regla general las etiquetas se agruparán en pares que indicarán el inicio y fin del marcado. El inicio lo indicaremos con una etiqueta tipo: “<**nombre\_tag**>” y el fin con una: “<**/nombre\_tag**>”. Veamos por ejemplo la siguiente porción de código HTML:

{% code lineNumbers="true" %}
```html
  <h1>Citas célebres de Noam Chomsky</h1>
    <p>
        La democracia participativa presupone la capacidad 
        de la gente normal para unir sus limitados recursos, 
        para formar y desarrollar ideas y programas, 
        incluirlos en la agenda política y actuar en su apoyo. 
        En ausencia de recursos y estructuras organizativas 
        que hagan posible esta actividad, la democracia 
        se limita a la opción de escoger entre varios candidatos 
        que representan los intereses de uno u otro grupo 
        que tiene una base de poder independiente, localizada 
        por lo general en la economía privada.
    </p>
    <p>
        El propósito de la educación es mostrar a la gente 
        cómo aprender por sí mismos. 
        El otro concepto de la educación es adoctrinamiento.
    </p>
```
{% endcode %}

Si eliminamos todas las marcas (etiquetas), el contenido continuará siendo perfectamente el mismo:

{% code lineNumbers="true" %}
```html
        Citas célebres de Noam Chomsky
        
        La democracia participativa presupone la capacidad 
        de la gente normal para unir sus limitados recursos, 
        para formar y desarrollar ideas y programas, 
        incluirlos en la agenda política y actuar en su apoyo. 
        En ausencia de recursos y estructuras organizativas 
        que hagan posible esta actividad, la democracia 
        se limita a la opción de escoger entre varios candidatos 
        que representan los intereses de uno u otro grupo 
        que tiene una base de poder independiente, localizada 
        por lo general en la economía privada.
     
        El propósito de la educación es mostrar a la gente 
        cómo aprender por sí mismos. 
        El otro concepto de la educación es adoctrinamiento.
```
{% endcode %}

Esto se debe a qué en realidad las etiquetas lo que proporcionan es _“metainformación”_ que indica cómo se organiza el contenido.\
Dado que las etiquetas no se muestran al usuario, podremos incluir tantas como sean necesarias sin afectar a la lectura del documento. Y aunque ahora no lo parezca, estas marcas tendrán un gran impacto en cómo se presenta esta información, siendo cruciales para garantizar la accesibilidad de la web.

{% hint style="info" %}
En HTML la mayoría de las etiquetas deben abrirse y cerrarse, es decir existe una etiqueta que marca el inicio de marcado y otra para indicar el fin. Aunque esta es la regla general, existen etiquetas especiales que solo emplean una única etiqueta, pues no se requiere indicar un fin de marcado concreto. Son los denominados **singleton tags**.
{% endhint %}
