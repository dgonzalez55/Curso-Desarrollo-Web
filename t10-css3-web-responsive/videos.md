# Vídeos

Si en un vídeo la propiedad <mark style="color:blue;">**`width`**</mark> se establece en un porcentaje y la propiedad <mark style="color:blue;">**`height`**</mark> se establece en <mark style="color:orange;">**"auto"**</mark>, el reproductor de vídeo será responsivo y se escalará hacia arriba y hacia abajo:

```css
video {
  width: 100%;
  height: auto;
}
```

No obstante, en la mayoría de casos no nos interesará que el reproductor de vídeo supere su tamaño original, para evitarlo podemos emplear la propiedad <mark style="color:blue;">**`max-width`**</mark>:

```css
video {
  max-width: 100%;
  height: auto;
}
```
