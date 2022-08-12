---
title: Componente icono para angular mediante SVG Sprites Symbols
published: true
description: Creación de componente Angular para pintado de SVG que permita ajustes de ancho / alto / color mediante un fichero SVG linkado mediante símbolo
tags:
  - javascript
ctime: "2022-04-17 19:30:00"
cover_image: svg-sprite-symbol-angular.png
alt_image: Componente icono para angular mediante SVG Sprites Symbols
---

<iframe src="https://codesandbox.io/embed/kind-cloud-kmfru7?fontsize=14&hidenavigation=1&theme=dark&view=editor"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="kind-cloud-kmfru7"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

## Librería usada

Usando como dependencia de desarrollo la librería https://www.npmjs.com/package/svg-sprite

## Definición de tarea script para generación de SVG sprite

Añadiendo script para la generación de SVG partiendo de ficheros SVG independientes:

```
"scripts": {
  "svg-sprite": "svg-sprite -s --symbol-dest src/assets/sprites --symbol-sprite svg-sprite.svg src/assets/icons/*.svg"
}
```

## Fichero typescript del componente:

```typescript
import { Component, Input, OnInit } from '@angular/core';

@Component({
  selector: 'app-svg-icon',
  templateUrl: './svg-icon.component.html',
  styleUrls: ['./svg-icon.component.scss']
})
export class SvgIconComponent implements OnInit {
  @Input() id = '';
  @Input() width = '40px';
  @Input() height = '40px';
  @Input() color = '#414141';

  constructor() { }

  ngOnInit(): void {
  }

}
```

Se define la ID del atributo para obtener la referencia del símbolo, sus dimensiones ancho / alto y color del SVG

## Definición del componente

```html
<svg [attr.width]="width" [attr.height]="height" [style.color]="color">
  <use [attr.xlink:href]="'/assets/sprites/svg-sprite.svg#' + id"></use>
</svg>
```

## Estilo del componente

Lo importante aquí es que al SVG le decimos que su <code>fill</code> es <code>currentColor</code> ya que lo que hacemos en javascript es dar valor a la propiedad color

```css
:host {
  display: inline-flex;
}
svg {
  fill: currentColor;
}
```

<a href="https://github.com/ivanalbizu/svg-sprite-symbol-angular" target="_blank" rel="noopener">Código en GitHub</a>

<a href="https://codesandbox.io/s/kind-cloud-kmfru7?file=/src/app/components/svg-icon/svg-icon.component.ts" target="_blank" rel="noopener">Ejemplo en Codesandbox</a>
