# Añadir CSS a HTML

Existen hasta cuatro formas distintas de vincular el código CSS al código HTML, aunque no todas son igual de recomendables.

### Hoja de estilo externa

Es la opción más recomendable, pues se independiza totalmente el contenido (código HTML) de su presentación (código CSS). Si empleamos esta opción tendremos nuestros ficheros CSS separados de los ficheros HTML. Las hojas de estilo de aplicación se asociarán a los ficheros HTML como un recurso externo a través de la etiqueta `<`<mark style="color:green;">**`link`**</mark>`>` dentro del apartado `<`<mark style="color:green;">**`head`**</mark>`>` de la página web. Cabe decir, que podremos añadir tantas hojas de estilo como sea necesario a un mismo fichero html, aunque deberá considerarse la posibilidad de que se creen conflictos entre reglas contradictorias (se aplicarán las más restrictivas/concretas o las últimas en cargarse).

Suponiendo que disponemos de un fichero llamado "misEstilos.css" que deseamos asociar a un determinado código html, la forma de hacerlo sería la siguiente:

```html
<!DOCTYPE html>
<html lang=es>
  <head>
     ...
     <link rel="stylesheet" type="text/css" href="misEstilos.css" />
  </head>
  <body>
   ...
  </body>
</html>
```

### Hoja de estilo interna

No es una opción recomendable, pues cambios en los estilos implican cambios sobre los ficheros HTML que los contienen. Debería limitarse a únicamente elementos CSS que se estimen invariables y cuyas reglas sean breves. Aquí el código CSS se incluye dentro de la etiqueta `<`<mark style="color:green;">**`style`**</mark>`>` ubicada habitualmente en el apartado `<`<mark style="color:green;">**`head`**</mark>`>` de la página web.

Sirva como ejemplo el presente código en el que se definen una serie de reglas para cambiar el color y estilo de la fuente de los párrafos contenidos en el documento HTML:

```html
<!DOCTYPE html>
<html lang=es>
  <head>
     ...
     <style>
       p {
         color: blue;
         font-weight: bold;
       }
     </style>
  </head>
  <body>
   ...
  </body>
</html>
```

### Estilo inline

El código CSS se incluye como valor del atributo global **`style`** disponible en todas las etiquetas HTML, por lo que no es necesario el uso de selectores CSS al limitarse su aplicación a la etiqueta HTML que presenta el atributo **`style`**. Es la opción menos recomendable y debería evitarse en la medida de lo posible ya que cambios en los estilos implican cambios sobre todas las etiquetas HTML afectadas.

Sirva como ejemplo el presente código en el que se definen una serie de reglas para cambiar el color y estilo de la fuente de un párrafo en particular:

```html
<!DOCTYPE html>
<html lang=es>
  <head>
     ...
  </head>
  <body>
    <p style="color: blue; font-weight: bold;">Gon, eres lo mejor que nos ha pasado</p>
  </body>
</html>
```

### Directiva @import

La directiva <mark style="color:green;">**`@import`**</mark> usada dentro del código CSS permite importar reglas desde otras hojas de estilo. Se utiliza para relacionar entre sí hojas de estilo que mantienen dependencias entre ellas y/o para decidir la carga o no de determinados estilos en función del medio desde el que se consulta la página web. Su uso debería estar justificado, pues el abuso de la directiva <mark style="color:green;">**`@import`**</mark>puede ocasionar problemas de rendimiento al presentar un comportamiento bloqueante ya que el sistema debe esperar a la descarga completa de los recursos CSS importados antes de continuar obeniendo el resto de elementos de la página.

Sirva como ejemplo el presente código de muestra:

```html
<!DOCTYPE html>
<html lang=es>
  <head>
     ...
     <style>
       @import "misEstilos.css"
       @import "mobilEstilos.css" screen and (max-width: 768px);
       p {
         color: blue;
       }
     </style>
  </head>
  <body>
   ...
  </body>
</html>
```

En el ejemplo, tenemos una hoja de estilo interna que define un color de fuente "azul" para el texto de todos los párrafos y que carga como recursos externos un fichero de estilo llamado "misEstilos.css" (que podríamos haber cargado de la misma forma con la etiqueta `<`<mark style="color:green;">**`link`**</mark>**` `**<mark style="color:purple;">**`rel`**</mark>**`="`**<mark style="color:orange;">**`stylesheet`**</mark>**`"`` `**<mark style="color:purple;">**`type`**</mark>**`="`**<mark style="color:orange;">**`text/css`**</mark>**`"`` `**<mark style="color:purple;">**`href`**</mark>**`="`**<mark style="color:orange;">**`misEstilos.css`**</mark>**`" /`**`>`  dentro del apartado `<`<mark style="color:green;">**`head`**</mark>`>`). Adicionalmente, si el dispositivo que carga la web es una pantalla con un ancho máximo de 768 píxeles (caso de un smartphone) se cargaría también la hoja de estillo llamada "mobilEstilos.css".
