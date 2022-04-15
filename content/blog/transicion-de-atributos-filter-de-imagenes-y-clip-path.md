---
title: Transición de imágenes modificando atributos filter
published: true
description: Transición entre imágenes modificando atributos CSS filter y animación de clip-path
tags:
  - javascript
  - html
  - css
ctime: "2021-06-19 15:10:00"
cover_image: transicion-de-imagenes-modificando-atributos-filter.jpg
alt_image: Transición de imágenes modificando atributos filter
---

Empiezo por decir que la animación de filters CSS no he dado soporte a pantallas pequeñas. La animación se lanza con eventos de mousewheel y flechas arriba y abajo.

La animación se ha aplicado a:

<ul class="list-bullets">
  <li>Sobre las imágenes aplicando <code>keyframes</code>: <code>transform: scale()</code> y <code>filter: blur() drop-shadow()</code></li>
  <li>Usando <code>transition</code> sobre elemento decorativo bajo las imágenes <code>clip-path()</code></li>
</ul>

Las diferentes imágenes son colcadas una sobre otra y cambiando su z-index en función del elemento activo

En este <a href="https://codepen.io/ivan_albizu/pen/PopLvro" target="_blank" rel="noopener">PEN</a> se puede ver ejemplo. Como he comentado, sólo lo hice para desktop

<iframe height="720" style="width: 100%;" scrolling="no" title="Image filter transition" src="https://codepen.io/ivan_albizu/embed/PopLvro?height=837&theme-id=2608&default-tab=result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/ivan_albizu/pen/PopLvro'>Image filter transition</a> by Iván Albizu
  (<a href='https://codepen.io/ivan_albizu'>@ivan_albizu</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

## Animación keyframes sobre las imágenes

El <code>keyframes image-current</code> se aplica en la primera parte de la animación a la imagen que actualmente se esté viendo, la animación consiste en hacer desaparecer la imagen cambiando su <code>scale</code> desde el estado normal hasta 0 y aplicando <code>blur</code> de 20px. La imagen tiene asociada un <code>drop-shadow()</code> que se convierte en transparente al finalizar la primera parte de la animación

La segunda parte de la animación esta basada en el <code>keyframes image-next</code>, se aplica a la imagen que entra. Inicialmente parte del mismo estado final de la imagen anterior para terminar con el estado por defecto, es decir, sin difuminar <code>blur(0px)</code>, sin cambiar su tamaño <code>scale(1)</code> y con sombra <code>drop-shadow(0px 20px 30px rgba(0,0,0,.9))</code>

Las animaciones son disparadas cuando hemos añadido con <code>javascript</code> la clase "animating"

```css
@keyframes image-current {
  from {
    filter: blur(0) drop-shadow(0px 20px 30px rgba(0,0,0,.9));
    transform: scale(1);
  }
  to {
    filter: blur(60px) drop-shadow(0px 20px 30px rgba(0,0,0,0));
    transform: scale(0);
  }
}
@keyframes image-next {
  from {
    filter: blur(60px) drop-shadow(0px 20px 30px rgba(0,0,0,0));
    transform: scale(0);
  }
  to {
    filter: blur(0) drop-shadow(0px 20px 30px rgba(0,0,0,.9));
    transform: scale(1);
  }
}

.animating {
  .content--active {
    img {
      animation: image-current .35s linear 0s forwards;
    }
  }
  .content--next {
    img {
      animation: image-next .35s linear .35s;
    }
  }
}
```

## Animación con transition de clip-path

En la cara inferior de las imágenes se colocan dos "capas" con <code>pseudo elementos before y after</code>. Estos elementos contienen los colores y se irá cambiando su visibilidad mediante modificación de <code>clip-path</code> de elemento que sale y elemento que entra, básicamente es la misma idea que con las imágenes, pero sin <code>keyframes</code> y con <code>transition</code>

```css
.grid {
  color: #fff;
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: min-content 1fr;
  gap: 0px;
  grid-template-areas:
    "nav nav"
    "left right";
  height: 100vh;
  background: linear-gradient(to right, $color-3 50%, $color-1 50%);
  overflow: hidden;
  &__nav {
    grid-area: nav;
    padding: 10px 15px;
  }
  &__left {
    grid-area: left;
    display: grid;
    grid-template-columns: 60px repeat(2, 1fr) 60px;
    grid-template-rows: 1fr 13vw;
    gap: 0;
    height: 100%;
    .content {
      grid-area: 1 / 1 / 3 / 5;
      z-index: -1;
      display: grid;
      grid-template-columns: 60px repeat(2, 1fr) 60px;
      grid-template-rows: 1fr 13vw;
      padding-top: 30px;
      img {
        z-index: 5;
        grid-area: 1 / 1 / 3 / 5;
        justify-self: center;
        max-height: calc(100vh - 120px);
        transform: scale(0);
      }
      &::before,
      &::after {
        content: '';
        display: block;
      }
      &::before {
        grid-area: 2 / 1 / 3 / 3;
        clip-path: polygon(0 0, 100% 0, 100% 0, 0 0); //no se ve
        transition: clip-path .5s ease-in-out .2s;
      }
      &::after {
        grid-area: 2 / 3 / 3 / 5;
        clip-path: polygon(100% 0%, 100% 0%, 100% 100%, 100% 100%); //no se ve
        transition: clip-path .7s ease-in-out;
      }
      transition: clip-path .7s ease-in-out;
      &--active {
        z-index: 2;
        img {
          transform: scale(1);
          filter: blur(0) drop-shadow(0px 20px 30px rgba(0,0,0,.9));
        }
        &::before {
          clip-path: polygon(0 0, 100% 0, 100% 100%, 0% 100%); //se ve completo
        }
        &::after {
          clip-path: polygon(0 0, 100% 0%, 100% 100%, 0% 100%); //se ve completo
        }
      }
      &--next {
        z-index: 3;
        &::before {
          clip-path: polygon(0 0, 100% 0, 100% 100%, 0% 100%); //se ve completo
        }
        &::after {
          clip-path: polygon(0 0, 100% 0%, 100% 100%, 0% 100%); //se ve completo
          transition: clip-path .7s ease-in-out;
        }
      }
      &--1 {
        &::before {
          background-color: #843577;
        }
        &::after {
          background-color: #53607A;
        }
      }
      &--2 {
        &::before {
          background-color: #357C97;
        }
        &::after {
          background-color: #F9DA4D;
        }
      }
      &--3 {
        &::before {
          background-color: #4D9B58;
        }
        &::after {
          background-color: #F27F30;
        }
      }
    }
    .pagination {
      grid-area: 1 / 1 / 3 / 2;
      place-self: center;
    }
  }
  &__right {
    grid-area: right;
    padding: 60px 50px 20px;
  }
}
```


Hay mucho más código, puede verse completo en mi <a href="https://github.com/ivanalbizu/image-filter-transition" target="_blank" rel="noopener">GitHub</a>
