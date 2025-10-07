# Flotación

La propiedad <mark style="color:blue;">**`float`**</mark> permite hacer flotar un elemento. Los elementos a continuación de un elemento flotante, fluyen a su alrededor. Esto se puede impedir mediante el uso de la propiedad <mark style="color:blue;">**`clear`**</mark>. Cabe señalar que los elementos posicionados de manera absoluta ignoran el valor de esta propiedad.\
Las palabras reservadas que se admiten como posibles valores para la propiedad son las siguientes:

* <mark style="color:orange;">**`none`**</mark> : El elemento no flota. Valor por defecto.
* <mark style="color:orange;">**`left`**</mark> : El elemento flota a la izquierda de su contenedor.
* <mark style="color:orange;">**`right`**</mark> : El elemento flota a la derecha de su contenedor.

Veamos algunos ejemplos de uso:

```html
<!DOCTYPE html>
<html>
<head>
    <style>
        .caja {
            color: white;
            border: 1px solid black;
            height: 30px;
            width: 200px;
            padding: 10px;
            text-align: center;
        }
        .normal {
            background-color: teal;
        }
        /* Flotación a la izquierda */
        .flotanteL {
            background-color: darkblue;
            float: left;
        }
        /* Flotación a la derecha */
        .flotanteR {
            background-color: darkred;
            float: right;
        }
        /* Eliminamos el efecto de flotación a la izquierda */
        #noFlota7 {
            clear: left;
            background-color: darkgreen;
        }
    </style>
</head>
<body>
    <div class="normal caja">NO FLOTANTE #1</div>
    <div class="normal caja">NO FLOTANTE #2</div>
    <div class="flotanteL caja">FLOTANTE IZQUIERDA #1</div>
    <div class="flotanteL caja">FLOTANTE IZQUIERDA #2</div>
    <div class="normal caja">NO FLOTANTE #3</div>
    <div class="normal caja">NO FLOTANTE #4</div>
    <div class="flotanteR caja">FLOTANTE DERECHA #1</div>
    <div class="flotanteR caja">FLOTANTE DERECHA #2</div>
    <div class="normal caja">NO FLOTANTE #5</div>
    <div class="normal caja">NO FLOTANTE #6</div>
    <div class="flotanteL caja">FLOTANTE IZQUIERDA #3</div>
    <div class="flotanteL caja">FLOTANTE IZQUIERDA #4</div>
    <div id="noFlota7" class="normal caja">NO FLOTANTE #7 (CLEAR)</div>
    <div class="normal caja">NO FLOTANTE #8</div>
</body>
</html>
```

{% embed url="https://cdpn.io/dgonzalez55/fullpage/KKwGoQB?anon=true&view=fullpage" %}

{% hint style="info" %}
La propiedad <mark style="color:blue;">**float**</mark> es especialmente útil para la creación de menús y la organización del _layout_ de la web, por lo que se recomienda encarecidamente la consulta de los [ejemplos de flotación del W3Schools](https://www.w3schools.com/css/css_float.asp)
{% endhint %}

### Cancelar la flotación

La propiedad <mark style="color:blue;">**`clear`**</mark> permite establecer en qué lados del elemento seleccionado no se permite la aparición de elementos flotantes, contrarestando así los efectos de la flotación.\
Las palabras reservadas que se admiten como posibles valores para la propiedad son las siguientes:

* <mark style="color:orange;">**`none`**</mark> : Se permiten elementos flotantes a ambos lados. Valor por defecto.
* <mark style="color:orange;">**`left`**</mark> : No se permiten elementos flotantes a la izquierda del elemento.
* <mark style="color:orange;">**`right`**</mark> : No se permiten elementos flotantes a la derecha del elemento.
* <mark style="color:orange;">**`both`**</mark> : No se permiten elementos flotantes en ambos lados.

Veamos algunos ejemplos de uso:

```css
/* Las imágenes flotan a la izquierda */
img {
  float: left;
}
/* Los párrafos de tipo clear no permiten la flotación de elementos en ninguno de sus lados, lo que impedirá que las imágenes floten a su izquierda, desplazando el texto a la derecha */
p.clear {
  clear: both;
}
```

{% hint style="warning" %}
Esta propiedad debería utilizarse siempre en elementos que no deban flotar y que aparezcan tras los elementos flotantes, de esta forma, se asegura el correcto control de flujo de renderizado
{% endhint %}

{% hint style="info" %}
Existe un truco llamado **Clearfix Hack** que permite corregir el problema de que si un elemento flotante es más alto que su contenedor éste sobresalga del mismo.\
**Clearfix Hack** consigue que el elemento contenedor se redimensione impidiendo que el elemento flotante sobresalga. Puedes ver un ejemplo de dicho truco en: [Ejemplo de uso de Clearfix Hack](https://www.w3schools.com/howto/howto_css_clearfix.asp)
{% endhint %}
