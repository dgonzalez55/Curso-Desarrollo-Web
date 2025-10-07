# Selectores Avanzados

<details>

<summary>SUMARIO</summary>

[#selector-hijo](selectores-avanzados.md#selector-hijo "mention")

[#selector-adyacente](selectores-avanzados.md#selector-adyacente "mention")

[#selector-predecesor](selectores-avanzados.md#selector-predecesor "mention")

[#selector-de-atributo](selectores-avanzados.md#selector-de-atributo "mention")

</details>

### Selector Hijo

El funcionamiento del selector de hijo es análogo al del selector descendente, pero limitando el alcance de la selección a los elementos que son hijos directos del elemento que antecede el "signo de mayor que" (**>**). Su sintaxis se resume de la siguiente manera:

```css
elementoPadre > elementoHijo { ... }
```

A continuación se presenta un posible ejemplo de su uso:

```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <style>
      p span { color: red; }
      p > span { color: blue; }
    </style>
  </head>
  <body>
    <p><span>Maese</span></p>
    <p><a href="#"><span>LeGon</span></a></p>
  </body>
</html>
```

En el ejemplo anterior, se modificaría el color del texto <mark style="color:blue;">**`Maese`**</mark> a azul, pues el elemento `<`<mark style="color:green;">**`span`**</mark>`>` asociado es un hijo directo de `<`<mark style="color:green;">**`p`**</mark>`>`. No obviamos el hecho de que para este elemento también se cumple la regla del selector descendente, pero ante múltiples reglas en conflicto se aplica siempre la más restrictiva, y el selector de hijo es siempre más restrictivo que el selector descendente. El texto <mark style="color:red;">**`LeGon`**</mark>, se mostraría en rojo, ya que el elemento `<`<mark style="color:green;">**`span`**</mark>`>` en este caso es hijo directo de un `<`<mark style="color:green;">**`a`**</mark>`>` y no de un elemento `<`<mark style="color:green;">**`p`**</mark>`>`, pero aunque no se cumple la regla del selector hijo, sí que se cumpliría la del selector descendente.

### Selector Adyacente

El selector adyacente se emplea para seleccionar elementos que en el código HTML de la página se encuentran justo a continuación de otros elementos. Su sintaxis emplea el signo **+** para separar los dos elementos.

```css
elementoAnterior + elementoSeleccionado { ... }
```

En este selector se deben cumplir dos reglas básicas:

* El _**elementoAnterior**_ y el _**elementoSeleccionado**_ son hermanos, es decir, tienen el mismo padre y por tanto se encuentran al mismo nivel.
* El _**elementoSeleccionado**_ debe aparecer exactamente justo a continuación del _**elementoAnterior**_.

Veamos un ejemplo de su uso:

```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <style>
      h2 { color: green; }
      h1 + h2 { color: red }
    </style>
  </head>
  <body>
    <h1>SMR</h1>
    <h2>Profesorado</h2>
    ...
    <h2>Alumnado</h2>
    ...
  </body>
</html>
```

Las reglas CSS anteriores hacen que todos los `<`<mark style="color:green;">**`h2`**</mark>`>` de la página se vean de color verde, salvo aquellos `<`<mark style="color:green;">**`h2`**</mark>`>` que se encuentran inmediatamente después de cualquier elemento `<`<mark style="color:green;">**`h1`**</mark>`>` y que se muestran de color rojo. Así pues, en nuestro ejemplo `"`<mark style="color:red;">**`Profesorado`**</mark>`"` aparecería de color rojo mientras que `"`<mark style="color:green;">**`Alumnado`**</mark>`"` aparecería de color verde.

### Selector Predecesor

El selector predecesor se emplea para seleccionar elementos que en el código HTML de la página se encuentran precedidos de otros elementos. Su sintaxis emplea el signo \~ para separar los dos elementos.

```css
elementoPredecesor ~ elementoSeleccionado { ... }
```

En este selector se deben cumplir dos reglas básicas:

* El _**elementoPredecesor**_ y el _**elementoSeleccionado**_ son hermanos, es decir, tienen el mismo padre y por tanto se encuentran al mismo nivel.
* El _**elementoSeleccionado**_ debe aparecer precedido del _**elementoPredecesor**_, pero no tiene por qué ser el anterior (como ocurre con el selector adyacente).

Veamos un ejemplo de su uso:

```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <style>
      h2 { color: green; }
      h1 ~ h2 { color: red }
    </style>
  </head>
  <body>
    <h1>SMR</h1>
    <h2>Profesorado</h2>
    ...
    <h2>Alumnado</h2>
    ...
  </body>
</html>
```

Las reglas CSS anteriores hacen que todos los `<`<mark style="color:green;">**`h2`**</mark>`>` de la página se vean de color verde, salvo aquellos `<`<mark style="color:green;">**`h2`**</mark>`>` que se encuentran precedidos por cualquier elemento `<`<mark style="color:green;">**`h1`**</mark>`>` y que se muestran de color rojo. Así pues, en nuestro ejemplo tanto `"`<mark style="color:red;">**`Profesorado`**</mark>`"` como `"`<mark style="color:red;">**`Alumnado`**</mark>`"` aparecerían de color rojo, ya que ambos son precedidos por el elemento `<`<mark style="color:green;">**`h1`**</mark>`>`**`SMR`**`<`<mark style="color:green;">**`/h1`**</mark>`>`.

### Selector de Atributo

Los selectores de atributos permiten seleccionar elementos HTML en función de sus atributos y/o valores de esos atributos.

Los cuatro tipos de selectores de atributos son:

* **`[`**<mark style="color:green;">**`nombre_atributo`**</mark>**`]`**: selecciona los elementos que tienen establecido el atributo llamado `nombre_atributo`, independientemente de su valor.
* **`[`**<mark style="color:green;">**`nombre_atributo`**</mark>**`=`**<mark style="color:orange;">**`valor`**</mark>**`]`**: selecciona los elementos que tienen establecido un atributo llamado `nombre_atributo` con un valor igual a `valor`.
* **`[`**<mark style="color:green;">**`nombre_atributo`**</mark>**`~=`**<mark style="color:orange;">**`valor`**</mark>**`]`**: selecciona los elementos que tienen establecido un atributo llamado `nombre_atributo` y al menos uno de los valores del atributo es `valor`.
* **`[`**<mark style="color:green;">**`nombre_atributo`**</mark>**`^=`**<mark style="color:orange;">**`valor`**</mark>**`]`**: selecciona los elementos que tienen establecido un atributo llamado `nombre_atributo` y cuyo valor empieza por `valor`.
* **`[`**<mark style="color:green;">**`nombre_atributo`**</mark>**`$=`**<mark style="color:orange;">**`valor`**</mark>**`]`**: selecciona los elementos que tienen establecido un atributo llamado `nombre_atributo` y cuyo valor acaba en `valor`.
* **`[`**<mark style="color:green;">**`nombre_atributo`**</mark>**`*=`**<mark style="color:orange;">**`valor`**</mark>**`]`**: selecciona los elementos que tienen establecido un atributo llamado `nombre_atributo` y en cuyo valor se encuentra la subcadena `valor`.
* **`[`**<mark style="color:green;">**`nombre_atributo`**</mark>**`|=`**<mark style="color:orange;">**`valor`**</mark>**`]`**: selecciona los elementos que tienen establecido un atributo llamado `nombre_atributo` y cuyo valor es una serie de palabras separadas con guiones, pero que comienza con `valor`. Este tipo de selector es útil para los atributos de tipo **`lang`** que indican el idioma del contenido del elemento.

\
A continuación se muestran algunos ejemplos de selectores de atributo:

```css
/* Se muestran de color azul todos los enlaces que tengan un atributo "class", independientemente de su valor */
a[class] { color: blue; }

/* Se muestran de color azul todos los enlaces que tengan un atributo "class" con el valor "externo" */
a[class="externo"] { color: blue; }

/* Se muestran de color azul todos los enlaces que apunten al sitio "http://www.ejemplo.com" */
a[href="http://www.ejemplo.com"] { color: blue; }

/* Se muestran de color azul todos los enlaces que tengan un atributo "class" en el que al menos uno de sus valores sea "externo" */
a[class~="externo"] { color: blue; }

/* Se muestran de color azul todos los enlaces que empleen protocolo https (no los que usen http) */
a[href^="https"] { color: blue; }

/* Se muestran de color azul todos los enlaces cuya ruta acabe en ".es" */
a[href$=".es"] { color: blue; }

/* Se muestran de color azul todos los enlaces que contengan en su ruta la palabra "educem" */
a[href*="educem"] { color: blue; }

/* Selecciona todos los elementos de la página cuyo atributo "lang" sea igual a "en", es decir, todos los elementos en inglés */
*[lang=en] { ... }

/* Selecciona todos los elementos de la página cuyo atributo "lang" empiece por "es", es decir, "es", "es-ES", "es-AR", etc. */
*[lang|="es"] { color : red }
```

{% hint style="info" %}
Para una lista completa de todos los posibles selectores puedes consultar la referencia del [W3Schools](https://www.w3schools.com/cssref/css_selectors.asp).
{% endhint %}
