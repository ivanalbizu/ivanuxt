---
title: Mejora responsive mediante función clamp() de CSS
published: true
description: Mejora de la experencia de usuario mediante el uso de la función clamp() de CSS para unidades, estableciando valores mínimos, máximos y deseados
tags:
  - css
ctime: "2021-04-04 15:10:00"
cover_image: hello-clamp.jpg
alt_image: Mejora responsive mediante función clamp() de CSS
---

La función CSS clamp(parametro1, parametro2, parametro3) permite establecer tres valores unitarios para propiedades CSS: <a href="https://www.w3schools.com/cssref/css_units.asp" target="_blank" rel="noopener">https://www.w3schools.com/cssref/css_units.asp</a>.

Los tres parámetros serán:

<ul class="list-bullets">
  <li>Parámetro 1: valor mínimo</li>
  <li>Parámetro 2: valor deseado</li>
  <li>Parámetro 3: valor máximo</li>
</ul>

Clamp puede ser generado también mediante la combinación de las las funciones <code>min()</code> y <code>max()</code>:

<code>max(MIN, min(VAL, MAX))</code> <code>font-size: clamp(14px, 4vw, 30px);</code>

Para los parámetros se puede usar otras funciones como <code>calc()</code>

Más detalles en <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/clamp()" target="_blank" rel="noopener">https://developer.mozilla.org</a>

En este PEN puede ver ejemplo. He usado la función <code>clamp()</code> y un <code>mixin SCSS</code> basado en <code>mediaqueries</code>. Recomiendo abrirlo directamente en codepen, cambiar tamaños de pantalla y editar los valores para ver como se ajustan a la pantalla

<iframe height="400" style="width: 100%;" scrolling="no" title="fluid css" src="https://codepen.io/ivan_albizu/embed/abpBOym?height=300&theme-id=2608&default-tab=css,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/ivan_albizu/pen/abpBOym'>fluid css</a> by Iván Albizu
  (<a href='https://codepen.io/ivan_albizu'>@ivan_albizu</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

## ¿Por que puede ser interesante el uso de clamp()?

<ol class="list-bullets">
  <li>Hacer una web más fluida, desde tamaño Mobile hasta Desktop, actuando en:
    <ol class="list-bullets">
      <li>Tamaño de fuentes y separación, principalmente para títulos de páginas y secciones</li>
      <li>Separaciones interiores en cajas (padding)</li>
      <li>Separación de elementos respecto a otros (margin)</li>
    </ol>
  </li>
  <li>Se podrían ahorrar más diseños. La transición desde Mobile hasta Desktop será fluida, estableciendo una guía de estilos</li>
  <li>Se puede ahorrar algo de tiempo en maquetación (menos usos de mediaqueries, toma de medidas...)</li>
</ol>

## Y esto, ¿A que viene?, ¿Las web actuales no son buenas?

Para nada, se siguen usando mediaqueries, unidades en %, vw, vh, vmax, vmin

Se podría simplificar la maquetación Responsive, o al menos, conseguir una web más fluida

No implica que siempre se tenga que usar, ni siempre tendrá sentido aplicar estos métodos

Este planteamiento no pretende simplificar el diseño, hay otros aspectos como imágenes, iconos, grid de productos... a los que esto pudiera no aplicar. Por ejemplo, para un grid de productos puede no interesar que los tamaños no sean lineales y si "escalonados". Pueden darse casos especiales que requieran diseño especial y maquetación acorde

## Calculadora de tamaños VW en función de tamaños mínimos / máximos para tamaño de pantalla mínimo / máximo

Si miraste el Pen anterior, para insertar el valor habrás visto "unidades" con muchos decimales. En este Pen puedes obtener los cálculos a modo de calculadora

<iframe height="393" style="width: 100%;" scrolling="no" title="Calculadora CSS clamp() viewport" src="https://codepen.io/ivan_albizu/embed/rNjwLxE?height=393&theme-id=2608&default-tab=result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/ivan_albizu/pen/rNjwLxE'>Calculadora CSS clamp() viewport</a> by Iván Albizu
  (<a href='https://codepen.io/ivan_albizu'>@ivan_albizu</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

<a href="https://github.com/ivanalbizu/css-clamp" target="_blank" rel="noopener">Código en mi GitHub</a>
