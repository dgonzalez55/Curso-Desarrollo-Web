# Posicionamiento

La propiedad <mark style="color:blue;">**`position`**</mark> permite establecer el método de posicionamiento del elemento seleccionado.\
Las palabras reservadas que se admiten como posibles valores para la propiedad son las siguientes:

* <mark style="color:orange;">**`static`**</mark> : El elemento se renderiza conforme al flujo de aparición. Valor por defecto.
* <mark style="color:orange;">**`absoulte`**</mark> : El elemento se renderiza conforme a las coordenadas indicadas relativas a la posición del primer elemento antecesor cuyo posicionamiento no sea _static_.
* <mark style="color:orange;">**`relative`**</mark> : El elemento se renderiza conforme a las coordenadas indicadas relativas a su posición por defecto.
* <mark style="color:orange;">**`fixed`**</mark> : El elemento se renderiza conforme a las coordenadas indicadas relativas a la ventana del navegador.

Veamos algunos ejemplos de uso:

```css
/* La Box1 se posicionará conforme al flujo de ejecución (valor por defecto) */
#Box1 {
    position: static;
}
/* La Box2 se posicionará 50 píxeles por debajo y 10 píxeles a la izquierda de la posición inicial (0,0) de su primer antecesor no estático */
#Box2 {
    position: absolute;
    top: 50px;
    left: 10px;
}
/* La Box3 se posicionará 50 píxeles por debajo y 10 píxeles a la izquierda de su posición inicial */
#Box3 {
    position: relative;
    top: 50px;
    left: 10px;
}
/* La Box4 se fijará en la posición 50 píxeles por debajo y 10 píxeles a la izquierda de la posición inicial (0,0) de la ventana del navegador */
#Box4 {
    position: fixed;
    top: 50px;
    left: 10px;
}
```

{% embed url="https://cdpn.io/dgonzalez55/fullpage/jOEeZRw?anon=true&view=fullpage" %}

{% hint style="danger" %}
Si un elemento se posiciona de manera absoluta y todos sus antecesores (contenedores) se posicionan de forma estática, el elemento se posicionará relativo a las coordenadas absolutas de la pantalla.
{% endhint %}
