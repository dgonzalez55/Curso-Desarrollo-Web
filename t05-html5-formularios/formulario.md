# Formulario

### Formulario: `<`<mark style="color:green;">`form`</mark>`>`

Para agrupar todos los controles de entrada y envío de datos, HTML utiliza la etiqueta `<`<mark style="color:green;">**`form`**</mark>`>` para encapsular la entrada y el envío. El elemento `<`<mark style="color:green;">**`form`**</mark>`>` realiza el envío de datos a través del **method** especificado hacia la página gestionada por un servidor o controlador que se indica en el atributo **action**. En resumen, todos los elementos de un formulario deben estar contenidos dentro de una estructura `<`<mark style="color:green;">**`form`**</mark>`>`. Un posible ejemplo de ello sería el siguiente formulario básico de login:

```html
  <form action="./login.php" method="POST">
    <!-- Aquí deben ir los controles del formulario, incluyendo los botones de envío -->
    <p>
      <label for="user"><b>Usuario</b></label>
      <input id="user" type="text" placeholder="Introduce tu usuario" name="uname" required>
    </p>
    <p>
      <label for="pwd"><b>Contraseña</b></label>
      <input id="pwd" type="password" placeholder="Introduce tu contraseña" name="password" required>
    </p>
    <p>
      <button type="submit">Login</button>
    </p>
  </form>
```

{% embed url="https://cdpn.io/dgonzalez55/fullpage/VwYZMqX?anon=true&view=fullpage" %}

Analizemos ahora sus principales atributos:

* **`action`** : Permite especificar la URL del fichero responsable de procesar los datos. En la mayoría de casos se tratará de un fichero PHP.
* **`method`** : Permite especificar como se realiza el envío de la información al servior.
  * <mark style="color:blue;">**GET**</mark> : Se utiliza la propia URL para enviar la información al servidor, por lo que los datos viajan en claro y se permite el envío directo sin necesidad de utilizar los controles del formulario. Su uso debería limitarse a formularios de búsqueda o similares que sirvan para consultar datos y en los cuáles no se introduzca información sensible.
  * <mark style="color:blue;">**POST**</mark> : Es el método habitual para enviar la información introducida por el usuario al servidor. En este caso el envío se realiza por un canal de comunicación interno y la información no es visible por parte del usuario. Su uso es el recomendado para la mayoría de formularios.
* **`enctype`** : Permite indicar cómo se deben codificar los datos cuando estos se envían al servidor (solo aplica para el método <mark style="color:blue;">**POST**</mark>)
  * **application/x-www-form-urlencoded** : Es el valor por defecto, convierte los espacios en blanco en "+" y recodifica los caracteres especiales a su valor ASCII en hexadecimal.
  * **multipart/form-data** : No se recodifican los caracteres. Debe emplearse cuando en el formulario se suban ficheros.
  * **text/plain** : Los espacios en blanco se convierten en "+" pero no se recodifican caracteres especiales. Debería evitarse este método a ser posible.
* **`autocomplete`** : Permite activar o desactivar la función de autocompletar en los campos contenidos en el formulario. Por defecto el valor es "on".
* **`novalidate`** : Permite desactivar la función de validación automática de los campos contenidos en el formulario.
* **`name`** : Indica el nombre del formulario.
* **`target`** : Especifica dónde debe mostrarse la respuesta que se reciba después enviar el formulario. Su uso es equivalente al visto en la etiqueta `<`<mark style="color:green;">**`a`**</mark>`>`.

{% hint style="danger" %}
Utilizar el método <mark style="color:blue;">**GET**</mark> para el envío de información al servidor es un error y supone un fallo de seguridad dado que la información se transmite en claro a través de la URL, por lo que cualquier dato sensible se revela al instante.
{% endhint %}

{% hint style="info" %}
Para la gran mayoría de los formularios nos bastará con indicar el **`action`** y el **`method`**, pues el valor por defecto del resto de atributos suele ser el conveniente.
{% endhint %}
