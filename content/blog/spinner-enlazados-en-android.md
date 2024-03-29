---
title: Spinner enlazados en Android
published: true
description: Construcción de Spinners en Android cargados desde datos en formato XML y segundo Spinner en función de los seleccionado en el primero
tags:
  - android
  - java
ctime: "2014-10-31 15:10:00"
---

Spinner enlazados en Android, en el que un segundo <code>Spinner</code> carga sus contenidos en función del ítem seleccionado del primer <code>Spinner</code>.

Los pasos que he seguido para conseguirlo han sido:

<ol class="list-bullets">
	<li>Creación de arrays dentro del archivo <code>strings.xml</code>.</li>
	<li>Creación de la vista en el archivo <code>layout.xml</code>.</li>
	<li>Declaración de variables.</li>
	<li>Referenciado de variables del XML.</li>
	<li>Construcción del "adaptador" para el primer <code>Spinner</code>.</li>
	<li>Cargar el tipo de vista para el adaptador.</li>
	<li>Aplicar el adaptador al <code>Spinner</code> de localidades.</li>
	<li>Listener para saber que item ha sido seleccionado y poder usarlo en el método <code>onItemSelected</code>.</li>
	<li>Sobre escribir el método <code>onItemSelected</code> de la interfaz <code>OnItemSelectedListener</code>.
		<ol class="list-bullets">
			<li>Se guarda en array de enteros los arrays de las provincias.</li>
			<li>Construcción del adaptador para el segundo <code>Spinner</code>.</li>
			<li>Se carga el tipo de vista para el adaptador.</li>
			<li>Se aplica el adaptador al <code>Spinner</code> de localidades.</li>
		</ol>
	</li>
</ol>

Creación de los arrays para los <code>Spinner</code>:

```xml
<string-array name="array_provincias">
    <item>Sevilla</item>
    <item>Málaga</item>
</string-array>

<string-array name="array_sevilla">
    <item>Villanueva del Ariscal</item>
    <item>Tomares</item>
    <item>Mairena del Aljarafe</item>
</string-array>

<string-array name="array_malaga">
    <item>Casares</item>
    <item>Manilva</item>
    <item>Estepona</item>
</string-array>
```

Creación de Spinner en la vista:

```xml
<Spinner
    android:id="@+id/spinnerProvincia"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_alignParentTop="true"
    android:layout_centerHorizontal="true"
    android:layout_marginTop="40dp" />

<Spinner
    android:id="@+id/spinnerLocalidad"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_below="@+id/spinnerProvincia"
    android:layout_centerHorizontal="true"
    android:layout_marginTop="66dp" />
```

Declaración y referenciado de los <code>Spinner</code>:

```java
//Declaración de variables
private Spinner spinnerPro, spinnerLoc;

@Override
protected void onCreate(Bundle savedInstanceState) {
  super.onCreate(savedInstanceState);
  setContentView(R.layout.activity_main);
  
  //Referenciado de variables del XML
  spinnerPro = (Spinner) findViewById(R.id.spinnerProvincia);
  spinnerLoc = (Spinner) findViewById(R.id.spinnerLocalidad);

  /*------ Método OnCreate continua ------*/
```

Adaptador para primer <code>Spinner</code>:

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
  /*------ Método continuado ------*/

    //Construcción del "adaptador" para el primer Spinner
  ArrayAdapter<CharSequence> adapter = ArrayAdapter.createFromResource(
    this, 
    R.array.array_provincias, //Se carga el array definido en el XML
    android.R.layout.simple_spinner_item);
  
  //Se carga el tipo de vista para el adaptador
  adapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item);
  
  //Se aplica el adaptador al Spinner de localidades
  spinnerPro.setAdapter(adapter);
  //Se aplica listener para saber que item ha sido seleccionado
  //y poder usarlo en el método "onItemSelected"
  spinnerPro.setOnItemSelectedListener(this);
}
```

Segundo <code>Spinner</code>, enlazado:

```java
//Sobre escrito el método "onItemSelected" de
//la interfaz "OnItemSelectedListener"
@Override
public void onItemSelected(AdapterView<?> parent, View view, int position, long id) {
  //Se guarda en array de enteros los arrays de las provincias
  int[] localdades = {R.array.array_sevilla,R.array.array_malaga};
  
  //Construcción del "adaptador" para el segundo Spinner
  ArrayAdapter<CharSequence> adapter = ArrayAdapter.createFromResource(
    this,
    localidades[position],//En función de la provincia, se carga el array que corresponda del XML
    android.R.layout.simple_spinner_item);
  
  //Se carga el tipo de vista para el adaptador
  adapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item);
  
  //Se aplica el adaptador al Spinner de localidades
  spinnerLoc.setAdapter(adapter); 
}
```

He creado un vídeo en el que realizo este ejemplo de Spinner enlazados en Android:

<div class="ratio-16-9">
	<iframe title="Spinner enlazados en Android" type="text/html" src="http://www.youtube.com/embed/AtuZoSpbypI?autoplay=0&origin=https://ivanalbizu.eu/" frameborder="0"></iframe>
</div>
