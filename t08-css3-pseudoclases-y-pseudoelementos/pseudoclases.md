# Pseudoclases

Las pseudoclases sirven para establecer estilos para determinados estados especiales de los elementos seleccionados, como por ejemplo dar un estilo específico al pasar el ratón por encima de un determinado elemento, modificar el color de la fuente tras visitar un enlace o modificar las propiedades de un control cuando éste recibe el foco.\


La sintaxi de una pseudoclase es:

```css
selector:pseudoclase {
  propiedad:valor;
}
```

A continuación repasaremos algunas de las pseudoclases más utilizadas.

{% hint style="info" %}
La lista completa de pseudoclases se puede consultar en la: [lista completa de pseudoclases del W3Schools](https://www.w3schools.com/css/css_pseudo_classes.asp)
{% endhint %}

### Pseudoclases para Enlaces

#### :visited

La pseudoclase <mark style="color:purple;">**`:visited`**</mark>permite aplicar estilo a los enlaces que se hayan visitado.

Veamos un ejemplo de aplicación:

```css
/* Cambia el color de fondo a rojo de los enlaces visitados */
a:visited {
  background-color:red;
}
```

{% hint style="danger" %}
Los navegadores limitan los estilos que se pueden aplicar mediante este selector por razones de seguridad
{% endhint %}

#### :link

La pseudoclase <mark style="color:purple;">**`:link`**</mark>permite aplicar estilo a los enlaces que no se hayan visitado.

Veamos un ejemplo de aplicación:

```css
/* Cambia el color de fondo a rojo de los enlaces no visitados */
a:link {
  background-color:red;
}
```

### Pseudoclases para Eventos

#### :hover

La pseudoclase <mark style="color:purple;">**`:hover`**</mark> permite aplicar estilo al elemento seleccionado cuando se pasa el ratón por encima del mismo.

Veamos un ejemplo de aplicación:

```css
/* Cambia el color de fondo a amarillo de los enlaces cuando el ratón se desliza por encima de los mismos */
a:hover {
  background-color: yellow;
}
```

{% hint style="danger" %}
<mark style="color:purple;">**:hover**</mark> debe ir siempre tras <mark style="color:purple;">**:link**</mark> y <mark style="color:purple;">**:visited**</mark> (si aparecen) para que sea efectivo.
{% endhint %}

#### :active

La pseudoclase <mark style="color:purple;">**`:active`**</mark> permite aplicar estilo al elemento seleccionado cuando éste se vuelve activo (se le hace _click_).

Veamos un ejemplo de aplicación:

```css
/* Cambia el color de fondo a rojo del texto dentro de la etiqueta span cuando se hace click sobre el mismo */
span:active {
  background-color:red;
}
```

{% hint style="danger" %}
<mark style="color:purple;">**:active**</mark> debe ir siempre tras <mark style="color:purple;">**:hover**</mark> (si aparece) para que sea efectivo.
{% endhint %}

#### :focus

La pseudoclase <mark style="color:purple;">**`:focus`**</mark> permite aplicar estilo al elemento seleccionado cuando éste recibe el foco. Solo funciona sobre los elementos que pueden recibir el foco tales como controles, botones, etc.

Veamos un ejemplo de aplicación:

```css
/* Cambia el color de fondo a amarillo cuando el control (input) recibe el foco */
input:focus {
  background-color: yellow;
}
```

### Pseudoclases para Controles

#### :checked

La pseudoclase <mark style="color:purple;">**`:checked`**</mark>permite aplicar estilo al `<`<mark style="color:green;">**`input`**</mark>`>` seleccionado cuando el estado del mismo pasa a tener el valor <mark style="color:orange;">**checked**</mark>.

Veamos un ejemplo de aplicación:

```css
/* Modifica el tamaño de los inputs (radio o checkbox) cuando se encuentran en estado checked */
input:checked {
  height: 50px;
  width: 50px;
}
```

#### :required

La pseudoclase <mark style="color:purple;">**`:required`**</mark>permite aplicar estilo al `<`<mark style="color:green;">**`input`**</mark>`>`seleccionado cuando este sea de tipo obligatorio y por tanto tenga el atributo <mark style="color:orange;">**required**</mark>.

Veamos un ejemplo de aplicación:

```css
/* Modifica el color del texto a rojo para los inputs obligatorios */
input:required {
  color: red;
}
```

#### :optional

La pseudoclase <mark style="color:purple;">**`:optional`**</mark>permite aplicar estilo al `<`<mark style="color:green;">**`input`**</mark>`>`seleccionado cuando este sea de tipo opcional y no tenga por tanto el atributo <mark style="color:orange;">**required**</mark>.

Veamos un ejemplo de aplicación:

```css
/* Modifica el color del texto a azul para los inputs opcionales */
input:optional {
  color: blue;
}
```

### Pseudoclases de Posición

#### :first-child

La pseudoclase <mark style="color:purple;">**`:first-child`**</mark> permite aplicar estilo al elemento seleccionado que sea el primer hijo para su padre.

Veamos un ejemplo de aplicación:

```css
/* Cambia el color de fondo a amarillo para los párrafos que sean el primer hijo de su padre */
p:first-child {
  background-color: yellow;
}
```

#### :first-of-type

La pseudoclase <mark style="color:purple;">**`:first-of-type`**</mark> permite aplicar estilo al elemento seleccionado que sea el primero hijo de su tipo para su padre.

Veamos un ejemplo de aplicación:

```css
/* Cambia el color de fondo a amarillo para los párrafos que sean el primer hijo de tipo para su padre */
p:first-of-type {
  background-color: yellow;
}
```

#### :last-child

La pseudoclase <mark style="color:purple;">**`:last-child`**</mark> permite aplicar estilo al elemento seleccionado que sea el último hijo para su padre.

Veamos un ejemplo de aplicación:

```css
/* Cambia el color de fondo a amarillo para los párrafos que sean el último hijo de su padre */
p:last-child {
  background-color: yellow;
}
```

#### :last-of-type

La pseudoclase <mark style="color:purple;">**`:last-of-type`**</mark> permite aplicar estilo al elemento seleccionado que sea el último hijo de su tipo para su padre.

Veamos un ejemplo de aplicación:

```css
/* Cambia el color de fondo a amarillo para los párrafos que sean el último hijo de tipo para su padre */
p:last-of-type {
  background-color: yellow;
}
```

#### :nth-child(n)

La pseudoclase <mark style="color:purple;">**`:nth-child(`**</mark><mark style="color:green;">**`n`**</mark><mark style="color:purple;">**`)`**</mark> permite aplicar estilo al elemento seleccionado que sea el n hijo para su padre.

Veamos un ejemplo de aplicación:

```css
/* Cambia el color de fondo a amarillo para los párrafos que sean el tercer hijo de su padre */
p:nth-child(3) {
  background-color: yellow;
}
```

#### :nth-of-type(n)

La pseudoclase <mark style="color:purple;">**`:nth-of-type(`**</mark><mark style="color:green;">**`n`**</mark><mark style="color:purple;">**`)`**</mark>  permite aplicar estilo al elemento seleccionado que sea el n hijo de su tipo para su padre.

Veamos un ejemplo de aplicación:

```css
/* Cambia el color de fondo a amarillo para los párrafos que sean el segundo hijo de tipo para su padre */
p:nth-of-type(2) {
  background-color: yellow;
}
```

### Pseudoclase Inversa

#### :not(selector)

La pseudoclase <mark style="color:purple;">**`:not(`**</mark><mark style="color:green;">**`selector`**</mark><mark style="color:purple;">**`)`**</mark> permite aplicar estilo a los elementos que no sean seleccionados por el selector indicado en la pseudoclase.

Veamos un ejemplo de aplicación:

```css
/* Cambia el color del texto a rojo para todos los elementos que no sean anchors */
:not(a) {
  color:red;
}
```
