**1º Ejercicio para la evaluación**
****Consiste en un chat con varios clientes, utilizando sockets y cmd****
+ Clase Servidor
```java
import java.io.IOException;
//import java.net.InetSocketAddress;
import java.net.ServerSocket;
import java.net.Socket;
import java.util.ArrayList;
import java.util.List;
import java.io.DataOutputStream;
import java.io.IOException;
import java.net.ServerSocket;
import java.net.Socket;
import java.util.Scanner;

public class Servidor {

	static void run() {
		try {
			int i = 1;
			ServerSocket serverSocket = new ServerSocket(8189);

			while (true) {
				Socket socket = serverSocket.accept();
				System.out.println("Que bien " + i);
				new Cliente(socket);
				i++;
			}
		} catch (IOException ex) {
			ex.printStackTrace();
		}
	}

	static void sendAll(String message) {
		for (Cliente handler : clientes) {
			handler.getOut().println(message);
		}
	}

	static List<Cliente> getHandlers() {
		return clientes;
	}

	private static List<Cliente> clientes = new ArrayList<Cliente>();

}
```
____
+ Clase Cliente
```java
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;
import java.io.PrintWriter;
import java.net.Socket;
import java.util.Scanner;
import java.io.DataOutputStream;
import java.io.IOException;
import java.net.Socket;
import java.util.Scanner;

public class Cliente extends Thread {

	private Socket incoming;
	private PrintWriter out;

	Cliente(Socket incoming) {
		this.incoming = incoming;
		this.start();
	}

	@Override
	public void run() {

		try {
			try {
				Servidor.getHandlers().add(this);

				InputStream inputStream = incoming.getInputStream();
				OutputStream outputStream = incoming.getOutputStream();

				Scanner scanner = new Scanner(inputStream);
				out = new PrintWriter(outputStream, true /* autoFlush */);

				out.println("dev::hubot.pl - Telnet Chat Demo");

				out.println("Elige tu nik para el chat:");
				String nick = "";
				nick = scanner.nextLine();

				out.println("Holi! escribe exit para salir");

				boolean conexion = false;
				while (!conexion && scanner.hasNextLine()) {
					String line = scanner.nextLine();
					Servidor.sendAll(nick + ": " + line);
					if (line.trim().equals("BYE"))
						conexion = true;
				}

			} finally {
				incoming.close();
			}
		} catch (IOException ex) {
			ex.printStackTrace();
		}
	}
	PrintWriter getOut() {
		return out;
	}
}
```
____
+ Clase App
```java

public class App {

	public static void main(String[] args) {
		Servidor.run();
	}

}
```
____
***Véase una imagen de ejemplo***

<img src="https://github.com/cynthiazl/PSP/blob/master/chatSockets.png" width="350"/>


