# Proyecto-f-sica-
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
