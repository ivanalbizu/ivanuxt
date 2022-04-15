---
title: Placeholder con selector :empty
published: true
description: Uso del pseudo selector CSS :empty para etiquetas sin contenido
tags:
  - css
  - pildoritas
ctime: '2022-01-19 09:10:00'
cover_image: placeholder-css-empty.jpg
alt_image: Placeholder con selector :empty
---

Maquetación de un elemento usando pseudo selector <code>:empty</code>, útil para usar como placeholder hasta que el contenido sea cargado, como por ejemplo vía API o usarlo como relleno mientras se maqueta

Lo más interesante aquí es que los estilos a <code>:empty</code> sólo aplican cuando la etiqueta no tenga ningún contenido texto u otras etiquetas, con un sólo espacio el selector no aplica

He aprovechado las custom properties de CSS para hacer el pintado de gradientes convenientemente definidos y posicionados

<ul class="list-bullets">
  <li>El primero para formar un degradado a todo el bloque</li>
  <li>El segundo para la primera forma rectangular</li>
  <li>El tercero para el círculo</li>
  <li>El cuarto para la última forma junto al círculo</li>
</ul>

Mi idea es que sea reutilizable, actualizando sólo estos valores

<ul class="list-bullets">
  <li><code>--color: rgb(199, 199, 199);</code></li>
  <li><code>--width: 100%;</code></li>
  <li><code>--width-line: 250px;</code></li>
  <li><code>--height-rectangle: 150px;</code></li>
  <li><code>--height-line: 24px;</code></li>
  <li><code>--gutter: 10px;</code></li>
</ul>

```scss
<style>
.card__content:empty {
  --color: rgb(199, 199, 199);
  --width: 100%;
  --width-line: 250px;
  --height-rectangle: 150px;
  --height-line: 24px;
  --gutter: 10px;
  --computed-circle-rad: calc(var(--height-line) * 0.5);
  --computed-height: calc(var(--height-rectangle) + var(--gutter) + var(--height-line) + calc(1.5 * var(--gutter))
  );
  height: var(--computed-height);
  background-image:
    linear-gradient(0.9turn, #fff, transparent),
    linear-gradient(var(--color), var(--color)),
    radial-gradient(var(--height-line) circle at var(--computed-circle-rad) var(--computed-circle-rad), var(--color) 50%, transparent 50%),
    linear-gradient(var(--color), var(--color));
  background-size:
    var(--width) var(--computed-height),
    var(--width) var(--height-rectangle),
    var(--height-line) var(--height-line),
    var(--width-line) var(--height-line);
  background-position:
    var(--width) 0,
    0 0,
    0px calc(var(--height-rectangle) + var(--gutter)),
    calc(var(--height-line) + var(--gutter)) calc(var(--height-rectangle) + var(--gutter));
  background-repeat: no-repeat;
}
</style>
```

<iframe height="511" style="width: 100%;" scrolling="no" title="CSS placeholder with :empty selector" src="https://codepen.io/ivan_albizu/embed/RwLOeZW?default-tab=css%2Cresult" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/ivan_albizu/pen/RwLOeZW">
  CSS placeholder with :empty selector</a> by Iván Albizu (<a href="https://codepen.io/ivan_albizu">@ivan_albizu</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>

En este repositorio puede verse el <a href="https://github.com/ivanalbizu/placeholder-css-empty/" target="_blank" rel="noopener">código del placehoder con CSS para selector <code>:empty</code></a>
