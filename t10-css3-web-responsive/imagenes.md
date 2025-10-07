# Imágenes

Si la propiedad <mark style="color:blue;">**`width`**</mark> de una imagen se establece en un porcentaje y la propiedad <mark style="color:blue;">**`height`**</mark> se establece en <mark style="color:orange;">**"auto"**</mark>, la imagen será responsiva y se escalará hacia arriba y hacia abajo:

```css
img {
  width: 100%;
  height: auto;
}
```

No obstante, en la mayoría de casos no nos interesará que la imagen supere su tamaño original, para evitarlo podemos emplear la propiedad <mark style="color:blue;">**`max-width`**</mark>:

```css
img {
  max-width: 100%;
  height: auto;
}
```

Otro aspecto que nos puede interesar, es utilizar una imagen distinta en función del tamaño de pantalla, para ello podemos utilizar los ya comentados **Media Queries**:

```css
/* Para smartphones (Mobile First) */
body {
  background-image: url('img_smallflower.jpg');
}

/* Para anchos de pantalla de como mínimo 768 pixeles (a partir de tablets en formato horizontal) */
@media only screen and (min-width: 768px) {
  body {
    background-image: url('img_flowers.jpg');
  }
}
```

