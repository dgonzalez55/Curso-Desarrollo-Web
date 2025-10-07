# Herencia y Resolución de Conflictos

### Efecto cascada y Herencia

Como ya se ha mencionado el **efecto cascada** se refiere al esquema de funcionamiento que rige la aplicación de las hojas de estilo y que nos permite reducir al mínimo posible el número de reglas a declarar, dado que la mayoría de estilos se aplicarán en **cascada**, heredándose las reglas establecidas en los contenedores padre.

\
En resumen:

* Los estilos se van propagando hacia abajo o lo que es lo mismo si especificamos una propiedades en un elemento padre los hijos tienen el mismo valor para esas propiedades (salvo excepciones).
* Si hay más de una regla que se puede aplicar al mismo elemento y hay conflicto, entonces se aplica la regla más específica o restrictiva.

Aunque la herencia de estilos se aplica automáticamente, se puede anular su efecto estableciendo de forma explícita otro valor para la propiedad que se hereda.\
La mayoría de propiedades CSS aplican la herencia de estilos de forma automática. Además, para aquellas propiedades que no se heredan automáticamente, CSS incluye un mecanismo para forzar que se hereden sus valores, tal y como se verá más adelante. Por último, aunque la herencia automática de estilos puede parecer complicada, simplifica en gran medida la creación de hojas de estilos complejas. Como se ha visto en los ejemplos anteriores, si se quiere establecer por ejemplo la tipografía base de la página, simplemente se debe establecer en el elemento `<`<mark style="color:green;">**`body`**</mark>`>` de la página y el resto de elementos la heredarán de forma automática.

### Resolución de Conflictos CSS

El método seguido por CSS para resolver las colisiones de estilos es:

1. Determinar todas las declaraciones que se aplican al elemento para el medio CSS seleccionado.
2. Ordenar las declaraciones según su origen (CSS de navegador, de usuario o de diseñador) y su prioridad (palabra clave <mark style="color:red;">**`!important`**</mark>).
3. Ordenar las declaraciones según lo específico que sea el selector. Cuanto más genérico es un selector, menos importancia tienen sus declaraciones.
4. Si después de aplicar las normas anteriores existen dos o más reglas con la misma prioridad, se aplica la que se indicó en último lugar.

En resumen:

* Cuanto más específico sea un selector, más importancia tiene su regla asociada.
* A igual especificidad, se considera la última regla indicada.

El uso de la palabra clave <mark style="color:red;">**`!important`**</mark> como sufijo del valor de una propiedad, indica que dicho valor prevalece sobre el de cualquier otra asignación en otras reglas CSS, incluso por delante de aquellas que resulten ser más específicas. Un ejemplo podría ser el siguiente:

```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <style>
      p, a { color: blue!important; }
      a.rojizo { color: red; }
    </style>
  </head>
  <body>
    <p>Ejemplo de palabra clave <a class="rojizo" href="#">!important</a></p>
  </body>
</html>
```

En este ejemplo todo el texto aparecería en azul, incluso el del enlace. Sin embargo, bastaría con eliminar la palabra clave <mark style="color:red;">**`!important`**</mark> de la regla css <mark style="color:purple;">**`p, a`**</mark> para que el texto del enlace pasara a mostrarse como rojo.

{% hint style="danger" %}
El uso de la palabra clave <mark style="color:red;">**`!important`**</mark> debe limitarse a estrictamente a aquellas circunstancias en las que resulte necesario, pues un abuso de la misma puede acarrear que nada funcione como es debido. Recuerda la máxima que dice "_**Si todo es importante, nada es importante.**_"
{% endhint %}
