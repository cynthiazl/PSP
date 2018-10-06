# Introducción a Java
#### Mi intención es que todo tipo de persona pueda entender los pilares de la programación, aún sin tener conocimientos previos sobre ésta.
* #### Clase
* #### Objeto
¿Qué es una clase Java?. Podemos decir que es, todo lo que engloba las características propias que define a un mismo objeto.   
Para entenderlo mejor pondré unos ejemplos.  
Cuando vamos por la calle nos topamos con diferentes tipos de objetos como, coches, personas, fincas, bares…
La palabra tipo y clase son sinónimos por lo que ahora cambiaremos la frase “tipos de objetos” por “clases de objetos”, dejemoslo en clases, así que ahora mismo estamos rodeados de “clases”. Para seguir aprendiendo vamos a elegir una clase de las mencionadas anteriormente. 
Yo me quedo con la clase coche, tú puedes elegir la que quieras. Una vez tengas tu clase elegida pasamos al siguiente nivel. 

Preguntémonos...Cómo son los coches? ¿Qué características diferencian a unos coches de otros?
Podríamos decir que todos los coches tienen una matrícula, un color, un modelo, una marca, un estado (a pasado la ITV o no la ha pasado).
A estas características les vamos a llamar atributos. En programación dirás que tu clase “coche” tiene los atributos que he ido listando antes. 
Es momento de pensar en el comportamiento de las clases.
La pregunta que debemos hacernos ahora es ¿Qué cosas hacen?¿Qué acciones pueden realizar?

Pues un coche por ejemplo, puede arrancar, puede frenar, acelerar, encender las luces, girar a la derecha, también puede pasar la itv o no pasarla.
A estas acciones que deciden el comportamiento(frenar) de una clase(coche) se les conoce en programación como **métodos.**
Como ya sabemos una clase es algo concreto que define el comportamiento y las características de un determinado tipo de objetos.
Pensemos en la clase como una plantilla de la cual se pueden fabricar objetos concretos.

Teniendo en cuenta todo lo anterior, podemos crear el coche que queramos utilizando los atributos(características) que nos apetezca y así obtendremos coches concretos, todos coches pero diferentes entre sí.

Coche primerCoche =  new Coche();
Ahora tenemos un coche al que hemos llamado “primerCoche”, pertenece a la clase coche y le daremos las características que queramos.

Una vez tenemos creado el coche, *debemos saber que “primerCoche” no va a contener en sí al objeto en sí, sino que contiene una dirección de memoria que apunta a él.* Esto significa que Java le ha dedicado un **espacio concreto en la memoria** para guardar todo lo que le otorgues a “primerCoche”.

***La palabra “new” se usa para crear nuevos objetos.***
Ahora le vamos a proporcionar características a nuestro coche.

primerCoche.color = “Negro”;
primerCoche.marca=”Opel”;
primerCoche.pasoItv = false;

Como puedes ver, hemos decidido que nuestro coche sea de color negro, de la marca opel y no ha pasado la itv.
```Java

package vehiculo;
import java.util.*;

public class Coche {//Esto es una clase
	public static Scanner teclado = new Scanner(System.in);

	public static void main(String[] args) {//este es el centro del programa
	

	//Ahoar vamos a definir nuestras variables, las carácterticas de los ocches
	String matricula = "";
	//por defecto el coche será blanco, si queremos que sea de otro color debemos indicarlo
	String color = "blanco";
	//por defecto no hay modelo, por lo cual si no le asignamos ninguno el resultado será nulo
	String modelo  ="";
	String marca = "";
	//aqui indicamos que no se ha pasado la ITV a menos que indiquemos lo contrario, en ese caso pondremos true
	boolean pasoItv= true;
	
		velocidadDelCoche();//Llamamos al método
	}
	//Aqui creamos el metodo que va a calcular la marcha que tenemos puesta en el coche
	public static void velocidadDelCoche() {
		
		System.out.println("Con este método vamos acalcular que marcha tienes puesta en tu coche");
		System.out.println("¿A qué velocidad vas? Opta por una de las opciones");
		System.out.println("1: En reposo, voy a arrancar el coche");
		System.out.println("2: 20km/H");
		System.out.println("3: 30km/H");
		System.out.println("4: 40km/H");
		System.out.println("5: 50km/H o más");

		
		int velocidad = teclado.nextInt();
		
		
		switch (velocidad) {
		case 1:
			System.out.println("Tienes que pones la primera marcha");
			break;
		case 2:
			System.out.println("La segunda marcha");
			break;
		case 3:
			System.out.println("La tercera marcha");
			break;
		case 4:
			System.out.println("La cuarta marcha");
			break;
		case 5:
			System.out.println("Llevas puesta la quinta marcha, si quieres reducir velocidad  
			debes bajar las marchas.");
			break;
		default:
			System.out.println("Debes elegir una opción");
			break;
		}
		
	}
}
```
___
* #### Sobrecarga de métodos 
La sobrecarga de métodos se utiliza para para que podamos reutilizar el nombre de un método pero con diferentes argumentos. Haremos uso de un método sobrecargado cuando al desarrollar el proyecto veamos que, en diferentes ocasiones vamos a necesitar de un mismo método diferentes cosas.  
Digamos que de mi clase “primerCoche” en un momento dado puedo necesitar toda la información: su color, el modelo, la matrícula...Entonces creare un método al que llamaré “infoDelCoche”.
Y que en una ocasión diferente yo necesite recordar si el coche tiene la itv pasada, en este caso crearemos otro método también llamado “infoDelCoche” pero esta vez en lugar de pasarle toda la información, solo voy a pasarle la matrícula y el sistema me dirá si tengo la itv pasada o no. Esto sería un método sobrecargado.  
___
* #### Herencia
Podemos definir la herencia en programación de Java como la manera de plasmar distintos objetos que comparten características en común.
Evoquemos el comienzo de esto, cuando estábamos viendo que era una clase, si recuerdas la definición, *decía que una clase es todo aquello que engloba diferentes características de un mismo tipo de cosas* como por ejemplo coches, bares, fincas y mascotas.
Bien si tenemos nuestra clase “Coche” podemos darnos cuenta de que hay varios tipos de coche todos con “factor común” y a su vez con características que los diferencian. Podemos ver que tenemos coches deportivos, también coches familiares y  todoterreno. 
**Coche es nuestra clase “padre” y de ella descienden las clases “hijo” que comparten cosas, o características,** como por ejemplo todos los coches tienen una cilindrada, todos tienen puertas, cambio de marcha(automático o manual), y todos tienen plazas para los ocupantes. 
Luego podemos ver que cada tipo de coche tiene una cilindrada diferente, diferente número de puertas, unos tendrán el cambio de marchas automático y otros manual, y variara el número de plazas. 



