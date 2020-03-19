# Proyecto-f-sica-
CLASE DIBUJAR
package fisica.Vista;

import java.awt.Color;
import java.awt.Graphics;
import java.awt.Graphics2D;
import java.awt.Image;
import java.awt.Toolkit;
import java.util.Timer;
import java.util.TimerTask;

import javax.swing.JPanel;

import fisica.Logica.Nave;

public class Dibujar extends JPanel {
private Nave nave;
private int alto=320;
private int teta=2;
	/**
	 * Create the panel.
	 */
	public Dibujar(int vlancha, int vrio) {
		setBackground (Color.WHITE); //color de fondo del juego
		nave=new Nave();
		Timer time=new Timer();
		int vestatua=4; //pruf
		
		try {
			nave.mover(vlancha,vrio);
			if(Math.abs(vlancha)>=31) {
				vestatua= (int) (31.25/31);
			}
			else
				vestatua=(int) (31.25/Math.abs(vlancha));
			
			time.wait(vestatua);//cuanto esperar para moverse mils
			if( alto== Math.abs(nave.tenery())) {//320==y
				time.cancel();
			}
		} catch (InterruptedException e) {
			e.printStackTrace();
		}
	}
	public void paint(Graphics g) {
		super.paint(g);
		Graphics2D g2=(Graphics2D) g;
		Toolkit t=Toolkit.getDefaultToolkit();
		Image nave1=t.getImage("/images/estatua.npg");
		g2.drawImage(nave1, nave.tenerx(), nave.tenery(), this);
	}
	public void setAlto(int alto) {
		this.alto = alto;
	}
	public int getAlto() {
		return alto;
	}
	
}

CLASE GAME
package fisica.Vista;

import java.awt.BorderLayout;
import java.awt.Color;
import java.awt.EventQueue;
import java.awt.Font;
import java.awt.Toolkit;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.sql.Time;

import javax.swing.ImageIcon;
import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.JPanel;
import javax.swing.JRadioButton;
import javax.swing.border.EmptyBorder;

import fisica.Logica.*;
import fisica.Vista.*;

import java.awt.Window.Type;
import java.awt.Dialog.ModalExclusionType;

public class Game extends JFrame {
	//ATRIBUTOS E INSTANCIAS PERTINENTES
	private JPanel contentPane;
	private int vlancha;
	private int vrio;

	/**
	 * Launch the application.
	 */
	public static void main(String[] args) {
		EventQueue.invokeLater(new Runnable() {
			public void run() {
				try {
					Game frame = new Game();
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
	public Game() {
		//CREA Y MODIFICA EL FRAME
		setResizable(false);
		setType(Type.UTILITY);
		setTitle("movimiento relativo");
		setFont(new Font("Lucida Calligraphy", Font.BOLD | Font.ITALIC, 18));
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		setLocationRelativeTo(null);
		setBounds(200, 50, 960, 544);
		Panel contentPane = new Panel("/images/Jugadores.png");
		getContentPane().add(contentPane);
		contentPane.setLayout(null);
		
		
		Dibujar d =new Dibujar(getVlancha(),getVrio());
	}
	public int getVlancha() {
		return vlancha;
	}
	public int getVrio() {
		return vrio;
	}

	public void setVlancha(int lancha) {
		this.vlancha = lancha;
	}

	public void setVrio(int rio) {
		this.vrio = rio;
	}
}

CLASE NAVE
package fisica.Logica;

public class Nave {
	int y=80;
	private int x;
	
	private int dx=0;
	private int dy;
	
	private int vlancha;
	private int vrio;
	
	private int teta=2;//???
/*	
	public static void main(String[] args) {
		Nave pruf = new Nave();
	}
*/	
	public Nave() {
		x=(int) (Math.random()*950+1);//donde inicia 
	}
	public void mover(int vlancha,int vrio) { //cuanto avanza
		dy=(int) (Math.abs(vlancha*Math.cos(teta)));
		if((vrio>0 && vlancha*Math.sin(teta)<0) || (vrio<0 && vlancha*Math.sin(teta)>0) ) {
			dx=(int) (Math.abs(vlancha*Math.sin(teta))-Math.abs(vrio));
		}
		else
			dx=(int) (Math.abs(vlancha*Math.sin(teta))+Math.abs(vrio));
		x+=dx;
		y+= dy;
	}
	public int tenerx() {
		return x;
	}
	public int tenery() {
		return y;
	}
}

DATOS
package fisica.Vista;

import java.awt.BorderLayout;
import java.awt.EventQueue;
import java.awt.Font;
import java.awt.Window.Type;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

import javax.swing.ImageIcon;
import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.JPanel;
import javax.swing.JSpinner;
import javax.swing.JTextField;
import javax.swing.SpinnerNumberModel;
import javax.swing.border.EmptyBorder;

import CuatroEnLinea.Vista.Game2;
import CuatroEnLinea.Vista.Panel;
import CuatroEnLinea.Vista.VentanaInicio;
import CuatroEnLinea.Vista.VentanaJugador;
import fisica.Logica.Nave;

public class Datos extends JFrame {
	//ATRIBUTOS 
	private JPanel contentPane;

	/**
	 * Launch the application.
	 */
///*
	public static void main(String[] args) {
		EventQueue.invokeLater(new Runnable() {
			public void run() {
				try {
					Datos frame = new Datos();
					frame.setVisible(true);
				} catch (Exception e) {
					e.printStackTrace();
				}
			}
		});
	}
//*/
	/**
	 * Create the frame.
	 */
	public Datos() {
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		setType(Type.UTILITY);
		setTitle("movimiento relativo");
		setLocationRelativeTo(null);
		setResizable(false);
		setBounds(200, 0, 800, 800);
		Panel contentPane = new Panel("/images/fondoInicio.jpg");
		getContentPane().add(contentPane);
		contentPane.setLayout(null);
		
		//CREA LOS COMPONENTES Y LOS POSICIONA EN EL FRAME
		JLabel Titulo = new JLabel("");
		Titulo.setIcon(new ImageIcon(VentanaInicio.class.getResource("/images/TITULO.png")));
		Titulo.setBounds(98, 86, 600, 150);
		contentPane.add(Titulo);
		
		JLabel lancha = new JLabel("Digite la velocidad del barco (m/s)");
		lancha.setFont(new Font("Agency FB", Font.BOLD, 20));
		lancha.setBounds(246, 227, 300, 40);
		contentPane.add(lancha);
		
		JSpinner vlancha = new JSpinner();
		vlancha.setModel(new SpinnerNumberModel(new Integer(0), null, null, new Integer(1)));
		vlancha.setBounds(246, 266, 300, 40);
		contentPane.add(vlancha);
		
		JLabel rio = new JLabel("Digite la velocidad del rio (m/s)");
		rio.setFont(new Font("Agency FB", Font.BOLD, 20));
		rio.setBounds(246, 317, 300, 40);
		contentPane.add(rio);
	
		JSpinner vrio = new JSpinner();
		vrio.setModel(new SpinnerNumberModel(new Integer(0), null, null, new Integer(1)));
		vrio.setBounds(246, 355, 300, 40);
		contentPane.add(vrio);
		
		//BOTON QUE CAPTURA LOS DATOS DE LOS USUARIOS Y LOS LLEVA AL FRAME DEL JUEGO
		JButton Siguiente = new JButton("");
		Siguiente.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent arg0) {
				if(!((Integer)(vlancha.getValue())).equals(0)){
					Game g=new Game();
					g.setVlancha(((Integer)(vlancha.getValue())));
					g.setVrio(((Integer)(vrio.getValue())));
					g.setVisible(true);
					g.setAlwaysOnTop(true);
					setVisible(false);
				}else{
					JOptionPane.showMessageDialog(null, "Debe Digitar un valor", "WARNING", JOptionPane.WARNING_MESSAGE);
				}
			}
		});
		Siguiente.setIcon(new ImageIcon(VentanaJugador.class.getResource("/images/ContinuarV3.jpg")));
		Siguiente.setBounds(246, 464, 300, 40);
		contentPane.add(Siguiente);
	}

}
/*		JLabel angu = new JLabel("Digite el angulo (grados)");
angu.setFont(new Font("Agency FB", Font.BOLD, 20));
angu.setBounds(246, 426, 300, 40);
contentPane.add(angu);

JSpinner angulo = new JSpinner();
angulo.setModel(new SpinnerNumberModel(new Integer(0), new Integer(0), null, new Integer(1)));
angulo.setBounds(246, 464, 300, 40);
contentPane.add(angulo);
*/
CLASE PANEL
package fisica.Vista;

import java.awt.Dimension;
import java.awt.Graphics;

import javax.swing.ImageIcon;
import javax.swing.JPanel;

public class Panel extends JPanel {
	//ATRIBUTOS
	ImageIcon imagen;
	String nombre;
	//CONSTRUCTOR
	public Panel(String nombre){
		this.nombre=nombre;
	}
	//GENERA UN PANEL PERSONALIZADO
	public void paint(Graphics g){
		Dimension tamanio= getSize();
		imagen = new ImageIcon(getClass().getResource(nombre));
		g.drawImage(imagen.getImage(), 0, 0, tamanio.width, tamanio.height, null);
		setOpaque(false);
		super.paint(g);
	}
}

CLASE VENTANA-INICIO
package fisica.Vista;

import java.awt.EventQueue;

import javax.swing.JFrame;
import javax.swing.JPanel;

import fisica.Vista.Instrucciones;
import fisica.Vista.Panel;
import fisica.Vista.VentanaInicio;
import fisica.Vista.Datos;

import javax.swing.JButton;
import javax.swing.ImageIcon;

import java.awt.Window.Type;
import java.awt.event.ActionListener;
import java.awt.event.ActionEvent;

import javax.swing.JLabel;

public class VentanaInicio extends JFrame {

	private JPanel contentPane;
	/**
	 * Launch the application.
	 */
	public static void main(String[] args) {
		EventQueue.invokeLater(new Runnable() {
			public void run() {
				try {
					VentanaInicio frame = new VentanaInicio();
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
	public VentanaInicio() {
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		setType(Type.UTILITY);
		setTitle("movimiento relativo");
		setLocationRelativeTo(null);
		setResizable(false);
		setBounds(200, 0, 800, 800);
		Panel contentPane = new Panel("/images/fondoInicio.jpg");
		getContentPane().add(contentPane);
		contentPane.setLayout(null);
		//CREA Y POSICIONA LOS COMPONENTES EN EL FRAME
		JLabel Titulo = new JLabel("");
		Titulo.setIcon(new ImageIcon(VentanaInicio.class.getResource("/images/TITULO.png")));
		Titulo.setBounds(98, 86, 600, 150);
		contentPane.add(Titulo);
		//BOTON QUE PERMITE IR A LAS OPCIONES DE JUEGO
		JButton Jugar = new JButton("");
		Jugar.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent arg0) {
				Instrucciones leer1 = new Instrucciones();
				leer1.setVisible(true);
				setVisible(false);
			}
		});
		Jugar.setIcon(new ImageIcon(VentanaInicio.class.getResource("/images/ImgBotonIniciarV1.jpg")));
		Jugar.setBounds(247, 290, 300, 40);
		contentPane.add(Jugar);
		
		//DIRIGE AL FRAME DE INSTRUCCIONES
		JButton Instrucciones = new JButton("");
		Instrucciones.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				Instrucciones leer2 = new Instrucciones();
				leer2.setVisible(true);
				setVisible(false);
			}
		});
		Instrucciones.setIcon(new ImageIcon(VentanaInicio.class.getResource("/images/ImgInstruccionesV1.jpg")));
		Instrucciones.setBounds(247, 440, 300, 40);
		contentPane.add(Instrucciones);
				
		//CIERRA EL PROGRAMA EN SU TOTALIDAD
		JButton Salir = new JButton("");
		Salir.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				dispose();
				setDefaultCloseOperation(JFrame.DISPOSE_ON_CLOSE);
				System.exit(-1);
			}
		});
		Salir.setIcon(new ImageIcon(VentanaInicio.class.getResource("/images/ImgSalirV1.jpg")));
		Salir.setBounds(247, 590, 300, 40);
		contentPane.add(Salir);
		
	}
}

CLASE RESULTADOS
package fisica.Vista;

import java.awt.BorderLayout;
import java.awt.EventQueue;

import javax.swing.JFrame;
import javax.swing.JPanel;
import javax.swing.border.EmptyBorder;
import javax.swing.JLabel;
import javax.swing.ImageIcon;

import java.awt.Font;

import javax.swing.JButton;

import fisica.Logica.*;
import fisica.Vista.*;

import java.awt.Window.Type;
import java.awt.event.ActionListener;
import java.io.DataInputStream;
import java.io.FileInputStream;
import java.awt.event.ActionEvent;

public class Resultados extends JFrame {
	//ATRIBUTOS
	private String NombreJ;
	private int score;
	private JPanel contentPane;
	private int vezjuego;
	/**
	 * Launch the application.
	 */
//	public static void main(String[] args) {
//		EventQueue.invokeLater(new Runnable() {
//			public void run() {
//				try {
//					Resultados frame = new Resultados();
//					frame.setVisible(true);
//				} catch (Exception e) {
//					e.printStackTrace();
//				}
//			}
//		});
//	}

	/**
	 * Create the frame.
	 */
	public Resultados() {
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		setType(Type.UTILITY);
		setTitle("movimiento relativo");
		setLocationRelativeTo(null);
		setResizable(false);
		setBounds(600, 0, 800, 740);
		Panel contentPane = new Panel("/images/FondoResultados.jpg");
		getContentPane().add(contentPane);
		contentPane.setLayout(null);
		//CREA LOS COMPONENTES Y LOS COLOCA EN EL FRAME
		JLabel Img = new JLabel("");
		Img.setBounds(177, 233, 437, 343);
		contentPane.add(Img);
		
		JLabel Score = new JLabel("");
		Score.setFont(new Font("Lucida Calligraphy", Font.BOLD, 30));
		Score.setBounds(415, 143, 220, 51);
		contentPane.add(Score);
		
		JLabel lblGanaste = new JLabel();
		lblGanaste.setFont(new Font("Comic Sans MS", Font.BOLD | Font.ITALIC, 60));
		lblGanaste.setBounds(227, 61, 331, 71);
		contentPane.add(lblGanaste);
		
		JLabel Nombre = new JLabel("");
		Nombre.setFont(new Font("Lucida Calligraphy", Font.BOLD, 30));
		Nombre.setBounds(177, 143, 220, 51);
		contentPane.add(Nombre);
		//BOTON QUE PERMITE REGRESAR AL INICIO
		JButton VentanaInicio = new JButton("");
		VentanaInicio.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent arg0) {
				VentanaInicio V1 = new VentanaInicio();
				V1.setVisible(true);
				V1.setAlwaysOnTop(true);
				setVisible(false);
			}
		});
		VentanaInicio.setIcon(new ImageIcon(Resultados.class.getResource("/images/resultadoSalir.jpg")));
		VentanaInicio.setBounds(312, 642, 160, 30);
		contentPane.add(VentanaInicio);
		
		

		
		
		//BOTON QUE ME MUESTRA AL GANADOR Y SU PUNTAJE
		JButton Mostrar = new JButton("");
		Mostrar.setIcon(new ImageIcon(Resultados.class.getResource("/images/botonMostrar.jpg")));
		Mostrar.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent arg0) {
				if(NombreJ.equals("Destructor")){
					Nombre.setText(NombreJ);
					lblGanaste.setText("Perdiste!!!");
					Score.setText("WINNER");
					ImageIcon imageIcon = new ImageIcon(Resultados.class.getResource("/images/pierde.gif"));
					Img.setIcon(imageIcon);
					imageIcon.setImageObserver(Img);
					
				}else{
					score=score;
					Nombre.setText(NombreJ);
					lblGanaste.setText("Ganaste!!!");
					ImageIcon imageIcon = new ImageIcon(Resultados.class.getResource("/images/Gana.gif"));
					Img.setIcon(imageIcon);
					imageIcon.setImageObserver(Img);  
					Img.setEnabled(true);
					Score.setText(String.valueOf(score));
					
				}
			}
		});
		Mostrar.setBounds(53, 157, 89, 23);
		contentPane.add(Mostrar);
		
	}
	//METODOS SETTERS AND GETTERS
	public String getNombreJ() {
		return NombreJ;
	}

	public void setNombreJ(String nombre) {
		NombreJ = nombre;
	}

	public int getScore() {
		return score;
	}

	public void setScore(int score) {
		this.score = 56;
	}
	
}
CLASE INSTRUCCIONES 
package fisica.Vista;

import java.awt.BorderLayout;
import java.awt.EventQueue;
import java.awt.Window.Type;

import javax.swing.ImageIcon;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JPanel;
import javax.swing.border.EmptyBorder;

import fisica.Logica.*;
import fisica.Vista.*;
import java.awt.Font;
import javax.swing.JTextPane;
import javax.swing.JButton;
import java.awt.event.ActionListener;
import java.awt.event.ActionEvent;

public class Instrucciones extends JFrame {
	//ATRIBUTOS
	private JPanel contentPane;

	/**
	 * Launch the application.
	 */
	
	/*
	  	public static void main(String[] args) {
	 
		EventQueue.invokeLater(new Runnable() {
			public void run() {
				try {
					Instrucciones frame = new Instrucciones();
					frame.setVisible(true);
				} catch (Exception e) {
					e.printStackTrace();
				}
			}
		});
	}
*/
	/**
	 * Create the frame.
	 */
	public Instrucciones() {
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		setType(Type.UTILITY);
		setTitle("movimiento relativo");
		setLocationRelativeTo(null);
		setResizable(false);
		setBounds(200, 0, 800, 800);
		Panel contentPane = new Panel("/images/fondoInicio.jpg");
		getContentPane().add(contentPane);
		contentPane.setLayout(null);
		//GENERA Y ORGANIZA LOS COMPONENTES EN EL FRAME
		JLabel Titulo = new JLabel("");
		Titulo.setIcon(new ImageIcon(VentanaInicio.class.getResource("/images/instrucciones.png")));
		Titulo.setBounds(155, 41, 480, 272);
		contentPane.add(Titulo);
		
		JLabel lbl2 = new JLabel("El juego consiste en tratar de predecir el amgulo y distanciias que un bote necesita para llegar a cierto lugar del otro lado de un rio, marcada con una X.Para esto se debe tener en cuneta la velocidad a la que va el agua y la fuerza que debe hacer la barca para llegar :D");
		lbl2.setFont(new Font("Lucida Calligraphy", Font.PLAIN, 20));
		lbl2.setBounds(133, 360, 534, 33);
		contentPane.add(lbl2);
		
		JLabel lbl3 = new JLabel("1. Seleccione \"Iniciar\" en la Ventana de Juego");
		lbl3.setFont(new Font("Lucida Calligraphy", Font.PLAIN, 20));
		lbl3.setBounds(133, 400, 534, 33);
		contentPane.add(lbl3);
		
		JLabel lblDisfruteEl = new JLabel("2. Escriba el angulo que usted considera correcto");
		lblDisfruteEl.setFont(new Font("Lucida Calligraphy", Font.PLAIN, 20));
		lblDisfruteEl.setBounds(133, 440, 534, 33);
		contentPane.add(lblDisfruteEl);
		
		JLabel lbl4 = new JLabel("3. Escriba las distancias que usted considera correctas");
		lbl4.setFont(new Font("Lucida Calligraphy", Font.PLAIN, 20));
		lbl4.setBounds(108, 500, 590, 33);
		contentPane.add(lbl4);
		
		JLabel lbl41 = new JLabel("4.Compare los datos que usted escribio con los correctos");
		lbl41.setFont(new Font("Lucida Calligraphy", Font.PLAIN, 20));
		lbl41.setBounds(108, 530, 590, 33);
		contentPane.add(lbl41);
		
		JLabel lbl42 = new JLabel("5.Disfrute del juego");
		lbl42.setFont(new Font("Lucida Calligraphy", Font.PLAIN, 20));
		lbl42.setBounds(108, 560, 590, 33);
		contentPane.add(lbl42);
		//CON ESTE BOTON REGRESA A LA VENTANA INICIAL
		JButton jugar = new JButton("");
		jugar.setIcon(new ImageIcon(Instrucciones.class.getResource("/images/ImgBotonIniciarV1.jpg")));
		jugar.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				Datos v2 = new Datos();
				v2.setVisible(true);
				setVisible(false);
			}
		});
		jugar.setBounds(240, 642, 300, 40);
		contentPane.add(jugar);
	}
}









