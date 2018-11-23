### Desarrollo de una barra de tareas
```Java
import java.awt.BorderLayout;
import java.awt.Dimension;
import java.awt.EventQueue;

import javax.swing.JFrame;
import javax.swing.JPanel;
import javax.swing.border.EmptyBorder;
import javax.swing.JLabel;
import java.awt.Font;
import java.awt.Graphics;
import java.awt.Image;

import javax.swing.ImageIcon;
import javax.swing.JButton;
import java.awt.event.ActionListener;
import java.awt.event.ActionEvent;
import java.awt.Color;

public class AbrirApp extends JFrame {

	private JPanel contentPane;
	private Image imagen;

	/**
	 * Launch the application.
	 */
	public static void main(String[] args) {
		EventQueue.invokeLater(new Runnable() {
			public void run() {

				try {
					AbrirApp frame = new AbrirApp();
					frame.setVisible(true);

					// Icono de la ventana
					ImageIcon img = new ImageIcon("icono.jpg");
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
	public AbrirApp() {
	
		setTitle("Barra de tareas\r\n");
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		setBounds(100, 100, 831, 573);
		contentPane = new JPanel();
		contentPane.setBackground(new Color(230, 230, 250));
		contentPane.setBorder(new EmptyBorder(5, 5, 5, 5));
		setContentPane(contentPane);
		contentPane.setLayout(null);

		JLabel lblAbrir = new JLabel("Ejecutar mis 4 aplicaciones preferidas");
		lblAbrir.setFont(new Font("Caladea", Font.BOLD, 22));
		lblAbrir.setBounds(207, 37, 396, 29);
		contentPane.add(lblAbrir);

		JButton btnSptofy = new JButton("Sptofy");
		btnSptofy.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent arg0) {
			
				try {
					// crea un proceso
					ProcessBuilder pb = new ProcessBuilder(
					"\"C:\\Users\\cynth\\AppData\\Roaming\\Spotify\\Spotify.exe\"", "");
					// parametro 1 ruta, parametro 2 especifica el archivo que quiero abrir
					pb.start();

				} catch (Exception e) {

					System.out.println("Exception " + e);
				}
			}
		});
		btnSptofy.setBounds(52, 360, 115, 29);
		contentPane.add(btnSptofy);

		//cargar imagen
		ImagePanel imagePanel1 = new ImagePanel(new ImageIcon("spotify_logo.jpg").getImage());
		imagePanel1.setBounds(60, 250, 250, 250);
		contentPane.add(imagePanel1);

		JButton btnTelegram = new JButton("Telegram");
		btnTelegram.addActionListener(new ActionListener() {
			@Override
			public void actionPerformed(ActionEvent e) {

				try {
					// crea un proceso
					ProcessBuilder pbv = new ProcessBuilder(
							"\"C:\\Users\\cynth\\AppData\\Roaming\\Telegram Desktop\\Telegram.exe\"", "");
					pbv.start();

				} catch (Exception es) {

					System.out.println("Exception " + es);
				}
			}
		});
		btnTelegram.setBounds(258, 360, 115, 29);
		contentPane.add(btnTelegram);

		//cargo la imagen
		ImagePanel imagePanel2 = new ImagePanel(new ImageIcon("telegram_logo.png").getImage());
		imagePanel2.setBounds(270, 250, 250, 250);
		contentPane.add(imagePanel2);

		JButton btnPaint = new JButton("Paint");
		btnPaint.addActionListener(new ActionListener() {

			@Override
			public void actionPerformed(ActionEvent e) {

				try {
					// crea un proceso
					ProcessBuilder pc = new ProcessBuilder("\"C:\\WINDOWS\\system32\\mspaint.exe\"", "");
					pc.start();
					
				} catch (Exception es) {
					System.out.println("Exception " + es);
				}

			}
		});
		btnPaint.setBounds(459, 360, 115, 29);
		contentPane.add(btnPaint);

		ImagePanel imagePanel3 = new ImagePanel(new ImageIcon("paint_logo.png").getImage());
		imagePanel3.setBounds(470, 250, 250, 250);
		contentPane.add(imagePanel3);

		JButton btnAndroid = new JButton("Android Studio");
		btnAndroid.addActionListener(new ActionListener() {
			@Override
			public void actionPerformed(ActionEvent e) {

				try {
					// crea un proceso
					ProcessBuilder pcd = new ProcessBuilder(
							"\"C:\\Program Files\\Android\\Android Studio\\bin\\studio64.exe\"", "");
					pcd.start();
				} catch (Exception es) {

					System.out.println("Exception " + es);
				}
			}
		});
		btnAndroid.setBounds(650, 360, 145, 29);
		contentPane.add(btnAndroid);

		ImagePanel imagePanel4 = new ImagePanel(new ImageIcon("android_logo.jpg").getImage());
		imagePanel4.setBounds(670, 250, 250, 250);
		contentPane.add(imagePanel4);
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
}
```
___
