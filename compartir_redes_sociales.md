Compartir en Redes Sociales con Enlaces
======

Usar anchor tags de html para compartir enlaces en las redes sociales más utilizadas.

Basic URL Text Encoder: [http://meyerweb.com/eric/tools/dencoder/](http://meyerweb.com/eric/tools/dencoder/)


## Facebook

```
<a href="https://www.facebook.com/sharer/sharer.php?u=http://ProbarDjango.com/">
Compartir en Facebook
</a>
```
Por supuesto puedes sustituir `http://probardjango.com/` con tu propio enlace.


## Twitter

```
<a href="https://twitter.com/home?status=Voy%20a%20aprender%20a%20escribir%20código...%20Anímate%20tú%20también%20a%20crear%20aplicaciones%20web%20conmigo!%20http://probardjango.com/">
Compartir en Twitter
</a>
```
Ojo!, Twitter es un poco más complicado. Tiene que ser texto con codificación URL. Algo así:

```
Voy%20a%20aprender%20a%20escribir%20código...%20Anímate%20a%20crear%20aplicaciones%20web%20conmigo!%20%http://probardjango.com/

```
En realidad se lee así:
```
Voy a aprender a escribir código... Anímate a crear aplicaciones web conmigo!  http://probardjango.com/
```
Fíjate que los espacios son `%20` en vez de un espacio real. Usando este formato asegura que puede ser compartido correctamente. 

Entonces:

``` 
Url base: <a href="https://twitter.com/home?status=">Compartir en Twitter</a>

Configurar "?status=" a tu cadena html como: 

Voy%20a%20aprender%20a%20escribir%20código...%20Anímate%20a%20crear%20aplicaciones%20web%20conmigo!%20%http://probardjango.com/

Tu etiqueta <a> será:

<a href="https://twitter.com/home?status=Voy%20a%20aprender%20a%20escribir%20código...%20Anímate%20tú%20también%20a%20crear%20aplicaciones%20web%20conmigo!%20http://probardjango.com/">
Compartir en Twitter
</a>

```

## Google Plus

Google Plus no tiene complicaciones. Utiliza lo siguiente:
```
<a href='https://plus.google.com/share?url=http://probardjango.com'>Compartir en Google+</a>
```
Cambiar `http://probardjango.com` con tu propia url



## LinkedIn

Muy parecido al proceso para Twitter:
```
<a href="https://www.linkedin.com/shareArticle?mini=true&url=http://probardjango.com/&title=Aprender%20Django:%20cursos%20para%20todos%20los%20niveles&
summary=Probar%20Django%20es%20una%20a%20comunidad%20donde%20puedes%20aprender%20el%20framework%20de%20Django%20a%20base%20de%20proyectos%20enteros.%20Únete%20y%20aprender%20a%20programar%20desde%20cero.&
source=http://probardjango.com/">
Compartir en Linkedin
</a>
```
Url base:  https://www.linkedin.com/shareArticle

Atributos opcionales: mini, url, title, summary, source


Añadir tus atributos a la url base
```
mini = True #o false

url = http://probardjango.com/ 
#Url de tu página web

title = Únete%20a%20%nuestra%20comunidad%20de%20Django:%20cursos%20para%20todos%20los%20niveles
#Especificas el título para el artículo que comparten 

summary = Probar%20Django%20es%20una%20comunidad%20donde%20puedes%20aprender%20el%20framework%20a%20base%20de%20proyectos%20enteros.%20Únete%20y%20aprende%20a%20programar%20desde%20cero.
# mensaje real

source = http://probardjango.com/
# Origen de tu artículo

```

Ahora que tienes atributos diferentes, los añades a to URL base así:
```
https://www.linkedin.com/shareArticle?mini=...&url=...&title=...&summary=...&source=...

```
Sustituir el "..." con los valores que elijas.


## Reddit

También parecido al proceso para Twitter y LinkedIn

```
<a href="http://www.reddit.com/submit?url=http://probardjango.com/&
title=Abrir%20tpara%20Aprender%20Django%20con%20nosotros!%20Cursos%20para%20todos%20los%20niveles.%20Incluso%20para%20principiantes%20sin%20experiencia.">Compartir en Reddit</a>
```

URL base y atributos
```
base_url = http://www.reddit.com/submit
atributos = url, title
```
En este ejemplo la url y título son:
```
url = http://probardjango.com/
title=Abrir%20tpara%20Aprender%20Django%20con%20nosotros!%20Cursos%20para%20todos%20los%20niveles.%20Incluso%20para%20principiantes%20sin%20experiencia.
```

Júntalos así:

```
http://www.reddit.com/submit?url=...&title=...
```
Sustituir "..." con el valor del atributo.



## Pinterest
Primero, añadir `Javascript` a tu archivo `base.html` si estás utilizando Django. 

```
<script async defer src="https://assets.pinterest.com/js/pinit.js"></script>
```

Después, añadir los tags anchor/img. Dónde el tag <img> tienes que meter la fuente de tu propia imágen. 
```
<a data-pin-do="buttonBookmark" href="//www.pinterest.com/pin/create/button/"><img src="//assets.pinterest.com/images/pidgets/pinit_fg_en_rect_gray_20.png" /></a>
```
En `Django` se parecerá a lo siguiente:

```
<a data-pin-do="buttonBookmark" href="//www.pinterest.com/pin/create/button/"><img src="{{ object.image.url }}" /></a>

```



