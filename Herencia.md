#### Ejercicio con Herencia
* Empleado
```Java

public class Empleado {

	private String nombre;

	public Empleado() {

	}

	public Empleado(String nombre) {
		this.nombre = nombre;
	}

	public String getNombre() {
		return nombre;
	}

	public void setNombre(String nombre) {
		this.nombre = nombre;
	}

	public String toString() {
		return " Empleado " + this.nombre + " ->";
	}
}
```



* Operario
```Java

public class Operario extends Empleado {
	
	public Operario(String nombre) {
		super(nombre);
	}


	public String toString() {
		return super.toString() + " Operario " + " ->";
	}
}

```
* Directivo
```Java

public class Directivo extends Empleado {

	
	public Directivo(String nombre) {
		super(nombre);
	}
	public String toString() {
		return super.toString() + " Directivo ";
	}
}
```
* Tecnico
```Java

public class Tecnico extends Operario {

	public Tecnico(String nombre) {
		super(nombre);
	}

	public String toString() {
		return super.toString() + " Tecnico ";
	}
}
```
* Oficial
```Java

public class Oficial extends Operario {

	public Oficial(String nombre) {
		super(nombre);
	}
	
	public String toString() {
		return super.toString() + " Oficial ";
	}
}
```
* Programa Principal
```Java

public class ProgramaPrincipal {

	public static void main(String[] args) {
		// TODO Auto-generated method stub

		Empleado E1 = new Empleado("Rafa");
		Empleado D1 = new Directivo("Mario");
		Empleado OP1 = new Operario("Alfonso");
		Empleado OF1 = new Oficial("Luis");
		Empleado T1 = new Tecnico("Pablo");
		
		System.out.println(E1);
		System.out.println(D1);
		System.out.println(OP1);
		System.out.println(T1);
	
	}

}
```
