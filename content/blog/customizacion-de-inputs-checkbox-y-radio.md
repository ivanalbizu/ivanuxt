---
title: Customización de inputs checkbox y radio
published: true
description: Customización de elementos de formulario tipo checkbox y radio con elementos SVG y animación con stroke-dasharray y stroke-dashoffset
tags:
  - html
  - css
  - svg
ctime: "2021-05-30 15:10:00"
cover_image: custom-checkbox-radio-buttons-with-SVG.jpg
alt_image: Customización de inputs checkbox y radio
---

Una entrada breve sobre customización de Inputs de tipo <code>checkbox</code> y <code>radio</code>

Mi idea es seguir mejorándolo y hacerlo más reutilizable, de momento dejo el código

<iframe height="483" style="width: 100%;" scrolling="no" title="Custom Checkbox / Radio buttons with SVG" src="https://codepen.io/ivan_albizu/embed/qBrVoGj?height=483&theme-id=2608&default-tab=css,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/ivan_albizu/pen/qBrVoGj'>Custom Checkbox / Radio buttons with SVG</a> by Iván Albizu
  (<a href='https://codepen.io/ivan_albizu'>@ivan_albizu</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

```html
<main class="main">

  <div class="talla">
    <h2 class="title">Tallas</h2>
    <div class="labels-radio-rect talla-instance">
      <label class="label">
        <input class="input" type="radio" name="size-product-01" checked>
        <span class="label__checkmark">
          <svg class="shape" xmlns="http://www.w3.org/2000/svg">
            <rect class="shape-rect" />
          </svg>
          <span class="outline">30</span>
        </span>
      </label>
      <label class="label">
        <input class="input" type="radio" name="size-product-01" checked>
        <span class="label__checkmark">
          <svg class="shape" xmlns="http://www.w3.org/2000/svg">
            <rect class="shape-rect" />
          </svg>
          <span class="outline">31</span>
        </span>
      </label>
      <label class="label">
        <input class="input" type="radio" name="size-product-01">
        <span class="label__checkmark">
          <svg class="shape" xmlns="http://www.w3.org/2000/svg">
            <rect class="shape-rect" />
          </svg>
          <span class="outline">32</span>
        </span>
      </label>
      <label class="label">
        <input class="input" type="radio" name="size-product-01">
        <span class="label__checkmark">
          <svg class="shape" xmlns="http://www.w3.org/2000/svg">
            <rect class="shape-rect" />
          </svg>
          <span class="outline">33</span>
        </span>
      </label>
    </div>
  </div>

  <div class="sexo">
    <h2 class="title">Sexo</h2>
    <div class="labels-radio-circle sexo-instance">
      <label class="label">
        <input class="input" type="radio" name="sex">
        <span class="label__checkmark">
          <svg class="shape" xmlns="http://www.w3.org/2000/svg">
            <circle class="shape-circle" />
          </svg>
          <span class="outline"></span>
          <span class="input-text">Mujer</span>
        </span>
      </label>
      <label class="label">
        <input class="input" type="radio" name="sex">
        <span class="label__checkmark">
          <svg class="shape" xmlns="http://www.w3.org/2000/svg">
            <circle class="shape-circle" />
          </svg>
          <span class="outline"></span>
          <span class="input-text">Hombre</span>
        </span>
      </label>
      <label class="label">
        <input class="input" type="radio" name="sex" checked>
        <span class="label__checkmark">
          <svg class="shape" xmlns="http://www.w3.org/2000/svg">
            <circle class="shape-circle" />
          </svg>
          <span class="outline"></span>
          <span class="input-text">Hexadecimal</span>
        </span>
      </label>
    </div>
  </div>

  <div class="politica">
    <h2 class="title">Privacidad</h2>
    <div class="labels-radio-rect labels-radio-rect--row politica-instance">
      <label class="label">
        <input class="input" type="checkbox" name="politica">
        <span class="label__checkmark">
          <svg class="shape" xmlns="http://www.w3.org/2000/svg">
            <rect class="shape-rect" />
          </svg>
          <span class="outline"></span>
          <span class="input-text">Casí lo he leído todo</span>
        </span>
      </label>
      <label class="label">
        <input class="input" type="checkbox" name="politica">
        <span class="label__checkmark">
          <svg class="shape" xmlns="http://www.w3.org/2000/svg">
            <rect class="shape-rect" />
          </svg>
          <span class="outline"></span>
          <span class="input-text">Pero aún así lo consiento</span>
        </span>
      </label>
    </div>
  </div>

</main>
```

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
	font-family: 'Montserrat', sans-serif;
	font-weight: 400;
	background: #fff;
	color: #242424;
}
h1, h2, h3, h4, h5, h6, p {
  margin-block-start: 0;
  margin-block-end: 0;
  margin-inline-start: 0;
  margin-inline-end: 0;
  font-weight: 300;
}

.main {
	display: grid;
	grid-template-columns: repeat(3, auto);
	//place-content: center;
	margin: 1em;
}
.title {
	margin-bottom: .4em;
}
.label {
	-webkit-user-select: none;
	-moz-user-select: none;
	-ms-user-select: none;
	user-select: none;
	.input {
		position: absolute;
		opacity: 0;
		cursor: pointer;
		height: 0;
		width: 0;
		margin: 0;
	}
}

.talla-instance {
	--label-radio-rect-w: 56;
	--label-radio-rect-h: 44;
	--color-bg-active: rgba(0,0,0,.1);
	--dasharray-rect: calc(calc(var(--label-radio-rect-w) * 2) + calc(var(--label-radio-rect-h) * 2));
}

.sexo-instance {
	--label-radio-circle-w: 20;
	--label-radio-circle-r: calc(var(--label-radio-circle-w) / 2);
	--color-bg-active: rgba(0,0,0,.1);
	--dasharray-circle: calc(2 * 3.14 * var(--label-radio-circle-r));
}

.politica-instance {
	--label-radio-rect-w: 24;
	--label-radio-rect-h: 24;
	--color-bg-active: rgba(0,0,0,.1);
	--dasharray-rect: calc(calc(var(--label-radio-rect-w) * 2) + calc(var(--label-radio-rect-h) * 2));
}


.labels-radio-rect {
	display: flex;
	margin-bottom: 1.2em;
	&--row {
		flex-direction: column;
		.label {
			margin-bottom: .4em;
		}
	}
	.label {
		&:not(:last-of-type) {
			margin-right: .6em;
			transition: margin .4s ease;
		}
		display: grid;
		gap: 0;
		position: relative;
		width: calc(var(--label-radio-rect-w) * 1px);
		height: calc(var(--label-radio-rect-h) * 1px);
		cursor: pointer;
		input {
			&:checked ~	.label__checkmark .shape-rect {
				stroke-dashoffset: 0;
				fill: var(--color-bg-active);
			}
			&:focus ~	.label__checkmark .shape-rect {
				fill: var(--color-bg-active);
			}
		}
		&__checkmark {
			display: grid;
			align-items: center;
			width: inherit;
			height: inherit;
			.shape,
			.outline {
				grid-area: 1 / 1 / 2 / 2;
				width: inherit;
				height: inherit;
			}
			.shape-rect {
				width: inherit;
				height: inherit;
				stroke-dasharray: var(--dasharray-rect);
				stroke-dashoffset: var(--dasharray-rect);
				stroke-width: 1px;
				fill: rgba(255,255,255,0);
				stroke: #111;
				transition: stroke-dashoffset 1s;
			}
			.outline {
				font-size: 1em;
				color: #242424;
				width: 100%;
				height: 100%;
				border: .5px solid rgba(0,0,0,.1);
				display: flex;
				justify-content: center;
				align-items: center;
				transition: color .5s ease .1s;
			}
			.input-text {
				grid-area: 1 / 2 / 2 / 2;
				padding-left: 10px;
				white-space: nowrap;
			}
			&:hover .shape-rect {
				stroke-dashoffset: 0;
			}
		}
	}
}


.labels-radio-circle {
	display: flex;
	margin-bottom: 1.2em;
	flex-direction: column;//
	.label {
		&:not(:last-of-type) {
			margin-right: .6em;
			transition: margin .4s ease;
		}
		display: grid;
		gap: 0;
		position: relative;
		width: calc(var(--label-radio-circle-w) * 1px);
		height: calc(var(--label-radio-circle-w) * 1px);
		cursor: pointer;
		font-size: 1em;
		margin-bottom: 10px;//
		input {
			&:checked ~	.label__checkmark .shape-circle {
				stroke-dashoffset: 0;
				fill: var(--color-bg-active);
			}
			&:focus ~	.label__checkmark .shape-circle {
				fill: var(--color-bg-active);
			}
		}
		&__checkmark {
			display: grid;
			align-items: center;
			width: inherit;
			height: inherit;
			.shape,
			.outline {
				grid-area: 1 / 1 / 2 / 2;
				width: inherit;
				height: inherit;
			}
			.shape-circle {
				cx: var(--label-radio-circle-r);
				cy: var(--label-radio-circle-r);
				r: calc(var(--label-radio-circle-r) - .5);
				width: inherit;
				height: inherit;
				stroke-dasharray: var(--dasharray-circle);
				stroke-dashoffset: var(--dasharray-circle);
				stroke-width: 1px;
				fill: rgba(255,255,255,0);
				stroke: #111;
				transition: stroke-dashoffset 1s;
			}
			.outline {
				font-size: 1em;
				color: #242424;
				width: 100%;
				height: 100%;
				border-radius: 50%;
				border: .5px solid rgba(0,0,0,.1);
				display: flex;
				justify-content: center;
				align-items: center;
				transition: color .5s ease .1s;
			}
			.input-text {
				grid-area: 1 / 2 / 2 / 2;
				padding-left: 10px;
				white-space: nowrap;
			}
			&:hover .shape-circle {
				stroke-dashoffset: 0;
			}
		}
	}
}
```