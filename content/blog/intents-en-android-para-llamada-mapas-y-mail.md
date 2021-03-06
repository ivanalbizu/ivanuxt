---
title: Intents en Android para llamada, mapas y mail
published: true
description: Uso de Intents en Android para comunicar información con ejemplos de lanzado de llamadas, mapas y mail
tags:
  - android
  - java
ctime: "2014-10-28 15:10:00"
---

Aplicación Android usando Intents para lanzar aplicación de llamada, búsqueda en mapa google y enviar mail.

Los pasos para hacer este proyecto son:

<ol class="list-bullets">
	<li>Declarar las **variables** en <code>MainActivity.java</code> y crear referencias de la vista XML.</li>
	<li>Se asigna **listener al botón llamar** con el texto que ha introducido el usuario.</li>
	<li>Se asigna **listener al botón buscar** en mapa la dirección que ha introducido el usuario.</li>
	<li>Se asigna **listener al botón enviar mail.**</li>

La declaración de variables la he realizado dentro del método <code>onCreate(...)</code>

```java
//Se declaran y se referencian las variables de la vista XML
final Button btnLlamar = (Button) findViewById(R.id.buttoncall);
final Button btnBuscarMapa = (Button) findViewById(R.id.buttonsearch);
final Button btnEnviarMail = (Button) findViewById(R.id.buttonsendmail);
```

Listener para el botón de realizar llamada

```java
//Se asigna listener al botón llamar con el texto que ha introducido el usuario
btnLlamar.setOnClickListener(new View.OnClickListener(){
	public void onClick(View v){
		
		//Se obtiene campo teléfono introducido por el usuario
		final EditText numeroTelefono = (EditText) findViewById(R.id.txtnumbercall);
		String numero = numeroTelefono.getText().toString();
		
		//Si no existe teléfono, se asigna teléfono de emergencias
		if (numero.equals("")) {
			numero = "112";
		}
		//Se parse el teléfono a URI
		Uri number = Uri.parse("tel:"+numero);
		
		//Se lanza el intent para llamada
		Intent callIntent = new Intent(Intent.ACTION_DIAL, number);
		startActivity(callIntent);
	}
});
```

Listener para buscar en mapa

```java
//Se asigna listener al botón buscar en mapa la dirección
// que ha introducido el usuario
btnBuscarMapa.setOnClickListener(new View.OnClickListener() {
	public void onClick(View v) {
		
		//Se obtiene la dirección introducida por el usuario
		final EditText localizacion = (EditText) findViewById(R.id.txtsearchmap);
		String buscado = localizacion.getText().toString();
		
		//Se parsea la dirección
		Uri location = Uri.parse("http://maps.google.co.in/maps?q="+buscado);
		
		//Se lanza el intent paramostra mapa
		Intent mapIntent = new Intent(Intent.ACTION_VIEW, location);
		startActivity(mapIntent);
	}
});
```

Listener para el envió de mail

```java
//Se asigna listener al botón enviar mail
btnEnviarMail.setOnClickListener(new View.OnClickListener() {
	public void onClick(View v) {
		
		//Se obtienen los campos introducidos por el usuario
		final EditText destinatario = (EditText) findViewById(R.id.txtmailuser);
		String dest = destinatario.getText().toString();
		final EditText asunto = (EditText) findViewById(R.id.txtmailsubject);
		String asun = asunto.getText().toString();
		final EditText cuerpo = (EditText) findViewById(R.id.txtmailbody);
		String cuer = cuerpo.getText().toString();
		
		//Se crea el intent para envío demail
		Intent emailIntent = new Intent(Intent.ACTION_SEND);
		
		//Se añaden campos extras para enviar mail
		emailIntent.setType("text/plain");
		emailIntent.putExtra(Intent.EXTRA_EMAIL, new String[] {dest});	//Destinatario
		emailIntent.putExtra(Intent.EXTRA_SUBJECT, asun);				//Asunto
		emailIntent.putExtra(Intent.EXTRA_TEXT, cuer);					//Cuerpo mail
		//Se lanza la actividad
		startActivity(Intent.createChooser(emailIntent, "Send email..."));
	}
});
```

La explicación de esta entrada ha sido escueta, es sencillo de entender directamente leyendo del código con sus comentarios.

He creado un vídeo del paso seguido para este proyecto Android:

<div class="ratio-16-9">
    <iframe title="Intents en Android para lanzar llamada, mapas y mail" type="text/html" src="http://www.youtube.com/embed/PuM4JO23VtM?autoplay=0&origin=https://ivanalbizu.eu/" frameborder="0"></iframe>
</div>

<a href="https://db.tt/CWIfbv3J" target="_blank">Descargar el programa Android para llamar, buscar en mapa y enviar mail</a>