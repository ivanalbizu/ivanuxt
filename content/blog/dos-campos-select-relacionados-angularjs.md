---
title: Dos campos Select relacionados en AngularJS
published: true
description: Construir Selects en el que uno de los Selects carga su contenido en función del option seleccionado en el Select anterior
tags:
  - angularJS
  - javascript
  - pildoritas
ctime: "2016-10-10 15:10:00"
cover_image: dos-campos-select-relacionados-en-angularjs.jpg
alt_image: Dos campos Select relacionados en AngularJS
---

He construido sistema de filtros con etiquetas <code>&lt;select&gt;</code>. Uno de ellos será el filtro inferior y el otro el filtro superior. Ambos estarán relacionados entre sí para que no se pisen los valores, y así el valor tomado por el filtro inferior sea uno de los límites del filtro superior, y viceversa.

Para darle valores a los <code>&lt;select&gt;</code> he construido un filtro que recibe tres parámetros. Los dos primeros parámetros, <code>min</code> y <code>max</code>, son los límites inferiores y superiores. El tercer parámetro, <code>step</code>, será la separación entre cada uno de los valores, que caso de no especificarse este valor tomará el valor 30000.

```javascript
(function() {
  'use strict';

  angular
    .module('app')
    .filter('filterRange', function () {
      return function (input, min, max, step) {
        step = parseInt(step) || 30000;
        min = parseInt(min);
        max = parseInt(max);
        for (var i = min; i < max; i += step)
          input.push(i);
        return input;
      };
    });

})();
```

La forma de usarla es sencilla. Se usará la directiva <code>ng-options</code> de AngularJS que genera los diferentes valores seleccionables. Le pasamos un array vacío y le aplicamos el filtro. (Ojo, el uso de la directiva <code>ng-options</code> requiere también la definición de <code>ng-model</code>. En este trozo de código no lo puse)

```html
<select ng-options="n for n in [] | filterRange:0:120000:30000"></select>
```

En el controlador definimos una variable para usarlo en la vista como modelo. Con valores mínimos y máximos definidos con valor para que se carguen los valores por defecto.

```javascript
(function() {
  'use strict';

  angular
    .module('app', [])
    .controller('ListHouseCtrl', ListHouseCtrl);

    ListHouseCtrl.$inject = [];
    function ListHouseCtrl() {

      var vm = this;

      vm.selectPrice = {
        min: 30000,
        max: 120000
      }

      vm.log = function() {
        console.log(vm.selectPrice);
      }

    }

})();
```

A ambos <code>&lt;select&gt;</code> le asignamos su modelo para obtener el valor seleccionado, que en su primera carga será el valor por defecto.

```html
<select ng-model="vm.selectPrice.min" ng-options="n for n in [] | filterRange:0:120000:30000"></select>
<select ng-model="vm.selectPrice.max" ng-options="n for n in [] | filterRange:150000:250000:30000"></select>
```

Ahora mismo se rellenan ambos <code>&lt;select&gt;</code>, el primero termina en 120000 y el segundo empieza en 150000. Pero podemos aprovechar los valores que hemos guardado en <code>ng-model="vm.selectPrice.min"</code> y en <code>ng-model="vm.selectPrice.max"</code> para los límites de los filtros.

```html
<select ng-model="vm.selectPrice.min" ng-options="n for n in [] | filterRange:0:vm.selectPrice.max:30000"></select>
<select ng-model="vm.selectPrice.max" ng-options="n for n in [] | filterRange:vm.selectPrice.min+30000:250000:30000"></select>
```

El código se encuentra en mi <a href="https://github.com/ivanalbizu/select_angular" target="_blank">repositorio de GitHub.</a>

Vídeo de campos relacionados en AngularJS 1

<div class="ratio-16-9"><iframe title="Campos relacionados en AngularJS 1" type="text/html" src="http://www.youtube.com/embed/xnti8Iz-m8c?autoplay=0&origin=https://ivanalbizu.eu/" frameborder="0"></div>