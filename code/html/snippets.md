### Image Tag must have's

```
<img src="some-img.png" loading="lazy" decoding="async" alt="A Description of the image" />
```
### WebP Fallback

<picture>
  <source srcset="img/awesomeWebPImage.webp" type="image/webp">
  <source srcset="img/creakyOldJPEG.jpg" type="image/jpeg"> 
  <img src="img/creakyOldJPEG.jpg" alt="Alt Text!">
</picture>
