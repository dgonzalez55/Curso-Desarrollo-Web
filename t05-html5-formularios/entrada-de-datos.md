# Entrada de datos

<details>

<summary>SUMARIO</summary>

[#entrada-para-texto-less-than-input-type-text-greater-than](entrada-de-datos.md#entrada-para-texto-less-than-input-type-text-greater-than "mention")

[#entrada-para-contrasenas-less-than-input-type-password-greater-than](entrada-de-datos.md#entrada-para-contrasenas-less-than-input-type-password-greater-than "mention")

[#entrada-para-emails-less-than-input-type-email-greater-than](entrada-de-datos.md#entrada-para-emails-less-than-input-type-email-greater-than "mention")

[#entrada-para-ficheros-less-than-input-type-file-greater-than](entrada-de-datos.md#entrada-para-ficheros-less-than-input-type-file-greater-than "mention")

[#entrada-para-colores-less-than-input-type-color-greater-than](entrada-de-datos.md#entrada-para-colores-less-than-input-type-color-greater-than "mention")

[#entrada-para-telefonos-less-than-input-type-tel-greater-than](entrada-de-datos.md#entrada-para-telefonos-less-than-input-type-tel-greater-than "mention")

[#entrada-para-fechas-less-than-input-type-date-greater-than](entrada-de-datos.md#entrada-para-fechas-less-than-input-type-date-greater-than "mention")

[#entrada-para-fechas-y-horas-less-than-input-type-datetime-local-greater-than](entrada-de-datos.md#entrada-para-fechas-y-horas-less-than-input-type-datetime-local-greater-than "mention")

[#entrada-para-urls-less-than-input-type-url-greater-than](entrada-de-datos.md#entrada-para-urls-less-than-input-type-url-greater-than "mention")

[#entrada-para-valores-numericos-less-than-input-type-number-greater-than](entrada-de-datos.md#entrada-para-valores-numericos-less-than-input-type-number-greater-than "mention")

[#entrada-para-rangos-numericos-less-than-input-type-range-greater-than](entrada-de-datos.md#entrada-para-rangos-numericos-less-than-input-type-range-greater-than "mention")

[#casillas-de-verificacion-less-than-input-type-checkbox-greater-than](entrada-de-datos.md#casillas-de-verificacion-less-than-input-type-checkbox-greater-than "mention")

[#selectores-less-than-input-type-radio-greater-than](entrada-de-datos.md#selectores-less-than-input-type-radio-greater-than "mention")

[#boton-de-envio-de-formulario-less-than-input-type-submit-greater-than](entrada-de-datos.md#boton-de-envio-de-formulario-less-than-input-type-submit-greater-than "mention")

[#boton-de-reinicio-de-formulario-less-than-input-type-reset-greater-than](entrada-de-datos.md#boton-de-reinicio-de-formulario-less-than-input-type-reset-greater-than "mention")

[#boton-generico-less-than-input-type-button-greater-than](entrada-de-datos.md#boton-generico-less-than-input-type-button-greater-than "mention")

[#etiquetas-less-than-label-greater-than](entrada-de-datos.md#etiquetas-less-than-label-greater-than "mention")

</details>

### Entrada de datos: `<`<mark style="color:green;">`input`</mark>`>`

Un componente clave de los formularios, son los controles de entrada de datos gestionados mediante la etiqueta `<`<mark style="color:green;">**`input`**</mark>`>`. Los diferentes tipos de elementos de entrada pueden regular los datos ingresados para ajustarse a un formato específico y proporcionar seguridad adicional en la entrada de una contraseña por ejemplo.

```html
<input>
```

Antes de revisar los diferentes controles `<`<mark style="color:green;">**`input`**</mark>`>` que podemos utilizar, veamos los principales atributos que todos tienen en común:

* **`id`** : Identificador HTML, necesario para poder vincular el control de entrada con su etiqueta **`label`** como se verá más adelante.
* **`name`** : Nombre del control de entrada, <mark style="color:red;">**imprescindible**</mark> añadirlo para después poder relacionar y procesar correctamente los datos recibidos.
* **`disabled`** : Permite deactivar el control, aunque continúa siendo visible por parte del usuario.
* **`checked`** : Útil para los controles de entrada de tipo radio o checkbox, ya que indica que el control está seleccionado por defecto. Para el resto de controles de entrada se ignora.
* **`placeholder`** : Texto de ayuda que aparece sobre el componente para indicarle al usuario los valores que se deben introducir.
* **`autocomplete`** : análogo al visto para el elemento `<`<mark style="color:green;">**`form`**</mark>`>`.
* **`readonly`** : Indica que el valor existente en el formulario no se puede editar.
* **`required`** : Especifica que el formulario no se puede enviar a menos que se rellene el campo de entrada. Por tanto, el campo pasa a ser obligatorio.
* **`autofocus`** : El control de entrada recibe el foco al cargarse la página. Solo se admite un autofocus por página web.
* **`value`** : Contiene el valor introducido. Útil para facilitar valores por defecto al usuario.

### Entrada para texto: `<`<mark style="color:green;">`input`</mark>` `<mark style="color:purple;">`type`</mark>`="`<mark style="color:orange;">`text`</mark>`" >`

```html
<input type="text" id="idNombre" name="nombre" placeholder="Introduce tu nombre" autofocus size="50" maxlength="100">
```

{% embed url="https://cdpn.io/dgonzalez55/fullpage/KKwPZMZ?anon=true&view=fullpage" %}

Mediante `<`<mark style="color:green;">**`input`**</mark>**` `**<mark style="color:purple;">**`type`**</mark>**`="`**<mark style="color:orange;">**`text`**</mark>**`"`**`>` se solicita la entrada de una cadena de texto. En un formulario de login, serviría para solicitar el nombre del usuario (que no el mail). Solo se permite una línea de texto. Para limitar la longitud del campo de entrada y el máximo de caracteres que se admiten se deben usar los siguientes atributos:

* **`size`** : Especifica la longitud del recuadro del campo de entrada en número de caracteres. Por defecto es de 20 caracteres. El valor de este atributo no limita el número máximo de caracteres que el usuario puede introducir.
* **`maxlength`** : Especifica el número máximo de caracteres que el usuario puede introducir como valor del campo. Por defecto es de 524288 caracteres.
* **`minlength`** : Especifica el número mínimo de caracteres que el usuario debe introducir como valor del campo. Por defecto es de 0 caracteres.

### Entrada para contraseñas: `<`<mark style="color:green;">`input`</mark>` `<mark style="color:purple;">`type`</mark>`="`<mark style="color:orange;">`password`</mark>`" >`

```html
<input type="password" id="idPass" name="password" placeholder="Introduce tu contraseña" size="10" maxlength="16" value="Educem00.">
```

{% embed url="https://cdpn.io/dgonzalez55/fullpage/VwYZQKW?anon=true&view=fullpage" %}

Mediante `<`<mark style="color:green;">**`input`**</mark>**` `**<mark style="color:purple;">**`type`**</mark>**`="`**<mark style="color:orange;">**`password`**</mark>**`"`**`>` se solicita la entrada de una cadena de texto que debe ocultarse al usuario. En un formulario de login, serviría para solicitar la contraseña del usuario. Solo se permite una línea de texto. Para limitar la longitud del campo de entrada y el máximo de caracteres que se admiten se deben usar los siguientes atributos:

* **`size`** : Especifica la longitud del recuadro del campo de entrada en número de caracteres. Por defecto es de 20 caracteres. El valor de este atributo no limita el número máximo de caracteres que el usuario puede introducir.
* **`maxlength`** : Especifica el número máximo de caracteres que el usuario puede introducir como valor del campo. Por defecto es de 524288 caracteres.
* **`minlength`** : Especifica el número mínimo de caracteres que el usuario debe introducir como valor del campo. Por defecto es de 0 caracteres.

{% hint style="warning" %}
Si en un formulario con el campo `<`<mark style="color:green;">**`input`**</mark>**` `**<mark style="color:purple;">**`type`**</mark>**`="`**<mark style="color:orange;">**`password`**</mark>**`"`**`>` editamos desde el navegador el código web para modificar el tipo del campo a `<`<mark style="color:green;">**`input`**</mark>**` `**<mark style="color:purple;">**`type`**</mark>**`="`**<mark style="color:orange;">**`text`**</mark>**`"`**`>` obtendremos automáticamente en claro la cadena oculta.
{% endhint %}

### Entrada para emails: `<`<mark style="color:green;">`input`</mark>` `<mark style="color:purple;">`type`</mark>`="`<mark style="color:orange;">`email`</mark>`" >`

```html
<input type="email" id="idEmail" name="correo" placeholder="Introduce tu correo electrónico">
```

{% embed url="https://cdpn.io/dgonzalez55/fullpage/ExaYQWK?anon=true&view=fullpage" %}

Mediante `<`<mark style="color:green;">**`input`**</mark>**` `**<mark style="color:purple;">**`type`**</mark>**`="`**<mark style="color:orange;">**`email`**</mark>**`"`**`>` se solicita la introducción de una dirección de correo electrónico válida. Una dirección de correo electrónico válida debe cumplir con el formato _<mark style="color:blue;">nombre\_cuenta@dominio\_web</mark>_. Para limitar la longitud del campo de entrada y el máximo de caracteres que se admiten se deben usar los siguientes atributos:

* **`size`** : Especifica la longitud del recuadro del campo de entrada en número de caracteres. Por defecto es de 20 caracteres. El valor de este atributo no limita el número máximo de caracteres que el usuario puede introducir.
* **`maxlength`** : Especifica el número máximo de caracteres que el usuario puede introducir como valor del campo. Por defecto es de 524288 caracteres.
* **`minlength`** : Especifica el número mínimo de caracteres que el usuario debe introducir como valor del campo. Por defecto es de 0 caracteres.

{% hint style="danger" %}
La validación web se limita a verificar el formato de la cuenta de correo electrónica introducida, no se comprueba si la cuenta existe o no. Tampoco impide el uso de correos temporales, por lo que pueden requerirse verificaciones adicionales a implementar por el desarrollador web.
{% endhint %}

### Entrada para ficheros: `<`<mark style="color:green;">`input`</mark>` `<mark style="color:purple;">`type`</mark>`="`<mark style="color:orange;">`file`</mark>`" >`

```html
<p><input type="file" id="idAvatar" name="avatar" accept="image/x- png,image/gif,image/jpeg"></p>
<p><input type="file" id="idMultimedia" name="multimedia" accept="image/*,audio/*,video/*" multiple></p>
```

{% embed url="https://cdpn.io/dgonzalez55/fullpage/ZEYzrxG?anon=true&view=fullpage" %}

Mediante `<`<mark style="color:green;">**`input`**</mark>**` `**<mark style="color:purple;">**`type`**</mark>**`="`**<mark style="color:orange;">**`file`**</mark>**`"`**`>` se solicita la subida de uno o múltiples ficheros. Para limitar el tipo de archivos que se permiten subir o si se permiten múltples ficheros o no se deben usar los siguientes atributos:

* **`multiple`** : Indica que se permite la subida de múltiples ficheros.
* **`accept`** : Especifica los tipos de ficheros que se admiten en la subida. Su sintaxis es la siguiente: `accept="file_extension|audio/*|video/*|image/*|media_type"`

{% hint style="danger" %}
Si el formulario permite la subida de ficheros deberás indicar como **enctype** el valor `"`<mark style="color:purple;">**`multipart/form-data`**</mark>`".`
{% endhint %}

### Entrada para colores: `<`<mark style="color:green;">`input`</mark>` `<mark style="color:purple;">`type`</mark>`="`<mark style="color:orange;">`color`</mark>`" >`

```html
  <input id="inColor1" name="color1" type="color" value="#FFFF00">
  <input id="inColor2" name="color2" type="color" value="#00FF00">
  <input id="inColor3" name="color3" type="color" value="#FF00FF">
```

{% embed url="https://cdpn.io/dgonzalez55/fullpage/povzaQv?anon=true&view=fullpage" %}

Mediante `<`<mark style="color:green;">**`input`**</mark>**` `**<mark style="color:purple;">**`type`**</mark>**`="`**<mark style="color:orange;">**`color`**</mark>**`"`**`>` se solicita la elección de un color. Se le puede asignar un valor por defecto mediante el código RGB en hexadecimal que corresponda al color elegido. Puede resultar útil para permitir que el usuario pueda personalizar el estilo visual de la web por ejemplo.

### Entrada para télefonos: `<`<mark style="color:green;">`input`</mark>` `<mark style="color:purple;">`type`</mark>`="`<mark style="color:orange;">`tel`</mark>`" >`

```html
<input id="inPhone" name="Phone" type="tel" value="+34666334455">
```

{% embed url="https://cdpn.io/dgonzalez55/fullpage/BayBYvb?anon=true&view=fullpage" %}

Mediante `<`<mark style="color:green;">**`input`**</mark>**` `**<mark style="color:purple;">**`type`**</mark>**`="`**<mark style="color:orange;">**`tel`**</mark>**`"`**`>` se solicita la introducción de un teléfono.

### Entrada para fechas: `<`<mark style="color:green;">`input`</mark>` `<mark style="color:purple;">`type`</mark>`="`<mark style="color:orange;">`date`</mark>`" >`

```html
<input id="inFecha" name="fecha" type="date" value="2019-11-30">
```

{% embed url="https://cdpn.io/dgonzalez55/fullpage/gObYvqQ?anon=true&view=fullpage" %}

Mediante `<`<mark style="color:green;">**`input`**</mark>**` `**<mark style="color:purple;">**`type`**</mark>**`="`**<mark style="color:orange;">**`date`**</mark>**`"`**`>` se solicita la introducción de una fecha válida, habitualmente mediante un selector de tipo calendario. Los valores por defecto deben introducirse mediante la sintaxis: <mark style="color:blue;">yyyy</mark>-<mark style="color:yellow;">MM</mark>-<mark style="color:green;">dd</mark> en dónde <mark style="color:blue;">yyyy</mark> es el año, <mark style="color:yellow;">MM</mark> es el número de mes y <mark style="color:green;">dd</mark> el número de día.

### Entrada para fechas y horas: `<`<mark style="color:green;">`input`</mark>` `<mark style="color:purple;">`type`</mark>`="`<mark style="color:orange;">`datetime-local`</mark>`" >`

```html
<input id="inFechaHora" name="fechahora" type="datetime-local" value="2019-11-30T17:41">
```

{% embed url="https://cdpn.io/dgonzalez55/fullpage/mdybXgz?anon=true&view=fullpage" %}

Mediante `<`<mark style="color:green;">**`input`**</mark>**` `**<mark style="color:purple;">**`type`**</mark>**`="`**<mark style="color:orange;">**`datetime-local`**</mark>**`"`**`>` se solicita la introducción de una fecha y hora válidas, habitualmente mediante un selector de tipo calendario. Los valores por defecto deben introducirse mediante la sintaxis: <mark style="color:blue;">yyyy</mark>-<mark style="color:yellow;">MM</mark>-<mark style="color:green;">dd</mark>T<mark style="color:orange;">hh</mark>:<mark style="color:purple;">mm</mark> en dónde <mark style="color:blue;">yyyy</mark> es el año, <mark style="color:yellow;">MM</mark> es el número de mes, <mark style="color:green;">dd</mark> el número de día, <mark style="color:orange;">hh</mark> la hora y <mark style="color:purple;">mm</mark> los minutos.

{% hint style="info" %}
Este control dispone de los atributos min, max y step que permiten limitar la selección del usuario. Si te interesa, consulta la especificación.
{% endhint %}

### Entrada para urls: `<`<mark style="color:green;">`input`</mark>` `<mark style="color:purple;">`type`</mark>`="`<mark style="color:orange;">`url`</mark>`" >`

```html
<input id="inURL" name="direccionURL" type="url" placeholder="Introduce la url de tu web favorita" size="40">
```

{% embed url="https://cdpn.io/dgonzalez55/fullpage/yLyBKLO?anon=true&view=fullpage" %}

Mediante `<`<mark style="color:green;">**`input`**</mark>**` `**<mark style="color:purple;">**`type`**</mark>**`="`**<mark style="color:orange;">**`url`**</mark>**`"`**`>` se solicita la introducción de una URL válida. En el caso de introducir la dirección de una página web es necesario incluir el protocolo correspondiente, ya sea _http_ o _https_.

### Entrada para valores numéricos: `<`<mark style="color:green;">`input`</mark>` `<mark style="color:purple;">`type`</mark>`="`<mark style="color:orange;">`number`</mark>`" >`

```html
<input id="inAltura" name="altura" type="number" min="1" max="2.5" step="0.01" value="1.74">
```

{% embed url="https://cdpn.io/dgonzalez55/fullpage/eYmOMNg?anon=true&view=fullpage" %}

Mediante `<`<mark style="color:green;">**`input`**</mark>**` `**<mark style="color:purple;">**`type`**</mark>**`="`**<mark style="color:orange;">**`number`**</mark>**`"`**`>` se solicita la introducción de un valor numérico (entero o real). Para limitar los posibles valores se deben usar los siguientes atributos:

* **`min`** : Indica el valor mínimo permitido.
* **`max`** : Indica el valor máximo permitido.
* **`step`** : Indica el valor numérico de los incrementos que realizará el control cuando sea accionado por el usuario.

{% hint style="danger" %}
El separador decimal que debes emplear es el "." y no la "," aunque en el navegador veas los decimales con el símbolo de la ",".
{% endhint %}

### Entrada para rangos numéricos: `<`<mark style="color:green;">`input`</mark>` `<mark style="color:purple;">`type`</mark>`="`<mark style="color:orange;">`range`</mark>`" >`

```html
<input id="inTemperatura" name="temperatura" type="range" min="18.0" max="24.0" step="0.1" value="21.0">
```

{% embed url="https://cdpn.io/dgonzalez55/fullpage/povzLbb?anon=true&view=fullpage" %}

Mediante `<`<mark style="color:green;">**`input`**</mark>**` `**<mark style="color:purple;">**`type`**</mark>**`="`**<mark style="color:orange;">**`range`**</mark>**`"`**`>` se solicita la elección de un valor numérico, pero usando para ello un control deslizante. Para limitar los posibles valores se deben usar los siguientes atributos:

* **`min`** : Indica el valor mínimo permitido.
* **`max`** : Indica el valor máximo permitido.
* **`step`** : Indica el valor numérico de los incrementos que realizará el control cuando sea accionado por el usuario.

### Casillas de Verificación: `<`<mark style="color:green;">`input`</mark>` `<mark style="color:purple;">`type`</mark>`="`<mark style="color:orange;">`checkbox`</mark>`" >`

```html
<p>
  <input id="inEstadoCivil" name="casado" type="checkbox" checked>
  <label for="inEstadoCivil">Casado ?</label>
</p>
<p>
  <input id="inParo" name="paro" type="checkbox">
  <label for="inParo">En Paro ?</label>
</p>
```

{% embed url="https://cdpn.io/dgonzalez55/fullpage/WNbezoQ?anon=true&view=fullpage" %}

Mediante `<`<mark style="color:green;">**`input`**</mark>**` `**<mark style="color:purple;">**`type`**</mark>**`="`**<mark style="color:orange;">**`checkbox`**</mark>**`"`**`>` se requiere al usuario confirmación para hialguna u otra cuestión a través de la marca de una casilla de verificación. Para marcar por defecto una casilla de verificación, deberá añadirse a la misma el atributo **`checked`**.

{% hint style="info" %}
Considera el uso del elemento `<`<mark style="color:green;">**`label`**</mark>`>` para mejorar la accesibilidad de tus casillas de verificación.
{% endhint %}

### Selectores: `<`<mark style="color:green;">`input`</mark>` `<mark style="color:purple;">`type`</mark>`="`<mark style="color:orange;">`radio`</mark>`" >`

```html
<h2>Estado Civil</h2>
<p>
  <input id="inCasado" name="estadocivil" value="casado" type="radio" checked>
  <label for="inCasado">Casado</label>
</p>
<p>
  <input id="inSoltero" name="estadocivil" value="soltero" type="radio">
  <label for="inSoltero">Soltero</label>
</p>
```

{% embed url="https://cdpn.io/dgonzalez55/fullpage/YzPKaZd?anon=true&view=fullpage" %}

Mediante `<`<mark style="color:green;">**`input`**</mark>**` `**<mark style="color:purple;">**`type`**</mark>**`="`**<mark style="color:orange;">**`radio`**</mark>**`"`**`>` se requiere al usuario seleccionar una opción válida de entre un conjunto limitado. La elección se realiza mediante el click sobre el control de tipo _**radiobutton**_. Para marcar por defecto una opción, deberá añadirse a la misma el atributo **`checked`**. Para que este control funcione correctamente es imprescindible que existan un mínimo de dos opciones posibles a elegir, que todas las opciones posibles tengan el mismo valor para su atributo **`name`** y que para cada una de ellas se defina un valor diferente: **`value`**. De lo contrario el funcionamiento del componente de entrada será erróneo.

{% hint style="info" %}
Considera el uso del elemento `<`<mark style="color:green;">**`label`**</mark>`>` para mejorar la accesibilidad de tus selectores.
{% endhint %}

{% hint style="danger" %}
Si el funcionamiento no es el esperado revisa atentamente el valor asignado a los atributos **`name`** y **`value`** para los distintos selectore&#x73;_._
{% endhint %}

### Botón de envío de formulario: `<`<mark style="color:green;">`input`</mark>` `<mark style="color:purple;">`type`</mark>`="`<mark style="color:orange;">`submit`</mark>`" >`

```html
<input value="Envía el Formulario" type="submit">
```

{% embed url="https://cdpn.io/dgonzalez55/fullpage/JjoPLLB?anon=true&view=fullpage" %}

Mediante `<`<mark style="color:green;">**`input`**</mark>**` `**<mark style="color:purple;">**`type`**</mark>**`="`**<mark style="color:orange;">**`submit`**</mark>**`"`**`>` se presenta un botón que permitirá enviar los datos de un determinado formulario hacia el servidor web, desencadenando la acción definida en el atributo **`action`** del propio `<`<mark style="color:green;">**`form`**</mark>`>`. El texto que aparece en el botón se puede indicar a través del valor del atributo **`value`**. Todo formulario debería contar con este componente.

### Botón de reinicio de formulario: `<`<mark style="color:green;">`input`</mark>` `<mark style="color:purple;">`type`</mark>`="`<mark style="color:orange;">`reset`</mark>`" >`

```html
<input value="Limpia el Formulario!" type="reset">co
```

{% embed url="https://cdpn.io/dgonzalez55/fullpage/XWJrEzz?anon=true&view=fullpage" %}

Mediante `<`<mark style="color:green;">**`input`**</mark>**` `**<mark style="color:purple;">**`type`**</mark>**`="`**<mark style="color:orange;">**`reset`**</mark>**`"`**`>` se presenta un botón que permitirá resetear todos los campos de un determinado formulario al valor por defecto. El texto que aparece en el botón se puede indicar a través del valor del atributo **`value`**. No se aconseja su utilización pues puede frustrar a los usuarios en caso de clickarlo por error.

### Botón genérico: `<`<mark style="color:green;">`input`</mark>` `<mark style="color:purple;">`type`</mark>`="`<mark style="color:orange;">`button`</mark>`" >`

```html
<input type="button" value="Tocamela otra vez Sam" onclick="alert('Oh yeah!');">
```

{% embed url="https://cdpn.io/dgonzalez55/fullpage/wvBwmxM?anon=true&view=fullpage" %}

Mediante `<`<mark style="color:green;">**`input`**</mark>**` `**<mark style="color:purple;">**`type`**</mark>**`="`**<mark style="color:orange;">**`button`**</mark>**`"`**`>` se presenta un botón genérico que puede usarse para desencadenar la ejecución de un script predeterminado. El texto que aparece en el botón se puede indicar a través del valor del atributo **`value`**.

### Etiquetas: `<`<mark style="color:green;">`label`</mark>`>`

Este elemento debería acompañar en la medida de lo posible los diferentes campos de entrada de información, pues al enlazarse con estos mejora exponencialmente la accesibilidad del formulario.

```html
  <label for="inUser">Usuario:</label>
  <input id="inUser" name="user" type="text">
  <br>
  <label for="inPasswd">Contraseña:</label>
  <input id="inPasswd" name="passwd" type="password">
  <br>
  <label for="inRemember">Recordar contraseña:</label>
  <input id="inRemember" name="remember" type="checkbox" checked>
```

{% embed url="https://cdpn.io/dgonzalez55/fullpage/rNaBdbv?anon=true&view=fullpage" %}

Como se puede apreciar en el ejemplo, este elemento se enlaza con un control de entrada de datos asignando a su atributo **`for`** el valor del atributo **`id`** del control de entrada de datos vinculado. Mediante esta unión se consigue que cuando el usuario pulse sobre la etiqueta definida se active el control de entrada vinculado (recibe el foco), o en el caso de los _checkbox_ y _radiobutton_ que estos se marquen. De esta forma se consigue mejorar la accesibilidad a la web y en general la experiencia del usuario con el formulario.

{% hint style="danger" %}
Recuerda que el valor del atributo **`id`** debería ser único en toda la web, así que tenlo presente cuando hagas _copy-paste_
{% endhint %}
