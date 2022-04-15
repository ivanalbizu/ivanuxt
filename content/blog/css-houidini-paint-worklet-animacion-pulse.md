---
title: CSS Houdini - paintWorklet para animacion de cursor estilo pulse
published: true
description: Animación de Cursor estilo Pulse usando CSS Houdini paintWorklet
tags:
  - javascript
  - css
ctime: "2021-01-09 15:10:00"
cover_image: css-houidini-paint-worklet-animacion-pulse.png
alt_image: CSS Houdini paintWorklet animacion cursor estilo pulse
---

Se trata de mi primer contacto con CSS Houdini. Venía tiempo viendo que se hablaba mucho sobre Houdini y por fin he decidido probar un poco en que consiste

Me ha venido muy bien:

<ul class="list-bullets">
  <li>Los aportes de Joan León en Youtube y sus recursos en GitHub. Su web: <a href="https://joanleon.dev/" target="_blank" rel="noopener">https://joanleon.dev/</a></li>
  <li>El canal de Youtube de <a href="https://www.youtube.com/c/LeonidasEsteban/search?query=houdini" target="_blank" rel="noopener">Leonidas Esteban</a></li>
</ul>

Aquí dejo el Pen con mi primera prueba con CSS Houdini usando Paint Worklet, con el que se le da color de fondo y se simula el cursor del ratón creando un círculo <code>canvas</code> y otro exterior animado estilo "Pulse". Las coordenadas del círculo son definidas mediante CSS <code>Custom Properties</code>

<iframe height="660" style="width: 100%;" scrolling="no" title="CSS Houdini paintWorklet - Button Pulse" src="https://codepen.io/ivan_albizu/embed/qBayPeR?height=543&theme-id=2608&default-tab=result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/ivan_albizu/pen/qBayPeR'>CSS Houdini paintWorklet - Button Pulse</a> by Iván Albizu
  (<a href='https://codepen.io/ivan_albizu'>@ivan_albizu</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

Para esta ocasión, no voy a comentar de momento el código, estoy en modo aprendizaje, y podría no hablar con mucha propiedad. Puede verse todo el código completo en mi Git o en el mismo Pen

<a href="https://github.com/ivanalbizu/css-houdini-button-pulse-animation" target="_blank" rel="noopener">Código en mi GitHub</a>