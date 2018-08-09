/**
    <one line to give the program's name and a brief idea of what it does.>
    Copyright (C) 2010  Sean Beecroft

    This program is free software: you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation, either version 3 of the License, or
    (at your option) any later version.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License
    along with this program.  If not, see <http://www.gnu.org/licenses/>.

 * @version 1.10 2010-01-01
 * @author Sean Beecroft
 */
package javaballs;

import java.awt.Color;
import java.awt.Dimension;
import java.awt.Graphics;
import java.awt.Image;
import java.awt.Toolkit;
import java.awt.event.MouseEvent;
import java.awt.event.MouseListener;
import java.awt.event.MouseMotionListener;
import java.util.Timer;
import java.util.TimerTask;
import java.util.Vector;
import javax.swing.JFrame;
import javax.swing.JPanel;


class Ball {
    private double x = 0;
    private double y = 0;
    private double vy = 0;
    private double vx = 0;
    private int width = 10;
    private double mass = 10;
    public Ball collisionBall = null;

    private Color color = Color.green;

    public String toString()
    {
        return "" + getVy();
    }

    public void hit(Ball b)
    {
        if( collisionBall == null ){
           
                double dx = x - b.x;
                double dy = y - b.y;

                double ca = Math.atan2(dy, dx);

                double speed1 = Math.sqrt(vx * vx + vy * vy);
                double speed2 = Math.sqrt(b.vx * b.vx + b.vy * b.vy);

                double direction1 = Math.atan2(vy, vx);
                double direction2 = Math.atan2(b.vy, b.vx);

                double vx_1 = speed1 * Math.cos(direction1 - ca);
                double vy_1 = speed1 * Math.sin(direction1 - ca);
                double vx_2 = speed2 * Math.cos(direction2 - ca);
                double vy_2 = speed2 * Math.sin(direction2 - ca);

                double final_vx_1 = ((mass - mass) * vx_1 + (b.mass + b.mass) * vx_2)/(mass + b.mass);
                double final_vx_2 = ((mass + mass) * vx_1 + (b.mass - mass) * vx_2)/(mass + b.mass);

                //Not change because this is an 1D environment collision.

                double final_vy_1 = ((mass - mass) * vy_1 + (b.mass + b.mass) * vy_2)/(mass + b.mass);
                double final_vy_2 = ((mass + mass) * vy_1 + (b.mass - mass) * vy_2)/(mass + b.mass);

           
                vx = Math.cos(ca) * final_vx_1 + Math.cos(ca + Math.PI/2) * final_vy_1;
                vy = Math.sin(ca) * final_vx_1 + Math.sin(ca + Math.PI/2) * final_vy_1;
                b.vx = Math.cos(ca) * final_vx_2 + Math.cos(ca + Math.PI/2) * final_vy_2;
                b.vy = Math.sin(ca) * final_vx_2 + Math.sin(ca + Math.PI/2) * final_vy_2;

            //new Player("bounce.wav").start();
            collisionBall = b;

        }
    }

    public boolean isTouchingAnything()
    {
        Vector v = Main.getBalls();
        for( int i = 0; i < v.size(); i++ ) {
            Ball m = (Ball)v.elementAt(i);
            if( this != m ){
                if( this.collide(m)){
                    return true;
                }
            }
        }
        collisionBall = null;
        return false;
    }



    boolean collide(Ball b2) {

        if( this == b2 ){
            return false;
        }
        // already collided.

        double wx = (x + (width / 2)) - (b2.x + (b2.width / 2));
        double wy = (y + (width / 2)) - (b2.y + (b2.width / 2));

        //we calculate the distance between the centers two
        //colliding balls (theorem of Pythagoras)
        double distance = Math.sqrt(wx * wx + wy * wy);

        if (distance < width) {
            return true;
        }
        return false;
    }

    public double getX() {
        return x;
    }

    public void setX(double x) {
        this.x = x;
    }

    public double getY() {
        return y;
    }

    public void setY(double y) {
        this.y = y;
    }

    public double getVy() {
        return vy;
    }

    public void setVy(double vy) {
        this.vy = vy;
    }

    public double getVx() {
        return vx;
    }

    public void setVx(double vx) {
        this.vx = vx;
    }

    public int getWidth() {
        return width;
    }

    public void setWidth(int width) {
        this.width = width;
    }

    public Color getColor() {
        return color;
    }

    public void setColor(Color color) {
        this.color = color;
    }

    public double getMass() {
        return mass;
    }

    public void setMass(double mass) {
        this.mass = mass;
    }
}

class G extends JPanel implements MouseMotionListener, MouseListener {
    Image buffer = null;
    Image clear = null;

    public G ()
    {
    }

    public void paint(Graphics g)
    {
        if( buffer == null || clear == null ) {
           buffer = this.createImage(Main.WIDTH, Main.HEIGHT);
           clear = this.createImage(Main.WIDTH, Main.HEIGHT);
           clear.getGraphics().fillRect(0,0,Main.WIDTH, Main.HEIGHT);
        }
        Graphics bg = buffer.getGraphics();
        bg.drawImage(clear, 0, 0, this);
        Vector balls = Main.getBalls();
        for( int i = 0; i < balls.size(); i++ ){
            Ball b = (Ball)balls.elementAt(i);
            bg.setColor(b.getColor());
            if( b != null ){
                bg.fillOval((int)b.getX(), (int)b.getY(),b.getWidth(), b.getWidth());
            }
        }

        g.drawImage(buffer, 0, 0, this);
        g.dispose();

    }

    public void mouseDragged(MouseEvent e) {
    }

    public void mouseMoved(MouseEvent e) {
    }

    public void mouseClicked(MouseEvent e) {
    }

    public void mousePressed(MouseEvent e) {
    }

    public void mouseReleased(MouseEvent e) {
        int x = e.getX();
        int y = e.getY();
        Ball ball = new Ball();
        ball.setX((double) x);
        ball.setY((double) y);
        ball.setVx(20);
        ball.setVy(10);
        double v =  (Math.random() * 50) + 10;
        ball.setWidth((int)v);
        ball.setMass((int)v);

        ball.setColor(Utility.getRandomColor());
        Main.getBalls().add(ball);
    }

    public void mouseEntered(MouseEvent e) {
    }

    public void mouseExited(MouseEvent e) {
    }
}

class CollisionDetector extends Thread {
    int n = 0;
    public void run()
    {
        while( true ){
            Vector balls = Main.getBalls();
            for( int i = 0; i < balls.size(); i++ ){
                Ball b = (Ball)balls.elementAt(i);
                for( int j = 0; j < balls.size(); j++ ){
                    Ball m = (Ball)balls.elementAt(j);
                    if( b != m ){
                        if(b.collide(m)){
                            b.hit(m);
                        }
                    }
                }
                b.isTouchingAnything();
            }
            Thread.yield();
        }
    }

}
class Engine extends TimerTask {

    boolean bb = false;
    double pos = 0;
    double m = 1.12;
    double g = 0.2;
    int n = 0;
    double f = 1.2; // friction

    private double f( double v)
    {
        v = v + g;
        return v;
    }

    public void run()
    {
        Vector balls = Main.getBalls();

        for(int i = 0; i < balls.size(); i++ ){
                Ball b = (Ball)balls.elementAt(i);
                // add gravity
                b.setVy(f(b.getVy()));
                b.setY(b.getY() + b.getVy());

                if( b.getY() + b.getWidth() >= (Main.HEIGHT-100) ){
                    b.setVy(-(Math.abs(b.getVy()) - (b.getVy() / m))) ;
                    b.setY(b.getY() - 1);
                }

                b.setX((int) (double) b.getX() + b.getVx());
                if( b.getX() + b.getWidth() > Main.WIDTH ){
                    b.setVx(-b.getVx()/f); // friction

                } else if( b.getX() < 0 ){
                    b.setVx(-b.getVx());
                }
        }
    }
}

class Utility {

    public static Color getRandomColor()
    {
        int d = (int)(Math.random() * 7);
        if( d == 0 ){
            return Color.blue;
        }
        else if( d == 1 ){
            return Color.orange;
        }
        else if( d == 2 ){
            return Color.yellow;
        }
        else if( d == 3 ){
            return Color.pink;
        }
        else if( d == 4 ){
            return Color.magenta;
        }
        else if( d == 5 ){
            return Color.green;
        }
        else if( d == 6 ){
            return Color.white;
        }
        else if( d == 7 ){
            return Color.red;
        }
        return null;
    }
}

/**
 *
 * @author beecrofs
 */
public class Main {

    public static int WIDTH = 324;
    public static int HEIGHT = 268;

    static Vector vec = new Vector();
    public static Vector getBalls()
    {
        return vec;
    }
    public static void setBalls(Vector v)
    {
        vec = v;
    }

    /**
     * @param args the command line arguments
     */
    public static void main(String[] args) {
        // TODO code application logic here
        JFrame frame = new JFrame();
        Dimension d = Toolkit.getDefaultToolkit().getScreenSize();
        Main.WIDTH = 700;
        Main.HEIGHT = 700;
        frame.setSize(new Dimension(Main.WIDTH,Main.HEIGHT));
        final G g = new G();
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.getContentPane().add(g);
        g.addMouseListener(g);
        frame.setVisible(true);
        Vector balls = new Vector();

        TimerTask task = new TimerTask(){
            @Override
            public void run() {
                g.repaint();
            }
        };

        Timer t = new Timer();
        Engine task2 = new Engine();
        CollisionDetector task3 = new CollisionDetector();
        t.scheduleAtFixedRate(task, 0, 5);
        t.scheduleAtFixedRate(task2, 0, 15);
        task3.start();

        for( int i = 0; i < 1; i++ ){
            Ball b3  = new Ball();
            b3.setX(Math.random() * 10 + 20);
            b3.setY(Math.random() * 100 + 20);
            b3.setVx(Math.random() * 3);
            b3.setVy(1); 
            double v = 5;
            b3.setWidth((int)v);
            b3.setMass(v);
            b3.setColor(Utility.getRandomColor()); 
            vec.add(b3);
            try { Thread.sleep(500); } catch(Exception ex){}
        }


    }



}