---
title: Anchor Positioning y animation-timeline
description: Como posicionar elementos anclados a puntos de referencia que están en sitios diferentes del DOM
published: true
tags:
  - css
ctime: '2023-12-30 22:00:00'
cover_image: anchor-positioning-y-animation-timeline.png
alt_image: anchor positioning y animation-timeline
---

## CSS Anchor Positioning

Tendremos un elemento que usaremos como punto de referencia de ancla. Daremos el nombre que nos interese mediante el atributo "anchor-name" (el nombre dado debe empezar por "--").

```css
.anchor {
  anchor-name: --anchor;
}
```

Y ahora otro elemento que será anclado al punto definido anteriormente. Lo más importante de este sistema de anclas es que no necesitamos relación padre/hijo para establecer dicha relación, pueden ser nodos en cualquier punto del DOM.

```css
.conditional-sticky {
  position: fixed;
  z-index: 1;
  top: anchor(--anchor bottom);
  left: anchor(--anchor left);
  right: anchor(--anchor right);
}
```

La estructura HTML de los elementos es la siguiente:

```html
<nav class="wrapper-nav anchor">
  <div class="nav">
    <!-- ... -->
  </div>
</nav>

<main class="main">
  <div class="card observe-visibility" id="go-to">
    <div class="card__content"></div>
    <div class="conditional-sticky">
      <div class="conditional-sticky__inner">
        Don't miss the CSS anchor positioning feature + animation-timeline
        <a href="#go-to" class="link">
          <span>let's go</span> <span class="arrow">&darr;</span>
        </a>
      </div>
    </div>
  </div>
  <div class="card">
    <div class="card__content"></div>
  </div>
</main>
```

Con todo lo anterior, hemos usado <a href="https://www.w3.org/TR/css-anchor-position-1/" target="_blank" rel="noopener">CSS Anchor Positioning</a> que todavía está en modo experimental, pero que puede probarse habilitando las flags experimentales en Chrome:

chrome://flags/#enable-experimental-web-platform-features

Un recurso bastante bueno en el que se ve toda la potencia de esta nueva <a href="https://blog.logrocket.com/use-css-anchor-positioning/" target="_blank" rel="noopener">Feature CSS Anchor Positioning</a> es el siguiente.

## Animation Timeline

Quería darle una vuelta a lo anterior y hacer una cosa que hice con Javascript en otro proyecto.

La idea es tener un elemento Sticky debajo del menú de navegación (que también es Sticky) que sea condicionado su visibilidad a que un elemento cualquiera del DOM esté dentro de Viewport. Hacer esto es sencillo hacerlo con Javascript usando al API IntersectionObserver, pero querí probar a no usarlo.

El elemento que será sticky es el que comentamos antes que posicionamos con "CSS Anchor Positioning" <mark>.conditional-sticky</mark>:

```html
<div class="card observe-visibility" id="go-to">
  <div class="card__content"></div>
  <div class="conditional-sticky">
    <div class="conditional-sticky__inner">
      Don't miss the CSS anchor positioning feature + animation-timeline
      <a href="#go-to" class="link">
        <span>let's go</span> <span class="arrow">&darr;</span>
      </a>
    </div>
  </div>
</div>
```

Mediante Custom Property estableceremos su valor de display (que más adelante modificaremos):

```css
.conditional-sticky {
  display: var(--observe-visibility);
}
```

Dicha Property la definimos con CSS:

```css
@property --observe-visibility {
  initial-value: block;
  inherits: true;
  syntax: '<custom-ident>';
}
```

Su valor irá cambiando mediante @keyframes:

```css
@keyframes observe-visibility {
  1%,
  100% {
    --observe-visibility: none;
  }
}
```

Esta @keyframes esta asociada al elemento de pantalla que queramos vigilar:

```css
.observe-visibility {
  animation: observe-visibility linear;
  animation-timeline: view();
  animation-range: cover 0%;
}
```

Los funciones de animación deben ser "linear", ya que no está asociadas a tiempos como tradicionalmente han sido. En este caso, está basado en el scroll que se hace en la página. animation-timeline nos ofrece dos funciones: <code>scroll()</code> y <code>view()</code>, en este caso me interesa la segunda. Sobre el rango, tenemos múltitud de opciones: entradas/salidas de pantalla, porcentajes/píxeles/...

Recomiendo este <a href="https://developer.chrome.com/docs/css-ui/scroll-driven-animations" target="_blank" rel="noopener">árticulo para más info de Bramus</a> con multitud de ejemplos, son una pasada.

## Extra: detectar si un elemento está por encima o por debajo del Viewport

Dentro del elemento sticky tengo un vínculo con una flecha que cambia de dirección: hacía abajo si el elemento de referencia se encuentra por la cara inferior del scroll y hacía arriba si está por la cara superior. Te dejo el snipet de código apra que lo pienses un poco :)

```html
<a href="#go-to" class="link">
  <span>let's go</span> <span class="arrow">&darr;</span>
</a>
```

```css
@property --detect-direction {
  initial-value: 0deg;
  inherits: true;
  syntax: '<angle>';
}
.arrow {
  rotate: var(--detect-direction);
}
.observe-visibility {
  animation: detect-direction linear forwards;
  animation-timeline: view();
  animation-range: exit;
}
@keyframes detect-direction {
  to {
    --detect-direction: 180deg;
  }
}
```

Nota: no me preocupé por la dirección correcta del arrow cuando esté el elemento observado en pantalla, ya que su padre estará oculto :)

Recomiendo bucear en las cosas que hacen y publican Bramus y de Jhey, cosas chulísimas!

<a href="https://www.bram.us/">Bram.us</a> y <a href="https://jhey.dev/links/">jhey.dev</a>
