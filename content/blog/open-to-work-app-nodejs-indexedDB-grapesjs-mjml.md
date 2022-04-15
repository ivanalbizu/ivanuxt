---
title: Aplicación con nodejs para maquetación de emails y envío con nodemailer
published: true
description: Aplicación nodejs para maquetación de emails con frameworks MJML y grapesjs y envío de emails de pruebas con nodemailer y configuración SMTP
tags:
  - nodejs
  - pug
  - mjml
  - grapesjs
ctime: "2021-03-20 15:10:00"
cover_image: open-to-work-app.jpg
alt_image: Aplicación nodejs maquetación de emails y envío con nodemailer
---

He realizado una APP para poder hacer maquetación de Emails con Framework MJML, grapesjs, datatables, backend con nodejs + pug + nodemailer, guardado en base de datos localmente en el navegador con indexedDB

La aplicación la inicié con la idea de poder diseñar currículum y poder enviar correos para la búsqueda de empleo, de ahí el nombre: AppToWork, en concreto para mi hermano, para tratar de ayudarle con la búsqueda de empleo, afortunádamente, ha encontrado empleo :)

Conforme la iba haciendo he ido usando cosas que ya tenía a nivel profesional para hacer unos Test de Emails, así que he aprendido y podido sacar partido profesionalmente

Para la App he usado:

<ul class="list-bullets">
  <li><code>Nodejs</code> para el backend y las vistas con <code>Pug</code></li>
  <li><code>Nodemailer</code> para las configuración de envíos de emails con SMTP de yahoo</li>
  <li>Guardado en BBDD local en el navegador con <code>indexedDB</code></li>
  <li>Framework <code>MJML</code> para la maquetación de Emails</li>
  <li>Framework javascript <code>Grapesjs</code> para el builder drag and drop de Emails</li>
  <li><code>Datatables</code> para representar los contactos creados por el usuario</li>
</ul>

La Aplicación la tengo <a href="https://opentowork.herokuapp.com/" target="_blank" rel="noopener">subida en Heroku</a>. Si has entrado anteriormente, antes del 20/03/2021, deberías borrar la Base de datos, ya que no he contemplado la actualización de la base de datos al nuevo esquema. (Suponiendo el caso de Chrome sería en: <code>Application -> Storage -> indexedDB -> nodemailer, pulsas en "Delete database"</code>. Con estos pasos, una vez recarges la página, se te volverá a generar la base de datos con el esquema final)

Es una App orientada a ser App de escritorio. No sé si más adelante me dará por aprender Quasar o Electron para ver si consigo crear la App de escritorio

<a href="https://github.com/ivanalbizu/opentowork" target="_blank" rel="noopener">Código en mi GitHub</a>