---
title: Cursor Blend Mode
description: Animación de cursor en evento mousemove aplicando blend-mode a imágenes y elementos html
published: true
tags:
  - javascript
  - css
ctime: "2022-08-31 22:10:00"
cover_image: cursor-blend-mode.jpg
alt_image: Cursor Blend Mode
---

La idea es jugar un poco con el cambio de propiedades blend-mode en la que se cambie visualización de imagen y de cursor. Blend-mode fusiona colores e imágenes de elementos

<ul class="list-bullets">
  <li>Para imágenes con <code>background-blend-mode</code></li>
  <li>Para resto de elementos <code>mix-blend-mode</code></li>
</ul>

Una imagen de fondo a la que se le da también color para que "fusione" con las diferentes opciones de blend-mode

```javascript
const blendModes = [
  'normal',
  'multiply',
  'screen',
  'overlay',
  'darken',
  'lighten',
  'color-dodge',
  'color-burn',
  'hard-light',
  'soft-light',
  'difference',
  'exclusion',
  'hue',
  'saturation',
  'color',
  'luminosity',
];
```

Y elementos <code>&lt;span&gt;</code> con definición de color de fondo y blend-mode para que "fusione". Se mezcla además con la imagen de fondo ya que queda por encima de la imagen

Los elementos <code>&lt;span&gt;</code> son creados (y eliminados pasado un tiempo) cuando se produce el evento <code>mousemove</code> para dar esa sensación de "persecución" del ratón. Podría ajustarse este evento y aplicarlo para desktop y crear otra versión para "touchables"

Entrando a comentar código

## Estilos blend-mode para imagen de fondo

He usado variables CSS para actualizar sus valores desde javascript y probar de manera fácil las combinaciones que se quieran

```scss
:root {
  --img-color: rgba(255, 255, 255, 0.5);
  --img-blend-mode: multiply;
}
body {
  // color de fondo + imagen de fondo
  background: var(--img-color) url('../img/tree.jpg') no-repeat center;
  background-size: cover;
  // definición de fusión blend-mode
  background-blend-mode: var(--img-blend-mode);
}
```

## Estilos blend-mode para el span "cursor"

También he usado variables CSS. Igual que antes: color de fondo y fusión blend-mode

```scss
:root {
  --frame-color: rgba(255, 255, 255, 0.3);
  --frame-blend-mode: overlay;
}
// clase que se añade a los span creados con 'mousemove'
.circle {
  // color de fondo
  background-color: var(--frame-color);
  // definición de fusión blend-mode
  mix-blend-mode: var(--frame-blend-mode);
}
```

## Animación mediante @keyframes

He aplicado animación a los span que "siguen" al cursor aplicando <code>@keyframes</code> a atributos color de fondo, escalado y blur

```scss
@keyframes fadeout {
  to {
    background-color: rgba(255, 255, 255, 0);
    transform: scale(var(--scale-end));
    filter: blur(calc(var(--blur-end) * 1px));
  }
}
```

## javascript para animaciones blend-mode

Antes de entrar en detalle voy a comentar las funciones JS que he usado como helpers en todo el código. Comentado en el snippet :)

### Helper functions

```javascript
// Obtener el valor CSS de un atributo de un elemento DOM dado
const getCSSProp = (element, propName) =>
  getComputedStyle(element).getPropertyValue(propName);
```

```javascript
// Crear elementos DOM:
//    Tag HTML
//    Atributos
//    Crear más nodos dentro de manera recursiva o texto
const elFactory = (type, attributes, ...children) => {
  const el = document.createElement(type);

  for (key in attributes) {
    el.setAttribute(key, attributes[key]);
  }

  children.forEach((child) => {
    if (typeof child === 'string')
      el.appendChild(document.createTextNode(child));
    else el.appendChild(child);
  });

  return el;
};
```

```javascript
// Eliminar nodo cuando termina la animación (listener)
// Se elimina también el listener anterior
const deleteAnimatedNode = (el) => {
  el.addEventListener(
    'animationend',
    () => {
      el.removeEventListener('animationend', this);
      el.remove();
    },
    true
  );
};
```

### Creación de nodos con "mousemove"

He decidido crear nuevos nodos cada vez que el usuario mueve el ratón con la posición X e Y del cursor que son eliminados después de 1 segundo con la modificación CSS de los atributos que he comentado más arriba

```javascript
const handlerMousemove = (event) => {
  // Obtención de las coordenadas
  const [x, y] = [Math.floor(event.clientX), Math.floor(event.clientY)];
  // Creación de span con
  //  - clase circle
  //  - seteo de Custom Property para posiciones X / Y
  //    con corrección para que se centro del span
  const el = elFactory('span', {
    class: `circle`,
    style: `--x: ${x - CONFIG['--w-frame'] / 2}px; --y: ${
      y - CONFIG['--h-frame'] / 2
    }px`,
  });
  // Añadir nodo al DOM
  body.appendChild(el);
  // Eliminar el nodo cuando termina la animación
  deleteAnimatedNode(el);
};
```

### Librería dat.gui para "debug"

En esta parte es donde más código javascript tenemos para poderlo customizar usando <a href="https://www.npmjs.com/package/dat.gui" target="_blank" rel="noopener">dat.gui</a>

Obtenemos los valores de las variables CSS y creamos un objeto con dichos valores que serán usados más tarde en dat.gui

```javascript
const body = document.body;
const root = document.documentElement;

// Obtener los valores que tengamos en CSS
const wFrame = getCSSProp(root, '--w-frame');
const hFrame = getCSSProp(root, '--h-frame');
const radius = getCSSProp(root, '--radius');
const blurStart = getCSSProp(root, '--blur-start');
const blurEnd = getCSSProp(root, '--blur-end');
const scaleEnd = getCSSProp(root, '--scale-end');
const imgBlendMode = getCSSProp(root, '--img-blend-mode').trim();
const frameBlendMode = getCSSProp(root, '--frame-blend-mode').trim();

// Se crea un objeto con los valores que serán personalizables
// usando dat.gui
const CONFIG = {
  '--w-frame': +wFrame,
  '--h-frame': +hFrame,
  '--radius': +radius,
  '--blur-start': +blurStart,
  '--blur-end': +blurEnd,
  '--scale-end': +scaleEnd,
  '--img-color': 'rgba(255,255,255,0.5)',
  '--frame-color': 'rgba(255, 255, 255, 0.3)',
  '--img-blend-mode': imgBlendMode,
  '--frame-blend-mode': frameBlendMode,
};
```

Método auxiliar para usarlo cuando se produzcan cambios en alguna propiedad

```javascript
const update = (target, link) => (value) => {
  root.style.setProperty(`${target}`, value);
  if (CONFIG.linked && link) {
    CONFIG[link] = value;
    root.style.setProperty(`${link}`, value);
    gui.updateDisplay();
  }
};
```

Importación de dat.gui

```javascript
const {
  dat: { GUI },
} = window;
const gui = new GUI();
```

La librería permite campos para números, colores, select... en cada caso se puede cambiar los parámetros que se pasan, incluso dar nombres (esto no quise personalizarlo, aparecerán los nombres de las variables CSS)

El primer parámetro

```javascript
// Al método .add pasamos:
//  Objeto de CONFIG + Key, min, max
// Si se producen cambios actualizamos valor de la Key
gui.add(CONFIG, '--w-frame', 5, 200).onChange(update('--w-frame'));
gui.add(CONFIG, '--h-frame', 5, 200).onChange(update('--h-frame'));

// Creamos anidación
const cursor = gui.addFolder('Cursor');
cursor.add(CONFIG, '--radius', 0, 50).onChange(update('--radius'));
cursor.add(CONFIG, '--blur-start', 0, 20).onChange(update('--blur-start'));
cursor.add(CONFIG, '--blur-end', 0, 20).onChange(update('--blur-end'));
// El escalado va de 0 a 1 con steps de 0.1
cursor.add(CONFIG, '--scale-end', 0, 1, 0.1).onChange(update('--scale-end'));
cursor
  .addColor(CONFIG, '--frame-color', 'rgba(255, 255, 255, 0.3)')
  .onChange(update('--frame-color'));
cursor
  .add(CONFIG, '--frame-blend-mode', blendModes)
  .onChange(update('--frame-blend-mode'));

const image = gui.addFolder('Image');
image
  .addColor(CONFIG, '--img-color', 'rgba(255,255,255,0.5)')
  .onChange(update('--img-color'));
image
  .add(CONFIG, '--img-blend-mode', blendModes)
  .onChange(update('--img-blend-mode'));
```

Enlaces:

<a href="https://github.com/ivanalbizu/cursor-blend-mode" target="_blank" rel="noopener">Código en GitHub</a>

<a href="https://codepen.io/ivan_albizu/pen/Yzamdeo" target="_blank" rel="noopener">Codepen</a>

<a href="/blog/slides-usando-blend-mode-y-document-fragment/" target="_blank" rel="noopener">Otra publicación usando blend-mode</a>
