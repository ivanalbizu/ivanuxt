---
title: Uso de Intersection Observer en Angular
published: true
description: Ejemplo de uso de Intersection Observer en Angular mediante una Directiva para mostrar elementos en pantalla con la API ScrollIntoView
tags:
  - javascript
ctime: "2022-04-15 17:30:00"
cover_image: intersection-observer-en-angular.png
alt_image: Uso de Intersection Observer en Angular
---

Estoy haciendo cursos de Angular, aún no he llegado a temas de Directivas, pero tenía una idea que quería probar 😃. Se trata de una Directiva que usa la Api ScrollIntoView. He añadido unos botones a modo de paginación para que detecte cajas fuera de un contenedor y las introduzca en pantalla

<iframe src="https://codesandbox.io/embed/inspiring-maxwell-hoybwv?fontsize=14&hidenavigation=1&theme=dark&view=editor"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="inspiring-maxwell-hoybwv"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

No recomiendo usarlo tal cual ya que para tamaños de pantalla reducidos podría darse el caso que no cupiera en pantalla y en ese caso no funciona el scrollIntoView. Al menos necesita un elemento al completo dentro de la caja

<a href="https://github.com/ivanalbizu/angular-directive-scrollintoview" target="_blank" rel="noopener">Código en GitHub</a>

<a href="https://codesandbox.io/s/inspiring-maxwell-hoybwv?file=/src/app/directives/scroll-to.directive.ts" target="_blank" rel="noopener">Ejemplo en Codesandbox</a>
