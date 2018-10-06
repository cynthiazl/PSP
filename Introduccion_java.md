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
La sobrecarga de métodos se utiliza para para que podamos reutilizar el nombre de un método pero con diferentes argumentos. Haremos uso de un método sobrecargado **cuando al desarrollar el proyecto veamos que, en diferentes ocasiones vamos a necesitar de un mismo método diferentes cosas.**  
En el siguiente ejemplo veremos que la clase "Perro" hemos sobrecargado el método "cambiar". Como podrás observar el méto mencionado nateriormente se ha **definido tres veces**, con un parametro de tipo String, uno de tipo Int y con dos de tipoString e Int.  
Desta manera yo podré utilizar cada método para un "Perro" diferente, obteniendo así de cada uno el resultado que yo quiera.
```JAva
public class Perro
{
    private String nombre;
    private int edad;

    public Perro(String nombre, int edad)
    {
        this.nombre = nombre;
        this.edad = edad;
    }

    public String getNombre()
    {
        return nombre;
    }

    public int getEdad()
    {
        return edad;
    }

    public void cambiar(String nombre)
    {
        this.nombre = nombre;
    }

    public void cambiar(int edad)
    {
        this.edad = edad;
    }

    public void cambiar(String nombre, int edad )
    {
        this.nombre = nombre;
        this.edad = edad;
    }
}
```
Veamos ahora como pasamos los parametros a cáda método. 
```Java
public class PruebaPerro
{
    public static void main(String[] args)
    {
        Perro perro1 = new Perro("Chispas", 5);
        Perro perro2 = new Perro("Sombra", 3);
        Perro perro3 = new Perro("Zeus", 7);

        System.out.println(perro1.getNombre() + " tiene " + perro1.getEdad() + " años.");
        System.out.println(perro2.getNombre() + " tiene " + perro2.getEdad() + " años.");
        System.out.println(perro3.getNombre() + " tiene " + perro3.getEdad() + " años.");

        perro1.cambiar("Jaque");
        perro2.cambiar(4);
        perro3.cambiar("Goku", 8);

        System.out.println("\nDespués de los cambios:");

        System.out.println(perro1.getNombre() + " tiene " + perro1.getEdad() + " años.");
        System.out.println(perro2.getNombre() + " tiene " + perro2.getEdad() + " años.");
        System.out.println(perro3.getNombre() + " tiene " + perro3.getEdad() + " años.");
    }
}
```
___
* #### Herencia
Podemos definir la herencia en programación de Java como la manera de plasmar distintos objetos que comparten características en común.
Evoquemos el comienzo de esto, cuando estábamos viendo que era una clase, si recuerdas la definición, *decía que una clase es todo aquello que engloba diferentes características de un mismo tipo de cosas* como por ejemplo coches, bares, fincas y mascotas.  
Bien si tenemos nuestra clase “Coche” podemos darnos cuenta de que hay varios tipos de coche todos con “factor común” y a su vez con características que los diferencian. Podemos ver que tenemos coches deportivos, también coches familiares y  todoterreno. 

**Coche es nuestra clase “padre” y de ella descienden las clases “hijo” que comparten cosas, o características,** como por ejemplo todos los coches tienen una cilindrada, todos tienen puertas, cambio de marcha(automático o manual), y todos tienen plazas para los ocupantes. 
Luego podemos ver que cada tipo de coche tiene una cilindrada diferente, diferente número de puertas, unos tendrán el cambio de marchas automático y otros manual, y variara el número de plazas.
```Java
package cotxes;
//Coche es la Super clase y de ella desciende la clase CocheCanmbioAutomatico
public class CotxeCanviAutomatic extends Cotxe{ 
	
	//nuestro constructor vacio
	public CotxeCanviAutomatic(String matri) {
		//en eset momento hacemos referencia a la clase Padre
		super(matri);
	}
	//método ascelerar
	public void acelerar(double ace){
		this.velocitat+=ace;
	if (velocitat>=0 && velocitat<=10){
		this.marxa=1;
	}
	else if(velocitat>10 && velocitat<=30){
		this.marxa=2;
	}
	else if(velocitat>30 && velocitat<=50){
		this.marxa=3;
	}
	else if(velocitat>50 && velocitat<=70){
		this.marxa=4;
	}
	else if(velocitat>70){
		this.marxa=5;
	}
	}
	//Un método para frenar
	public void frenar(double fren){
		this.velocitat-=fren; 
	if (velocitat>=0 && velocitat<=10){
		this.marxa=1;
	}
	else if(velocitat>10 && velocitat<=30){
		this.marxa=2;
	}
	else if(velocitat>30 && velocitat<=50){
		this.marxa=3;
	}
	else if(velocitat>50 && velocitat<=70){
		this.marxa=4;
	}
	else if(velocitat>70){
		this.marxa=5;
	}
	}
	//De esta manera lo imprimimos por pantalla
	@Override
	public String toString(){
		return "Coche automàtic\n=========================\nMatrícula: " + this.matricula + 
		"\nvelocitat: " + this.velocitat + "\nmarxa: " + this.marxa;
	}
}
```
___
* #### Polimorfismo 
*Es cuando objetos distintos comparten propiedades.*
Como verás en el ejemplo siguiente, se usa la palabra "abstract", esto quiere decir que no podremos hacer un **new SeleccionFutbol()** es una clase abstracta y por lo tanto no se puede instanciar.  
También hemos usado la palabra abstract para un método (entrenamiento), por lo cual todas las clases "hijas" de la clase "SeleccionFutbol" **tienen que implementar este método por obligación.**  
Por estos motivos podemos decir que la clase "SeleccionFutbol" puede adoptar diferentes formas y en el siguiente ejemplo puede tener la forma de "Futbolista" aunque podría tener otras formas como "Entrenador", "Masajista", "Arbitro", en fin, modos que formasen parte de una "SeleccionFutbol" y compartiesen las mismas características id, nombre, apellidos y edad.
```Java
public abstract class SeleccionFutbol {

	protected int id;
	protected String nombre;
	protected String apellidos;
	protected int edad;

	// constructores, getter y setter

	public void viajar() {
	     System.out.println("Viajar (Clase Padre)");
	}

	public void concentrarse() {
	     System.out.println("Concentrarse (Clase Padre)");
	}

	// IMPORTANTE -> METODO ABSTRACTO => no se implementa en la clase abstracta pero si en la clases hijas
	public abstract void entrenamiento();

	public void partidoFutbol() {
	     System.out.println("Asiste al Partido de Fútbol (Clase Padre)");
	}
}
```
```Java
public class Futbolista extends SeleccionFutbol {

   private int dorsal;
   private String demarcacion;

   // constructor, getter y setter

   @Override
   public void entrenamiento() {
      System.out.println("Realiza un entrenamiento (Clase Futbolista)");
   }

   @Override
   public void partidoFutbol() {
      System.out.println("Juega un Partido (Clase Futbolista)");
   }

   public void entrevista() {
      System.out.println("Da una Entrevista");
   }
}
```
___
* #### Interface 
Una interface es una lista de acciones que puede hacer un objeto determinado, a diferencia de los métodos, en una interface sólo está el prototipo de una función pero no su código.
___
