# Etiquetas de Listas

{% hint style="info" %}
Las listas son un elemento sumamente importante en el proceso de diseño web pues nos permiten relacionar contenidos entre sí, estableciendo jerarquías y orden.\
Especialmente interesante es su uso para la creación de menús junto con la etiqueta `<`<mark style="color:green;">**`nav`**</mark>`>`.
{% endhint %}

### Listas no numeradas: `<`<mark style="color:green;">`ul`</mark>`>` y `<`<mark style="color:green;">`li`</mark>`>`

```html
<ul>
  <li>Primer Elemento</li>
  <li>Segundo Elemento</li>
  <li>Tercer Elemento</li>
  ...
  <li>Último Elemento</li>
</ul>
```

<figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption><p>Efecto de las etiquetas</p></figcaption></figure>

Sirven para definir listas de elementos `<`<mark style="color:green;">**`li`**</mark>`>` (list ítems) sin orden establecido. Son equivalentes al uso de listas de viñetas de _MS WORD_. Una vez abierta la lista con la etiqueta `<`<mark style="color:green;">**`ul`**</mark>`>` todo el contenido de esta debería definirse mediante las etiquetas de elemento de lista `<`<mark style="color:green;">**`li`**</mark>`>`.

### Listas numeradas: `<`<mark style="color:green;">`ol`</mark>`>` y `<`<mark style="color:green;">`li`</mark>`>`

```html
<ol>
  <li>Primer Elemento</li>
  <li>Segundo Elemento</li>
  <li>Tercer Elemento</li>
  ...
  <li>Último Elemento</li>
</ol>
```

<figure><img src="../.gitbook/assets/image (33).png" alt=""><figcaption><p>Efecto de las etiquetas</p></figcaption></figure>

El funcionamiento es idéntico al de las listas no ordenadas, pero en este caso el navegador las renderiza por defecto estableciendo una numeración para cada elemento. Para indicar que una lista es ordenada, solamente debe sustituirse la etiqueta `<`<mark style="color:green;">**`ul`**</mark>`>` por la etiqueta `<`<mark style="color:green;">**`ol`**</mark>`>`.

### Listas de definiciones: `<`<mark style="color:green;">`dl`</mark>`>`, `<`<mark style="color:green;">`dt`</mark>`>` y `<`<mark style="color:green;">`dd`</mark>`>`

```html
<dl>
  <dt>Término</dt>
  <dd>Definición</dd>
  ...
  <dt>Término</dt>
  <dd>Definición</dd>
</dl>
```

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption><p>Efecto de las etiquetas</p></figcaption></figure>

El uso de las listas de definiciones es algo más infrecuente y sirven para elaborar glosarios en los que se agrupen términos y sus respectivas definiciones (como un diccionario). Estas listas se abren usando la etiqueta `<`<mark style="color:green;">**`dl`**</mark>`>` y en su interior solamente deberían haber conjuntos de pares `<`<mark style="color:green;">**`dt`**</mark>`>` y `<`<mark style="color:green;">**`dd`**</mark>`>`, en donde `<`<mark style="color:green;">**`dt`**</mark>`>` sirve para indicar el término y `<`<mark style="color:green;">**`dd`**</mark>`>` su correspondiente definción.
