**Escaner de Puertos en mi PC**
```Java
import java.io.IOException;
import java.net.ServerSocket;

public class EscanearPuertos {

	public static void main(String[] args) {
		// TODO Auto-generated method stub

		System.out.println("Start!");
		int i = 0;
		ServerSocket socket;

		for (i = 0; i < 65535; i++) {

			try {
				socket = new ServerSocket(i);

			} catch (IOException e) {
				System.out.println("Puerto: " + i + " abierto!");
			}

		}
	}

}
```
___
