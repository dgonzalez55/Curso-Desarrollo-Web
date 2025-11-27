# Etiquetas para Audios

### Audios: `<`<mark style="color:green;">`audio`</mark>`>`

```html
   <!-- Ejemplo de uso si únicamente disponemos del recurso de audio en un formato compatible -->
   <audio src="https://archive.org/download/MLKDream/MLKDream_64kb.mp3" controls loop muted preload="none">Discurso de Martin Luther King</audio>

   <!-- Ejemplo de uso si disponemos del mismo recurso de audio en varios formatos compatibles -->
   <audio controls loop muted preload="none">
     Discurso de Martin Luther King
     <source src="https://archive.org/download/MLKDream/MLKDream.wav" type="audio/wav">
     <source src="https://archive.org/download/MLKDream/MLKDream_64kb.mp3" type="audio/mpeg">
   </audio>
```

{% embed url="https://cdpn.io/dgonzalez55/fullpage/OKBvrg?anon=true&view=fullpage" %}

Mediante este elemento podremos incrustar un fichero de audio en nuestra página web para que pueda ser reproducido a través del propio navegador.\
Cualquier texto situado entre las etiquetas `<`<mark style="color:green;">**`audio`**</mark>`>...</`<mark style="color:green;">**`audio`**</mark>`>` se mostrará por parte del navegador en caso de que no se pueda reproducir el elemento multimedia. Resulta por tanto recomendable añadirlo en aras a mejorar la experiencia de usuario sea cual sea su mecanismo de acceso a la web.\
\
El elemento `<`<mark style="color:green;">**`audio`**</mark>`>` dispone de varios atributos que permiten configurar la reproducción del mismo:

| Atributo     | Descripción                                                                                                                                                                                                                                                                                                                                                                  | Ejemplo                                                                                                                |
| ------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| **src**      | <p>URL del fichero de audio:<br></p><p><em><strong>Ruta Absoluta</strong></em>: Origen externo a la propia web<br></p><p><em><strong>Ruta Relativa</strong></em>: Origen interno</p>                                                                                                                                                                                         | `<audio src="https://archive.org/download/MLKDream/MLKDream.wav"></audio>`                                             |
| **controls** | <p>Si se añade provee de un interfaz de control de reproducción del audio: play, pause, mute,...<br><img src="../.gitbook/assets/Audio-controls.png" alt=""></p>                                                                                                                                                                                                             | `<audio src="https://archive.org/download/MLKDream/MLKDream.wav" controls></audio>`                                    |
| **loop**     | Si se añade, la reproducción se realizará en bucle sin final                                                                                                                                                                                                                                                                                                                 | `<audio src="https://archive.org/download/MLKDream/MLKDream.wav" controls loop></audio>`                               |
| **muted**    | Si se añade, la reproducción se iniciará en silencio                                                                                                                                                                                                                                                                                                                         | `<audio src="https://archive.org/download/MLKDream/MLKDream.wav" controls loop muted></audio>`                         |
| **preload**  | <p>Indica al navegador si debe descargar el recurso de audio durante la carga de la página web:<br></p><p><em><strong>none</strong></em>: no descargar nada</p><p><br><em><strong>metadata</strong></em>: descargar los metadatos del recurso</p><p><br><em><strong>auto</strong></em>: se puede descargar el fichero de audio durante el proceso de carga de la página.</p> | `<audio src="https://archive.org/download/MLKDream/MLKDream.wav" controls loop muted preload="none"></audio>`          |
| **autoplay** | Si se añade, la reproducción se inicia automáticamente.                                                                                                                                                                                                                                                                                                                      | `<audio src="https://archive.org/download/MLKDream/MLKDream.wav" controls loop muted preload="none" autoplay></audio>` |

Como se deduce del ejemplo expuesto al principio del apartado, existe también la posibilidad de incorporar nuestro recurso de audio proporcionando múltiples fuentes en diferentes formatos. La ventaja de dicha implementación es la de que si por cualquier motivo el navegador no puede reproducir el primer formato, lo intentará con el segundo y así sucesivamente. Adicionalmente el navegador podrá seleccionar entre la lista de fuentes de audio aquel recurso cuyo codec soporte (por ejemplo, algunos navegadores no soportan los ficheros _wav_ por lo que directamente se optaría por reproducir el _mp3_).\
Para añadir múltiples fuentes de audio deberemos utilizar la etiqueta `<`<mark style="color:green;">**`source`**</mark>`>` contenida dentro del elemento `<`<mark style="color:green;">**`audio`**</mark>`>...</`<mark style="color:green;">**`audio`**</mark>`>`. Dicha etiqueta sirve al mismo propósito que el atributo **src** ya referido.\
El elemento `<`<mark style="color:green;">**`source`**</mark>`>` dispone de un par de atributos para indicar la fuente del recurso:<br>

| Atributo | Descripción                                                                                                                                                                                                                                                                  | Ejemplo                                                                              |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| **src**  | URL del fichero de audio                                                                                                                                                                                                                                                     | `<source src="https://archive.org/download/MLKDream/MLKDream.wav">`                  |
| **type** | <p>Especifica el tipo de recurso multimedia (MIME). Los principales tipos MIME son:</p><p><br><em><strong>audio/mpeg</strong></em>: Ficheros MP3</p><p><br><em><strong>audio/ogg</strong></em>: Ficheros OGG</p><p><br><em><strong>audio/wav</strong></em>: Ficheros WAV</p> | `<source src="https://archive.org/download/MLKDream/MLKDream.wav" type="audio/wav">` |

{% hint style="info" %}
Puedes consultar todos los tipos MIME de audio disponibles en: [http://www.iana.org/assignments/media-types/media-types.xhtml#audio](http://www.iana.org/assignments/media-types/media-types.xhtml#audio)\
También puedes consultar los formatos compatibles para los diferentes navegadores en: [https://developer.mozilla.org/en-US/docs/Web/HTML/Supported\_media\_formats#Browser\_compatibility](https://developer.mozilla.org/en-US/docs/Web/HTML/Supported_media_formats#Browser_compatibility)
{% endhint %}
