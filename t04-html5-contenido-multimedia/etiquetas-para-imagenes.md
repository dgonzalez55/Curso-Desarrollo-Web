# Etiquetas para Imágenes

### Imágenes: `<`<mark style="color:green;">`img`</mark>`>`

```html
<img src="./hipo.png" alt="Hipopótamo Ocre">
```

<figure><img src="../.gitbook/assets/EtiquetaIMG.png" alt="" width="151"><figcaption><p>Imagen correspondiente al fichero "hipo.png" de ejemplo</p></figcaption></figure>

Sirven para añadir imágenes al contenido de nuestra página web. Estas etiquetas tienen dos atributos que son obligatorios, uno por razones obvias es el que indica la URL del que obtener la imagen que se va a renderizar, es el atributo **src**. Debemos tener en cuenta que las rutas que utilicemos deben seguir las siguientes reglas:

* No se deben incluir espacios en blanco.
* Debe garantizarse que la ruta respeta las mayúsculas y minúsculas de la ruta real, pues, aunque Windows no es _case sensitive_, <mark style="background-color:orange;">la mayoría de los servidores web en los que se alojan las páginas son servidores Linux</mark>. Lo recomendable es utilizar siempre minúsculas para el nombre de carpetas y ficheros, evitando también el uso de caracteres especiales.
* Emplea el separador de carpetas tipo UNIX (/) en vez del separador de carpetas tipo Windows (\\). El separador de Windows solo es válido para sistemas Windows, pero el tipo UNIX es válido para todos.
* Asegúrate que la imagen se encuentra en el path indicado o de lo contrario el usuario va a recibir un enlace roto.
* Utiliza siempre rutas relativas y nunca rutas absolutas. Esto es vital para garantizar el mantenimiento de la web y facilitar la migración de la web y todos sus recursos.

\
El otro atributo que siempre debería acompañar una imagen es el atributo **alt** ya que de esta forma se garantiza la correcta accesibilidad de la web. Este atributo debe contener una breve descripción de la imagen, de forma que esta información pueda ser transmitida a las personas que no puedan visualizar la imagen. La importancia del atributo **alt** estriba en:

* Los lectores web avisarán de la existencia de una imagen y leerán al usuario el contenido del atributo **alt**.
* Si la imagen no carga por latencias de red, path erróneo, … El usuario podrá conocer qué imagen se esperaba mostrar.
* Los buscadores no “ven” las imágenes, por lo que confían en dicho atributo para sus búsquedas.
* Para reducir el consumo de datos algunos usuarios de dispositivos mobile desactivan la carga de imágenes. Sin el atributo **alt** serían incapaces de saber lo que la web mostraría.
* Contribuye a crear una web semántica. Si la imagen es pura decoración, debería dejarse el atributo en blanco **alt=””**.

Es nuestra responsabilidad como diseñadores el construir una web libre de barreras y accesible para todos.

Otro aspecto que deberías considerar cuando incorpores imágenes a tu página web es el formato que vas a utilizar, veamos algunos ejemplos:

* **JPEG**: Buena compresión y formato estándar de fotografía. No obstante, no soporta ni transparencias ni animaciones.
* **PNG**: El estándar que promueve el W3C. Se trata de un formato abierto con soporte para transparencias y canales Alpha.
* **SVG**: Imágenes vectoriales generadas mediante funciones matemáticas que soportan animación y que no pierden calidad tras su escalado. Son el formato más recomendable para mostrar gráficos, tablas, mapas, formas geométricas, … El W3C ha definido el estándar SVG 1.1.

{% hint style="info" %}
¿Te interesa saber qué formatos de imagen están soportados por los distintos navegadores? Wikipedia te lo pone fácil, pues puedes consultar dicha información a través de: [https://en.wikipedia.org/wiki/Comparison\_of\_web\_browsers#Image\_format\_support](https://en.wikipedia.org/wiki/Comparison_of_web_browsers#Image_format_support)
{% endhint %}

Sea cual sea el formato que se utilice, es sumamente importante limitar el tamaño de las imágenes para optimizar la carga de la página web.

{% hint style="danger" %}
Recuerda que para aquellas imágenes que actuén como figuras de ejemplo o ilustrativas, debes utilizar la estructura **figure** + **figcaption** que se expuso en: [Figuras y Rótulos: `<figure>` y `<figcaption>`](../t02-html5-organizacion-de-contenido/elementos-estructurales-adicionales.md#figuras-y-rotulos)
{% endhint %}
