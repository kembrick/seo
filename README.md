Оптимизации для успешного прохождения сайтом теста Lighthouse 

1. Настройка кэширования статики в конфиге nginx
```
location ~* ^.+\.(jpg|jpeg|gif|png|svg|js|css|mp3|ogg|mpe?g|avi|zip|gz|bz2?|rar|swf|woff2)$ {
    expires 120d;
    try_files $uri $uri/ @fallback;
}
```
Под голым Apache можно бы было так:
```
AddType image/webp .webp
AddType video/webm .webm
AddType video/mp4 .mp4
AddType image/svg+xml .svg
AddType text/woff .woff
AddType text/woff2 .woff2
<IfModule mod_expires.c>
  ExpiresActive on
  ExpiresByType image/jpeg "access plus 1 year"
  ExpiresByType image/gif "access plus 1 year"
  ExpiresByType image/png "access plus 1 year"
  ExpiresByType image/svg+xml "access 1 year"
  ExpiresByType image/webp "access plus 1 year"
  ExpiresByType video/webm "access plus 1 year"
  ExpiresByType video/mp4 "access plus 1 year"
  ExpiresByType text/woff "access plus 1 year"
  ExpiresByType text/woff2 "access plus 1 year"
  ExpiresByType text/css "access plus 1 year"
  ExpiresByType application/javascript "access plus 1 year"
</IfModule>
```
2. В CSS всем загружаемым шрифтам указать
```   
font-display: swap;
```
4. Предотвращение CLS в адаптивном слайдере Owl carousel

В SCSS:
```
// CLS-fix
.owl-carousel {
  display: block;
  & > *:not(.owl-nav, .owl-dots) {
    display: none;
    &:first-child {
      display: block;
    }
  }
  @-moz-document url-prefix() {
    @media only screen and (min-width: $screen-lg-min) {
      img {
        width: auto;
      }
    }
  }
}
```
В HTML:
```
<div class="first-slider owl-carousel owl-theme">
  <div>
    <picture>
       <source class="owl-lazy" data-srcset="..." media="(min-width: 768px)" width="1125" height="553">
       <img class="owl-lazy" data-src="..." width="400" height="500">
    </picture>
  </div>
</div>
```
