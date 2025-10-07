# Listas desplegables

### Listas desplegables: `<`<mark style="color:green;">`select`</mark>`>`

Un componente muy habitual en los formularios, es aquel que permite seleccionar una entre múltiples opciones desplegables de una lista de valores. Este tipo de selectores se conocen habitualmente como _combobox_.

```html
  <select name="profePrefe">
    <option value="porti">Tito Porti</option>
    <option value="gon" selected>Maese LeGon</option>
    <option value="miguelangel">El Doctor</option>
    <option value="roberto">Legionario</option>
  </select>
```

{% embed url="https://cdpn.io/dgonzalez55/fullpage/XWJrEyE?anon=true&view=fullpage" %}

Como se puede apreciar en el ejemplo, este control requiere definir las distintas opciones posibles mediante la etiqueta `<`<mark style="color:green;">**`option`**</mark>`>`. Es importante definir para cada opción el valor del atributo **`value`**, pues de lo contrario no se podría saber qué opción fue elegida por el usuario, por esta misma razón deberemos definir también el valor del atributo **`name`** para el elemento `<`<mark style="color:green;">**`select`**</mark>`>`. Para seleccionar por defecto una determinada opción, deberá añadirse a la misma el atributo **`selected`**.

{% hint style="info" %}
Lo más habitual es que las webs carguen las opciones posibles a partir de los valores recogidos en una BBDD, este trabajo es transparente al usuario y es realizado en el servidor por parte del backend.
{% endhint %}
