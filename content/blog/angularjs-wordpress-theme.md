---
title: AngularJS Wordpress Theme
published: true
description: Construcción de Theme Wordpress con AngularJS 1, usando plugins de Wordpress Wp Rest Api para generar JSON de las entradas y Advanced Custom Fields (ACF) para añadir nuevos campos
tags:
  - angularJS
  - javascript
  - php
  - css
  - wordpress
ctime: "2016-10-26 15:10:00"
cover_image: angularjs-wordpress-theme.jpg
alt_image: AngularJS Wordpress Theme
---

## Instalación
Instalar el tema que se encuentra en mi <a href="https://github.com/ivanalbizu/Angular-Wordpress-Theme/" target="_blank">GitHub</a>.

## Después de habilitar el tema

<ul class="list-bullets">
	<li>Instalar y habilitar los plugins</li>
	<li>Especificar la ruta base de la instalación. En <code>header.php</code> la etiqueta <code>&lt;base href="/wordpress/"&gt;</code></li>
	<li>Importar los custom fields con el archivo <code>advanced-custom-field-export.xml</code></li>
	<li>Editar el formulario de contacto que generar Contact Form 7 por defecto.</li>
	<ul class="list-bullets">
		<li>Al campo correo electrónico añadir la siquiente ID: <code>checkvalid</code></li>
		<li>Al campo submit añadir las siguientes clases: <code>waves-effect waves-light btn cyan darken-3</code></li>
	</ul>
</ul>

## Crear contenido

<ul class="list-bullets">
	<li>Crear una página y añadir los campos necesarios</li>
	<li>Hay dos tipo de entradas: ventas y alquileres. Crear contenido para ambos (para el tipo venta hay un campo llamado "Destacada venta", la entrada que la tenga marcada se mostrará en la Home)</li>
</ul>

Para ver la <a href="http://inmo.mentiraspoliticas.es" target="_blank">demo en funcionamiento</a>.