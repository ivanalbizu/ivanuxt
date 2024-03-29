---
title: Ejemplo de programa Java para tienda
published: true
description: Programa construido en Java que simula una tienda. Permite mostrar los productos, cantidad, precio, disponibilidad. Cantidad de productos añadidos, precio unitario y total
tags:
  - java
ctime: "2014-10-10 15:10:00"
---

Ejemplo de programa Java para tienda de venta de juegos, música y películas. Al final del post añado vínculo para descargar el programa y probarlo y un vídeo explicando el código.

El programa está compuesto de seis clases: <code>Test.java</code>, <code>Gestion.java</code>, <code>Producto.java</code>, <code>Cine.java</code>, <code>Musica.java</code> y <code>Videojuego.java</code>. La clase producto define propiedades comunes de los tipos Cine, Música y Videjuego, y cada una de estas define sus propios atributos. La clase Gestión, como su nombre indica, gestiona la tienda y la clase Test ejecuta el programa. Como se ha comentado, la clase principal que ejecuta el programa es la <code>Test</code>.

El código es el siguiente:

```java
package ejerc03;
import leer.*;
public class Test {

  public static void main(String[] args) {
    /*
     * Sólo se debe añadir métodos para establecer los valores de los atributos, poder imprimirlos datos en pantalla y calcular cantidad a pagar según el precio de venta. De momento, no hace falta gestionar el almacén con los artículos que quedan, sólo se pedirá la cantidad de artículos que lleva el cliente y se dará el precio a pagar según esa cantidad. 
     */
    
    System.out.println("Bienvenido a la tienda de JUEGOS, MÚSICA Y PELÍCULASn--------n"+
              "El programa simula una tienda que vende juegos, música y películasn"+
              "Los artículos sólo se pueden vender si están disponibles en la tiendan"+
              "El usuario puede:n"+
              "t Comprar productos de los existentes.n"+
              "t Añadir nuevos productos a la cesta.n"+
              "t Consultar el importe de la cuenta.");
    
    boolean continuar = true;
    int lecturaProducto, lecturaCantidad; //Variables para seleccionar el producto y la cantidad que se quiere comprar
    
    //Se instancian y cargan los productos
    Producto disco1 = new Musica("Portishead", 18.53, 6, true, "Trip Hop");
    Producto disco2 = new Musica("Radiohead", 21.2, 20, true, "Rock");
    Producto cine1  = new Cine("Hierro 3", 30.2, 5, true, "Kim Ki Duk");
    Producto juego1 = new Videojuego("Mario Bross", 35.11, 0, false, "Plataformas");
    
    //Se crea el array "catálogo" para contener los productos. Su dimensión viene del número de veces que se
    //instancia el contructor de Producto
    Producto catalogo[] = new Producto[Producto.dimesionArray];
    //Se crea el objeto gestion para trabajar (mostrar y vender productos, y mostrar caja)
    Gestion gestion = new Gestion();

    //Se rellena el array catálogo
    catalogo[0] = disco1;
    catalogo[1] = disco2;
    catalogo[2] = cine1;
    catalogo[3] = juego1;
    
    do {
      System.out.println("nnIntroduzca la opción que desea realizar:n"
                +"1. Mostrar productosn"
                +"2. Vender productosn"
                +"3. Mostrar cajan"
                +"SALIR --> Pulse cualquier otro númeron"
                );
      switch (Leer.datoInt()) {
        case 1:
          gestion.mostrarProductos(catalogo);
          break;
        case 2:
          System.out.println("¿Que producto desea comprar?");
          gestion.mostrarNombreProductos(catalogo);
          lecturaProducto=Leer.datoInt();
          System.out.println("¿Cuánta cantidad desea comprar?");
          lecturaCantidad=Leer.datoInt();
          //Se carga el producto y la cantidad solicitada por el usuario
          gestion.comprarProducto(catalogo, lecturaProducto, lecturaCantidad);
          break;
        case 3:
          System.out.println(gestion.mostrarCaja() +" €");
          break;
        default:
          //Se sale del programa
          continuar=false;
      }
      
    } while(continuar);
    
    System.out.println("---- Gracias por usar la aplicación. ----");

  }
}
```

## Explicando un poco el código de Test

Se declaran tres variables. Una variable booleana <code>Continuar</code> para repetir el proceso de compra, dos variables enteras <code>lecturaProducto</code> y <code>lecturaCantidad</code> para que el usuario elija el producto que desea y su cantidad.

Se declaran y cargan cinco arrays para contener productos de tipos <code>Música</code>, <code>Cine</code> y <code>Juegos</code> que serán guardados en el array <code>Catálogo</code>. Se declara el objeto <code>Gestion</code> para realizar los procesos del programa. Al ejecutarse el programa el usuario ve un pequeño menú con las opciones: Mostrar productos, vender, mostrar caja y salir.

La opción elegida por el usuario determinará que trozo de código debe ejecutarse mediante un <code>switch</code>. Si la opción elegida es mostrar productos se le aplica el método <code>mostrarProductos(Catalogo)</code> al objeto <code>Gestion</code>. Si la opción es vender producto se muestra los nombres de los productos mediante <code>gestion.mostrarNombreProductos(catalogo)</code> y luego se solicita la cantidad de dicho producto, y se ejecuta la venta con el método: <code>gestion.comprarProducto(catalogo, lecturaProducto, lecturaCantidad)</code> en el que se pasan como parámetros el catálogo, el producto y la cantidad. Si la opción es "mostrar caja" se ejecuta el método <code>gestion.mostrarCaja()</code> que devuelve el importe de las ventas.

La última opción de salida se lleva a cabo si el usuario introduce un número diferente al 1, 2 ó 3. La clase que lleva la lógica del programa es la <code>Gestion</code>.

Su código es el siguiente:

```java
package ejerc03;

public class Gestion {
  
  //Attributes
  private Producto productos[] = null;
  private double caja;
  
  //Constructors
  public Gestion() { }
  public Gestion(Producto[] productos) {
    this.productos = productos;
  }
  
  //Methods
  public Producto[] cargarProductos() {

    return productos;
  }
  
  public void mostrarProductos(Producto[] productos) { 
      for (int i = 0; i < productos.length; i++) {
        System.out.print(productos[i]+"n-------n");
      }
  }
  public void mostrarNombreProductos(Producto[] productos) { 
      for (int i = 0; i < productos.length; i++) {
        System.out.println(i+1 +" "+productos[i].getNombre()+"n");
      }
      System.out.println("n------------n");
  }   
  public double comprarProducto(Producto[] productos, int num, int cantidadUnidades) {
    if (productos[num-1].isDisponible()) {
      if (productos[num-1].getCantStock() >= cantidadUnidades){
        System.out.println("La compra se ha realizado con éxito!!n");
        productos[num -1].setCantStock(productos[num -1].getCantStock()-cantidadUnidades);
        return caja+=cantidadUnidades*productos[num-1].getPrecioUnit();
      } else {System.out.println("No hay cantidad suficiente de producto");}
    } else {System.out.println("No hay cantidad suficiente de producto");}
    return caja;
  }
  public double mostrarCaja() {
    System.out.print("El total de la caja es ");
    caja=Math.round(caja*100);
    return caja/100;
  } 
}
```

## Explicando un poco el código de Gestion

En la clase <code>Gestion</code> se declaran dos atributos, un array de tipo <code>Producto</code> para contener los productos y otro de tipo <code>Double</code> para contener el importe.

Se declaran dos constructores, uno vació y otro que carga el array de productos.

Esta clase contiene 5 métodos.

El primero, <code>public Producto[] cargarProductos()</code>, devuelve el array de productos.

El segundo, <code>public void mostrarProductos(Producto[] productos)</code>, recibe como parámetro el array de productos que se mostrarán.

El tercer método, <code>public void mostrarNombreProductos(Producto[] productos)</code>, es parecido al anterior, con la diferencia que dentro de su código se llama al código método <code>getNombre()</code> para imprimir por pantalla el nombre en lugar de todo el array de productos.

El cuarto método, public double <code>comprarProducto(Producto[] productos, int num, int cantidadUnidades)</code>, recibe el array de productos, un entero identificador del producto seleccionado y otro entero para la cantidad de productos elegida por el usuario. Este método, comprueba que el producto seleccionado exista <code>if (productos[num-1].isDisponible())</code> y que la cantidad seleccionada sea menor que la cantidad en stock <code>if (productos[num-1].getCantStock() >= cantidadUnidades)</code>. En el caso que la compra se pueda llevar a cabo cumpliendo las condiciones anteriores, la cantidad de productos en stock será actualizado <code>productos[num -1].setCantStock(productos[num -1].getCantStock()-cantidadUnidades)</code> y se añadirá el importe de la compra a la caja: <code>caja+=cantidadUnidades\*productos[num-1].getPrecioUnit()</code>.

El último método, <code>public double mostrarCaja()</code>, devuelve entero que indica el importe de la venta actual <code>caja=Math.round(caja*100); return caja/100;</code>.

## Explicando un poco el código de Producto

En la clase Producto se definen atributos comunes a los tipos <code>Música</code>, <code>Videojuego</code> y <code>Cine</code>: <code>nombre</code>, <code>precioUnit</code>, <code>cantStock</code> y <code>disponible</code>. Se crea un cuarto atributo estático llamado <code>dimensionArray</code> para que cuando en la clase Test se cree el catálogo de productos le podamos designar la dimensión de este array directamente usando esta variable: <code>Producto catalogo[] = new  producto[Producto.dimesionArray]</code> (cada nueva creación de objeto Producto incrementa en uno la dimensión).

En esta clase también generamos los <code>getters</code> y <code>setters</code> para acceder a los atributos. También el método <code>toString()</code>. Uno de los métodos generados <code>public boolean isDisponible()</code> lo modificamos un poco. En la declaración de atributos pusimos a <code>false</code> la disponibilidad, con lo que siempre figura que no existe producto, para ello usamos: <code>if(getCantStock()>0) this.disponible = true;</code> sabremos si hay disponibilidad.

El código de la clase <code>Producto</code> es el siguiente:

```java
package ejerc03;

public abstract class Producto {

  //Attributes
  private String nombre;
  private double precioUnit;
  private int cantStock;
  private boolean disponible = false;
  public static int dimesionArray;
  
  
  //Constructors
  public Producto() { }
  public Producto(String nombre, double precioUnit, int cantStock, boolean disponible) {
    this.nombre   = nombre;
    this.precioUnit = precioUnit;
    this.cantStock  = cantStock;
    this.disponible = disponible;
    
    dimesionArray++;//Se obtiene con esta variable la dimensión del array. Según número de instancias del constructor
  }
  
  
  //Methods
  @Override
  public String toString() {
    return  "Nombre: "      +this.getNombre()+    "n"+
        "Precio unidad: " +this.getPrecioUnit()+  " €n"+
        "En Stock: "    +this.getCantStock()+ "n";
  }
  
  //Get and Set
  public String getNombre() {
    return this.nombre;
  }
  public void setNombre(String nombre) {
    this.nombre = nombre;
  }
  public double getPrecioUnit() {
    return this.precioUnit;
  }
  public void setPrecioUnit(double precioUnit) {
    this.precioUnit = precioUnit;
  }
  public int getCantStock() {
    return this.cantStock;
  }
  public void setCantStock(int cantStock) {
    this.cantStock = cantStock;
  }
  public boolean isDisponible() {
    if(getCantStock()>0) this.disponible = true;
    return this.disponible;
  }
  public void setDisponible(boolean disponible) {
    this.disponible = disponible;
  }

}
```

## Resto de clases

Las tres clases restantes: <code>Musica</code>, <code>Videojuego</code> y <code>Cine</code> se crean por <code>herencia</code> de la clase padre <code>Producto</code>. Por darle un poco de diferencia, he añadido un atributo a cada una de ellas: "genero", "tematica" y "director". Por herencia se crean los constructores y método <code>toString()</code>. Y se añaden getters y setters de los nuevos atributos. Para no añadir mucho código, copio el código de la clase <code>Musica</code>:

```java
package ejerc03;

public class Cine extends Producto {

  //Attribute
  private String director;

  
  //Constructor
  public Cine() { }
  public Cine(String nombre, double precioUnit, int cantStock, boolean disponible, String director) {
    super(nombre, precioUnit, cantStock, disponible);
    this.director = director;
  }
  
  
  //Methods
  @Override
  public String toString() {
    return  "ARTÍCULO DE CINEn"+
        super.toString()+
        "Director: "  +this.director;
  }
  
  //Gets and Sets
  public String getDirector() {
    return director;
  }
  public void setDirector(String director) {
    this.director = director;
  }
}
```

## Clase de utlidad Leer

Lo único a mencionar de esta clase es que en su declaración inicial se añade la palabra reservada <code>extends</code> indicando que extiende de la clase padre <code>Producto</code>.

```java
package leer;

import java.io.*;

public class Leer {

	public static String dato() {
		String sdato = " ";
		try {
			InputStreamReader isr = new InputStreamReader(System.in);
			BufferedReader flujoE = new BufferedReader(isr);
			sdato = flujoE.readLine();
		} catch (IOException e) {
			System.out.println("Error " + e.getMessage());
		}
		return sdato;

	}

	public static int datoInt() {
		return Integer.parseInt(dato());
	}

	public static float datoFloat() {
		return Float.parseFloat(dato());
	}

	// Leer un char por teclado

	public static char datoChar() {
		char c = ' ';
		try {
			java.io.BufferedInputStream b = new BufferedInputStream(System.in);
			c = (char) b.read();
		} catch (IOException e) {
			System.out.println("Error al leer");
			e.printStackTrace();
		}
		return c;
	}

	public static long datoLong() {
		return Long.parseLong(dato());
	}
}
```

En este vídeo explico el código:

<div class="ratio-16-9">
    <iframe title="Programa ehemplo crear tienda en Java" type="text/html" src="http://www.youtube.com/embed/FqQSwOSC830?autoplay=0&origin=https://ivanalbizu.eu/" frameborder="0"></iframe>
</div>
