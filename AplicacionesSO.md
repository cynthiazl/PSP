## Aplicaciones del Sistema Operativo
* Abrir aplicación de PDF
* Abrir una hoja de cálculo
* Mostrar por consola la versión instalada de Java

```Java
import java.awt.BorderLayout;
import java.awt.EventQueue;

import javax.swing.JFrame;
import javax.swing.JPanel;
import javax.swing.border.EmptyBorder;
import javax.swing.JLabel;
import java.awt.Font;

import javax.swing.ImageIcon;
import javax.swing.JButton;
import java.awt.event.ActionListener;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.awt.event.ActionEvent;
import java.awt.Color;

public class AbrirAp extends JFrame {

	private JPanel contentPane;

	/**
	 * Launch the application.
	 */
	public static void main(String[] args) {
		EventQueue.invokeLater(new Runnable() {
			public void run() {
				try {
					AbrirAp frame = new AbrirAp();
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
	public AbrirAp() {
		//Modifico el titulo de la ventana
		setTitle("Aplicaciones del SO");
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		setBounds(100, 100, 676, 609);
		contentPane = new JPanel();
		contentPane.setBackground(new Color(224, 255, 255));
		contentPane.setBorder(new EmptyBorder(5, 5, 5, 5));
		setContentPane(contentPane);
		contentPane.setLayout(null);

		//titulo
		JLabel lblAbrirAplicacionesDel = new JLabel("Abrir Aplicaciones del Sistema Operativo");
		lblAbrirAplicacionesDel.setFont(new Font("Malgun Gothic Semilight", Font.BOLD, 24));
		lblAbrirAplicacionesDel.setBounds(90, 79, 474, 33);
		contentPane.add(lblAbrirAplicacionesDel);

		// creo un boton y le asigno la imagen del pdf
		JButton btn_pdf = new JButton(new ImageIcon("pdf_logo.png"));

		btn_pdf.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent arg0) {

				try {
					// crea un proceso
					ProcessBuilder p = new ProcessBuilder("\"C:\\Program Files (x86)\\Adobe\\Acrobat Reader DC\\Reader\\AcroRd32.exe\"",
							"");
					p.start();
				} catch (Exception es) {
					System.out.println("Exception " + es);
				}
			}
		});
		btn_pdf.setBounds(80, 235, 110, 110);
		contentPane.add(btn_pdf);

		// creo un boton y le asigno la imagen de calculo
		JButton btn_calculo = new JButton(new ImageIcon("hojaCalculo_logo.png"));
		
		btn_calculo.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
			
				try {
					// crea un proceso
					ProcessBuilder pc = new ProcessBuilder("\"C:\\Program Files\\LibreOffice\\program\\scalc.exe\"",
							"");
					pc.start();
				} catch (Exception es) {
					System.out.println("Exception " + es);
				}
			}
		});
		btn_calculo.setBounds(278, 235, 104, 110);
		contentPane.add(btn_calculo);

		// creo boton y le asigno la imagen de java
		JButton btnJava = new JButton(new ImageIcon("java_logo.png"));
		
		btnJava.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				String linea;
				try {
					// crea un proceso
					Process pro = Runtime.getRuntime().exec("java -version");
					BufferedReader reader = new BufferedReader(new InputStreamReader(pro.getErrorStream()));
					
					while ((linea = reader.readLine()) != null) {
					System.out.println(linea);
					}
					System.exit(0);			
				} catch (Exception es) {
					System.out.println("Exception " + es);
				}
			}
		});
		btnJava.setBounds(476, 235, 104, 111);
		contentPane.add(btnJava);
	}
}
```
<img src="https://github.com/cynthiazl/PSP/blob/master/abrirApSO.png" width="350">

____
