**Página principal**
```Java
import javax.swing.*;
import java.awt.BorderLayout;
import java.awt.Color;
import java.awt.Dimension;
import java.awt.EventQueue;

import javax.swing.border.EmptyBorder;
import java.awt.Font;
import java.awt.Graphics;
import java.awt.Image;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class PaginaPrincipal extends JFrame {

	private JPanel contentPane;
	private Image imagen;

	/**
	 * Launch the application.
	 */
	public static void main(String[] args) {
		EventQueue.invokeLater(new Runnable() {

			public void run() {

				try {

					PaginaPrincipal frame = new PaginaPrincipal();
					frame.setVisible(true);

					ImageIcon img = new ImageIcon("avion.jpg");
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
	public PaginaPrincipal() {

		setTitle("Página principal de Aeropuertos");
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		setBounds(100, 100, 672, 280);
		contentPane = new JPanel();
		contentPane.setBackground(new Color(250, 208, 251));
		contentPane.setBorder(new EmptyBorder(5, 5, 5, 5));
		setContentPane(contentPane);
		contentPane.setLayout(null);

		JLabel lbTitulo = new JLabel("Buscador de Aeropuetos");
		lbTitulo.setForeground(Color.WHITE);
		lbTitulo.setHorizontalAlignment(SwingConstants.CENTER);
		lbTitulo.setFont(new Font("Verdana", Font.BOLD, 30));
		lbTitulo.setBounds(0, 48, 665, 25);
		contentPane.add(lbTitulo);

		ImagePanel imagePanel = new ImagePanel(new ImageIcon("aeropuerto.jpg").getImage());
		imagePanel.setBounds(0, 0, 665, 250);
		contentPane.add(imagePanel);

		JButton btnBuscar = new JButton("Buscar");
		btnBuscar.setBounds(289, 136, 86, 23);
		imagePanel.add(btnBuscar);
		btnBuscar.setFont(new Font("Georgia", Font.PLAIN, 16));
		btnBuscar.addActionListener(new ActionListener() {
			@Override
			public void actionPerformed(ActionEvent e) {
				Buscador nombre = new Buscador();
				nombre.setVisible(true);

			}
		});

	}

}

class ImagePanel extends JPanel {
	private Image img;

	public ImagePanel(Image img) {

		this.img = img;
		Dimension size = new Dimension(img.getWidth(null), img.getHeight(null));

		setPreferredSize(size);
		setMinimumSize(size);
		setMaximumSize(size);
		setSize(size);
		setLayout(null);
	}

	public void paintComponent(Graphics g) {
		g.drawImage(img, 0, 0, null);
	}
}
```
<img src="https://github.com/cynthiazl/PSP/blob/master/pag_principal.png" width="350"/>
```Java
import java.awt.BorderLayout;
import java.awt.Color;
import java.awt.Desktop;
import java.awt.EventQueue;
import java.awt.Font;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.io.Console;
import java.net.URI;
import java.util.ArrayList;

import javax.swing.JFrame;
import javax.swing.JPanel;
import javax.swing.border.EmptyBorder;
import javax.swing.table.DefaultTableModel;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.JTextField;
import javax.swing.DefaultListModel;
import javax.swing.JButton;
import javax.swing.JList;
import javax.swing.JTable;
import javax.swing.JComboBox;

public class Buscador extends JFrame {

	private String nomAirport = "";

	private JPanel contentPane;
	private JTextField textAeropuerto;
	private JButton btnBuscar;
	private JTable table;
	private JButton btnMapa;

	/**
	 * Launch the application.
	 */
	public static void main(String[] args) {
		EventQueue.invokeLater(new Runnable() {
			public void run() {
				try {
					Buscador frame = new Buscador();
					frame.setVisible(true);
				} catch (Exception e) {
					e.printStackTrace();
				}
			}
		});
	}

	/**
	 * Create the frame.
	 */
	public Buscador() {

		LeoFichero leeFichero = new LeoFichero();
		ArrayList<Airport> airports = leeFichero.Lee();

		setTitle("Buscador de Aeropuertos");
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		setBounds(100, 100, 630, 500);
		contentPane = new JPanel();
		contentPane.setBackground(new Color(250, 208, 251));
		contentPane.setBorder(new EmptyBorder(5, 5, 5, 5));
		setContentPane(contentPane);
		contentPane.setLayout(null);

		JLabel lbTituloBuscador = new JLabel("Buscar Aeropuerto");
		lbTituloBuscador.setBounds(220, 48, 170, 25);
		contentPane.add(lbTituloBuscador);
		lbTituloBuscador.setFont(new Font("Verdana", Font.PLAIN, 18));

		contentPane.add(lbTituloBuscador);

		JLabel lblIntroduzcaElNombre = new JLabel("Introduzca Ciudad, País o Cod Aeropuerto:");
		lblIntroduzcaElNombre.setFont(new Font("Verdana", Font.PLAIN, 14));
		lblIntroduzcaElNombre.setBounds(10, 129, 304, 14);
		contentPane.add(lblIntroduzcaElNombre);

		JLabel informo = new JLabel("");
		informo.setForeground(Color.RED);
		informo.setBounds(324, 128, 270, 20);
		contentPane.add(informo);

		// Recojo el texto
		textAeropuerto = new JTextField();
		textAeropuerto.setBounds(324, 128, 270, 20);
		contentPane.add(textAeropuerto);
		textAeropuerto.setColumns(10);

		JComboBox comboBoxResultado = new JComboBox();
		comboBoxResultado.setBounds(131, 270, 310, 20);
		contentPane.add(comboBoxResultado);

		btnMapa = new JButton("Mapa");
		btnMapa.setBounds(246, 353, 89, 23);
		contentPane.add(btnMapa);
		btnMapa.addActionListener(new ActionListener() {

			@Override
			public void actionPerformed(ActionEvent e) {
				// TODO Auto-generated method stub
				if (textAeropuerto.getText().isEmpty()) {

					informo.setText("Debe introducir texto");

				} else {

					Desktop browser = Desktop.getDesktop();
					String url = "https://www.google.com/maps/place/{name}/@{latitude},{longitude},15z/data=!3m1!4b1!4m5!3m4!1s0x0:0x0!8m2!3d38.2821999!4d-0.558156?hl=es";

					for (Airport aeropuerto : airports) {

						if (comboBoxResultado.getSelectedItem().equals(aeropuerto.getName().replace("\"", ""))) {

							try {

								url = url.replace("{name}",
										aeropuerto.getName().replace("\"", "").replaceAll(" ", "+"));
								url = url.replace("{latitude}", Double.toString(aeropuerto.getLatitude()));
								url = url.replace("{longitude}", Double.toString(aeropuerto.getLongitude()));

								browser.browse(new URI(url));

								System.out.println(url);

							} catch (Exception e2) {
								// TODO: handle exception
								JOptionPane.showMessageDialog(null,
										"Ha ocurrido un error insesperado: " + e2.getMessage());
							}
						}
					}
				}
			}
		});

		// Boton para buscar el aeropuerto
		btnBuscar = new JButton("Buscar");
		btnBuscar.setFont(new Font("Georgia", Font.PLAIN, 16));
		btnBuscar.setBounds(246, 162, 89, 23);
		contentPane.add(btnBuscar);

		btnBuscar.addActionListener(new ActionListener() {
			@Override
			public void actionPerformed(ActionEvent e) {

				comboBoxResultado.removeAllItems();

				if (textAeropuerto.getText().isEmpty()) {

					JOptionPane.showMessageDialog(null, "Debe introducir texto");

				} else {

					ArrayList<Airport> resultados = new ArrayList<Airport>();

					for (Airport airport : airports) {

						if ((textAeropuerto.getText().length() == 3
								&& textAeropuerto.getText().toLowerCase()
										.equals(airport.getCode().toLowerCase().replace("\"", ""))
								|| (airport.getCity().toLowerCase().contains(textAeropuerto.getText().toLowerCase())
										|| airport.getCountry().toLowerCase()
												.contains(textAeropuerto.getText().toLowerCase())
										|| airport.getName().toLowerCase()
												.contains(textAeropuerto.getText().toLowerCase())))) {

							resultados.add(airport);
							comboBoxResultado.addItem(airport.getName().replace("\"", ""));
							// System.out.println("Encontrado" + airport.getCode()+ airport.getName());
						}
					}

				}
			}
		});
	}
}
```
<img src="https://github.com/cynthiazl/PSP/blob/master/buscador.png" width="350"/>
