---
title: Programa Java gestionar ascensor
published: true
description: Programa Java que simula el comportamiento de un ascensor para controlar las paradas, movimientos subida, bajada y número de personas
tags:
  - java
ctime: "2014-02-11 15:10:00"
---

El siguiente programa java intenta modelar el funcionamiento básico de un ascensor. Para ello se crean dos clases, <code>Principal.java</code> y <code>Ascensor.java</code>.

La clase <code>Ascensor.java</code> tiene como **atributos** el "pisco actual", la "planta máxima" y la "planta mínima", así como la cantidad máxima de personas. Esta clase tiene el **constructor** vacío y un constructor que recibe un entero de piso actual. Se generan los <code>gets</code> y <code>sets</code> del atributo "piso actual". Se crean dos **métodos** booleanos de comprobación. Para validar que el número de personas no sea mayor a la permitida y que la planta a la que se desea ir no sea el mismo en el que se está.

Se crean dos métodos void para subir y bajar plantas. Y métodos void para mostrar "cerrando" o "abriendo" puertas cuando proceda. Se crea un método principal void denominado "ir", que será el que gestione los desplazamientos y los mensajes. Si se cumple el número máximo de personas, que se encuentra en una planta diferente a la que se desea ir y que la planta elegida esté dentro del rango, en ese caso se produce el movimiento y a cada movimiento se muestra el mensaje "subiendo" o "bajando" según proceda.

```java
package ejerc01;

import leer.*;

public class Principal {

	public static void main(String[] args) {

		System.out.println("Bienvenido al ascensor FOUR ROOMS \n---------\n"
				+ "El programa gestiona el funcionamiento de un ascensor \n"
				+ "Se entra en la Planta Baja(0). Tiene 2 sótanos y 6 plantas sobre rasante \n"
				+ "El número máximo de personas es 5 \n---------");

		boolean repetir = true;

		int plantaElegida;
		int cantidadPersonas;
		Ascensor viaje = new Ascensor();

		do {
			//Se solicita PLANTA y Nº PERSONAS
			System.out.println("¿A qué planta quieres ir?");
			plantaElegida=Leer.datoInt();
			System.out.println("¿Cuántas personas soys?");
			cantidadPersonas=Leer.datoInt();

			//Se ejecuta la clase Ascensor con losdatos del usuario
			viaje.ir(plantaElegida, cantidadPersonas);

			//Se da la posibilidad de usar nuevamente el ascensor
			System.out.println("\n\n------------\n¿Quiere ir a otra planta? "
					+ "\nPulse: \n1 en caso afirmativo \nCualquier número en caso negativo");
			if(Leer.datoInt() != 1){
				repetir=false;
				System.out.println("Que tenga usted un buen día");
			}
		} while(repetir);

	}
}
```

La primera vez que se ejecute el programa el ascensor se encuentra en la planta 0 (baja). Se crean atributos tipo entero "planta elegida" y "cantidad de personas", y un objeto instanciado (llamado viaje) de tipo Ascensor con con el que operar.

Al usuario se le piden dos datos:

<ul class="list-bullets">
	<li>Planta a la que desea ir</li>
	<li>Número de personas</li>
</ul>

Estos datos son pasados como parámetros al objeto viaje.

```java
package ejerc01;

import leer.*;

public class Principal {

	public static void main(String[] args) {

		System.out.println("Bienvenido al ascensor FOUR ROOMS n---------n"
				+ "El programa gestiona el funcionamiento de un ascensor n"
				+ "Se entra en la Planta Baja(0). Tiene 2 sótanos y 6 plantas sobre rasante n"
				+ "El número máximo de personas es 5 n---------");

		boolean repetir = true;

		int plantaElegida;
		int cantidadPersonas;
		Ascensor viaje = new Ascensor();

		do {
			//Se solicita PLANTA y Nº PERSONAS
			System.out.println("¿A qué planta quieres ir?");
			plantaElegida=Leer.datoInt();
			System.out.println("¿Cuántas personas soys?");
			cantidadPersonas=Leer.datoInt();

			//Se ejecuta la clase Ascensor con losdatos del usuario
			viaje.ir(plantaElegida, cantidadPersonas);

			//Se da la posibilidad de usar nuevamente el ascensor
			System.out.println("nn------------n¿Quiere ir a otra planta? "
					+ "nPulse: n1 en caso afirmativo nCualquier número en caso negativo");
			if(Leer.datoInt() != 1){
				repetir=false;
				System.out.println("Que tenga usted un buen día");
			}
		} while(repetir);
	}
}
```

El programa da la posibilidad de repetirse, utilizando como planta actual la última a la que se ha ido, y el número de personas siempre se solicita.