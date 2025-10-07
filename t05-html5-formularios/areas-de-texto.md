# Áreas de texto

### Entrada de datos: `<`<mark style="color:green;">`textarea`</mark>`>`

Este elemento es requerido en el caso de que deseemos que los usuarios nos puedan hacer llegar un texto de varias linias.

```html
<textarea name=observaciones rows="10" cols="100">
Lorem ipsum dolor sit amet consectetur adipiscing elit nostra vel, vitae aptent aliquam fames blandit metus dictumst semper nam congue, vestibulum orci sociis ullamcorper libero curabitur augue primis. Gravida non vestibulum iaculis ullamcorper ante erat tellus felis, nullam scelerisque commodo eget vel tempor nulla nascetur faucibus, porttitor suscipit dis rhoncus condimentum tortor primis. Eget pulvinar iaculis fames tristique commodo cras integer nisi rutrum augue odio, eleifend consequat ad non et class nullam pellentesque ante.

Torquent vehicula auctor iaculis natoque potenti proin, massa sodales libero inceptos cubilia dis, velit viverra blandit tempus nulla. Interdum neque fusce malesuada posuere aliquam integer consequat cum ut tellus commodo sem cras, sapien himenaeos ridiculus ornare elementum vestibulum ultrices accumsan aptent vulputate etiam. Scelerisque eu urna condimentum hendrerit viverra platea pellentesque orci, nisi magna congue iaculis odio faucibus ligula fames laoreet, vel accumsan eros curae consequat cras convallis.
</textarea>
```

{% embed url="https://cdpn.io/dgonzalez55/fullpage/XWJrqJP?anon=true&view=fullpage" %}

Veamos sus principales atributos:

* **`rows`** : Cantidad de linias de texto que se mostrarán
* **`cols`** : Cantidad de columnas de texto que se mostrarán.
* **`maxlength`** : Número máximo de caracteres que se admiten.
* **`placeholder`** : Texto de ayuda que aparece sobre el componente para indicarle al usuario los valores que se deben introducir.
* **`readonly`** : Indica que el valor existente en el formulario no se puede editar.
* **`required`** : Especifica que el formulario no se puede enviar a menos que se rellene el campo de entrada. Por tanto, el campo pasa a ser obligatorio.
* **`autofocus`** : El control de entrada recibe el foco al cargarse la página. Solo se admite un autofocus por página web.
