---
title: Badges con SASS y SVG
description: Mixing Sass para crear Badges que puedan ser modificados y adaptados mediante parámetros
published: true
tags:
  - pildoritas
  - css
  - svg
ctime: "2016-10-11 15:10:00"
cover_image: badges-sass-svg.png
alt_image: Badges con SASS y SVG
---

## Código css Badge

He construido badges con **sass y svg**. Mediante mixins de sass he creado el fondo del badge, en el que se puede personalizar el ancho, el color y el margen superior pasando los parámetros. El primer parámetro es el ancho en px (sin indicar la unidad), el siguiente el color y el último el margen al elemento superior (sin indicar la unidad).

```scss
body {
  @include badge-generator(90, #ff1744, 200);
}
```

Lo he incluido (@include) en el body para que se genere el css a partir de sass. Dichos elementos se van a generar a partir de la función @mixin. El código no tiene misterio, son operaciones para formar un hexágono.

```scss
@mixin badge-generator($width: 94, $color: #ff1744, $margin_top: 0) {
	$middle_width: $width/2;
	$height: ($width/2) * 1.154700538;
	$border_top: $height/2;

	text-align: center; //center image
	margin-top: unquote( $margin_top + 'px');

	.hexagon-draw {
		display: inline-block;
		margin-right: 10px;

		.hexagon-construct-top {
			width: 0;
			border-bottom: unquote( $border_top + 'px') solid $color;
			border-left: unquote( $middle_width + 'px') solid transparent;
			border-right: unquote( $middle_width + 'px') solid transparent;
		}
		.hexagon-construct-middle {
			width: unquote( ($width) + 'px');
			height: 54px;//width/2*1,154700538
			height: unquote( ( ($width/2) * 1.154700538 ) + 'px');
			background-color: $color;
		}
		.hexagon-construct-bottom {
			width: 0;
			border-top: unquote( $border_top + 'px') solid $color;
			border-left: unquote( $middle_width + 'px') solid transparent;
			border-right: unquote( $middle_width + 'px') solid transparent;
		}
		.hexagon-picture {
			position: relative;
			top: unquote( (-0.83 * $width) + 'px');
			height: 0;
			img {
				max-height: unquote( $middle_width + 'px');
			}
		}
	}
}
```

## Código html Badge

Para usarlo en el html hay que seguir la siguiente estructura:

```html
<div class="box-badge">
	<div class="hexagon-draw">
		<div class="hexagon-construct-top"></div>
		<div class="hexagon-construct-middle"></div>
		<div class="hexagon-construct-bottom"></div>
		<div class="hexagon-picture">
			<img src="img/badge.svg" alt="Title Badge">
		</div>
	</div>
	<div class="hexagon-draw">
		<div class="hexagon-construct-top"></div>
		<div class="hexagon-construct-middle"></div>
		<div class="hexagon-construct-bottom"></div>
		<div class="hexagon-picture">
			<img src="img/dollar-symbol.svg" alt="Title Dollar Symbol">
		</div>
	</div>
</div>
```

## Pen con ejemplo de Badge Sass Svg

<div class="ratio-16-9">
    <iframe title="Badges con SASS y SVG" src="https://codepen.io/ivan_albizu/pen/MWWEjrP"></iframe>  
</div>


En la etiqueta de imagen se le añade la imagen, puede ser en cualquier formato, pero usando "svg" se adaptará mejor a diferentes tamaños o escalados.
El código completo para probarlo se encuentra en <a href="https://github.com/ivanalbizu/Badges-with-Sass-and-Svg" target="_blank">mi GitHub</a>.
