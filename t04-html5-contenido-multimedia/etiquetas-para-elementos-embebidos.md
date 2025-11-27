# Etiquetas para elementos Embebidos

### Contenido Embebido: `<`<mark style="color:green;">`iframe`</mark>`>`

```html
   <!-- Visor de PDFs embebido -->
   <iframe src="http://docs.google.com/gview?url=http://file.allitebooks.com/20190407/HTML5%20in%20Action.pdf&embedded=true" style="width:300px; height:400px;" frameborder="0"></iframe>

   <!-- Vídeos de Youtube -->
   <iframe width="560" height="400" src="https://www.youtube.com/embed/6JsdQa48rko" frameborder="0" allowfullscreen></iframe>

   <!-- Audios de Soundcloud -->
   <iframe width="300" height="400" scrolling="no" frameborder="no" allow="autoplay" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/480583797&color=%23ff5500&auto_play=false&hide_related=false&show_comments=true&show_user=true&show_reposts=false&show_teaser=true&visual=true"></iframe>

   <!-- Mapas de Google Maps -->
   <iframe src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d12287.113943754763!2d66.96709040604117!3d39.65469953457392!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x0%3A0x992830472abcf47d!2sTillya-Kori+Madrasah!5e0!3m2!1ses!2ses!4v1565692361960!5m2!1ses!2ses" width="400" height="400" frameborder="0" style="border:0" allowfullscreen></iframe>
```

{% embed url="https://cdpn.io/dgonzalez55/fullpage/wvwMgmZ?anon=true&view=fullpage" %}

Los **Iframes** se utilizan para presentar contenido o recursos externos a la propia web. El tipo de su contenido no se limita a ofrecer simples ventanas a otras web, sino que va desde poder incrustar vídeos de Youtube, a embeber visores para ficheros PDF o mapas de Google Maps. No obstante los **iframes** presentan un problema de seguridad y es que un usuario malintencionado los podría utilizar para suplantar la identidad de un sitio web legítimo embebiendo la página al completo, razón por la que muchos portales bloquean su uso. Este es el caso de Google que no permite **iframe** alguno para embeber su página web.<br>

Existen múltiples e importantes atributos que atañen a los iframes, pero nos centraremos en los más importantes:

| Atributo               | Descripción                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | Ejemplo                                                                                                                                                                 |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **src**                | URL de la página/componente web que deseamos embeber en el _iframe_                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | `<iframe src="https://www.youtube.com/embed/6JsdQa48rko"></iframe>`                                                                                                     |
| **allowfullscreen**    | Si aparece indica que se permite mostrar el contenido del iframe a pantalla completa, lo que resulta muy práctico para la reproducción de vídeos por ejemplo.                                                                                                                                                                                                                                                                                                                                                                                                                                                        | `<iframe src="https://www.youtube.com/embed/6JsdQa48rko" allowfullscreen></iframe>`                                                                                     |
| **height** y **width** | Especifican la altura y ancho del _iframe' en píxels_                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | `<iframe src="https://www.youtube.com/embed/6JsdQa48rko" allowfullscreen width="560" height="400"></iframe>`                                                            |
| **name**               | Especifica el nombre del iframe, lo que le permite ser un válido para el atributo **target** de los `<`<mark style="color:green;">**`a`**</mark>`>` y poder así alterar el contenido del **iframe** de forma interactiva                                                                                                                                                                                                                                                                                                                                                                                             | `<iframe name="marco-dinamico" src="https://www.w3.org/"></iframe><a href="https://www.wikipedia.org/" target="marco-dinamico">Mostrar Wikipedia dentro del iframe</a>` |
| **sandbox**            | <p>Admite múltiples valores y permite aplicar restricciones sobre el <em>iframe</em> como prevenir la aparición de pop-ups, ejecución de scripts, etc. Su principales valores posibles son:</p><p><br><em><strong>Sin Valor</strong></em> : Se aplican todas las restricciones posibles.</p><p><br><em><strong>allow-forms</strong></em>: Se permiten formularios.</p><p><br><em><strong>allow-modals</strong></em>: Se permiten ventanas modales.</p><p><br><em><strong>allow-popups</strong></em>: Se permiten pop-ups.</p><p><br><em><strong>allow-scripts</strong></em>: Se permite la ejecución de scripts.</p> | `<iframe src="https://www.w3.org/" sandbox></iframe>`                                                                                                                   |

\
Los aspectos claves en relación a los iframes se pueden resumir en:

* Aunque los _iframes_ se cargan de forma independiente al contenido de la página principal éstos pueden ralentizar la carga de la misma. Para evitarlo, se debería aplicar **Javascript**.
* Utilizar el atributo **sandbox** añade seguridad y evita que el contenido externo pueda afectar al contenido interno.
* Especialmente útiles para contenido de terceros como publicidad.
* Resultan prácticos para combinar contenido estático con contenido dinámico.
* Se deben considerar como piezas auxiliares de nuestra web y no como elementos principales.
* Presentan problemas de accesibilidad aunque se pueden añadir notas para los lectores de pantalla.
* No se tiene control sobre el contenido que presenta el _iframe_ lo que puede repercutir en una brecha de seguridad posteriormente.
* Penalizan el SEO de la web.

<br>
