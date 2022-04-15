---
title: Nested CSS @container
published: true
description: Ejemplo visual de comportamiento de posibilidad de definir CSS @container dentro de otras
tags:
  - html
  - css
ctime: "2021-10-02 15:10:00"
cover_image: nested-css-container.png
alt_image: Nested CSS Container
---

Estoy haciendo pruebas con una nueva feature de CSS, se llama <code>@container</code>. Todavía no está implementada en los navegadores actuales, pero es posible probar en Chrome Canary o en Brave.

En este PEN puedes ver ejemplo, cambiando el tamaño de la ventana. Pulsa en "Edit on CODEPEN" en la esquina superior derecha para abrir en nueva pestaña. Eso si, necesitas habilitar en Brave o Chrome Canary el Flag "container querie" (más detalle en el siguiente punto)

<iframe height="511" style="width: 100%;" scrolling="no" title="Nested CSS @container" src="https://codepen.io/ivan_albizu/embed/YzQWxKN?default-tab=html%2Cresult" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/ivan_albizu/pen/YzQWxKN">
  Nested CSS @container</a> by Iván Albizu (<a href="https://codepen.io/ivan_albizu">@ivan_albizu</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>

## Habilitar @container en el navegador

Para habilitarlo hay que ir a "chrome://flags/" y buscar por "container queries" y "Habilitar". Para Brave el procedimiento es el mismo pero entrando por "brave://flags/"
Y si te vas a poner a trastear recomiendo Chrome Canary ya que además de poder ver las diferentes Queries que tengas definidas, Canary añade en el marcado HTML los diferentes <code>@container</code> que tengas asociado a el/los elementos HTML.

Como he comentado, no está aún implementada, y su estado es UNOFF https://caniuse.com/css-container-queries por lo que mucho de que estoy probando podría cambiar o no llegar a implementarse, aunque espero que no, porque su potencia es enorme

## ¿Qué es CSS @container?

<code>@container</code> es similar a @media queries, pero en lugar de aplicar estilos en función del ancho del "viewport" los estilos se aplican en función del ancho del elemento HTML que sea definido como <code>@container</code>.

Estoy realizando un componente TABS, en el que cada uno de sus elementos sea "independiente" y pueda tener estilos propios en función de su tamaño concreto. No me quiero enredar con esto, ya que lo publicaré en una próxima entrada.

## Anidación de @container dentro de otras

Quería probar si era posible que elementos hijos de un <code>@container</code> pudieran tener otras <code>@container</code>. Es posible!!

Básicamente, necesitamos tener un envolvente que se defina como <code>@container</code> y dentro los elementos que necesitamos.

El ejemplo CSS:

```css
.layout {
  contain: layout inline-size style; // elemento @container principal
  &-wrapper {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: auto auto;
    align-items: center;
    text-align: center;
  }
  &__top {
    grid-column: 1 / -1;
  }
  &__left {
    contain: layout inline-size style; // elemento @container nested
  }
  &__right {
    contain: layout inline-size style; // elemento @container nested
  }
}
```

Y el ejemplo HTML, escrito en PUG:

```pug
main.layout // es envolvente, sólo defino @container
  .layout-wrapper
    .layout__top(data-width='') // es envolvente, sólo defino @container
      .data Superior >700
        span
    .layout__left(data-width='') // es envolvente, sólo defino @container
      .data Izquierda <250
        span
    .layout__right(data-width='') // es envolvente, sólo defino @container
      .data Derecha >500
        span
```

Puede verse todo el código completo en mi Git

<a href="https://github.com/ivanalbizu/nested-css-container/" target="_blank" rel="noopener">Código en mi GitHub</a>