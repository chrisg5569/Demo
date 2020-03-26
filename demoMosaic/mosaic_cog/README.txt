In this README file I will be providing you directions on compiling and running as well as source code.

In order to compile you can either use javac *.java or javac Mosaic.java

to run it you will need to do java Mosaic


and the source code will be provided down below:

//java imports
import javax.swing.JFrame;
import javax.swing.JPanel;
import javax.swing.JButton;
import java.awt.Container; 
import java.awt.GridLayout;
import java.awt.BorderLayout;
import java.awt.event.ActionListener;
import java.awt.event.ActionEvent;
import java.util.Random;
import java.awt.Graphics;
import java.awt.Color;
import java.awt.Font;
import java.util.ArrayList;



//JPanel
class LetterTiles extends JPanel {
    //creating ints
    private int red, green, blue;
    private String letter;
    private int choice;
    //calling super class
    LetterTiles() {
        super();
        SetRandomValues();
    }
//getting random possibilities 
    final public void SetRandomValues() {
        //colors
        red = GetNumberBetween(0,255);
        green = GetNumberBetween(0,255);
        blue = GetNumberBetween(0,255);

        //getting the letters per tile
        letter = "A";
        if (GetNumberBetween(0,30) == 1) {
            letter = "B";
        }
        if (GetNumberBetween(0,30) == 2) {
            letter = "C";
        }
        if (GetNumberBetween(0,30) == 3) {
            letter = "D";
        }
        if (GetNumberBetween(0,30) == 4) {
            letter = "E";
        }
        if (GetNumberBetween(0,30) == 5) {
            letter = "F";
        }
        if (GetNumberBetween(0,30) == 6) {
            letter = "G";
        }
        if (GetNumberBetween(0,30) == 7) {
            letter = "H";
        }
        if (GetNumberBetween(0,30) == 8) {
            letter = "I";
        }
        if (GetNumberBetween(0,30) == 9) {
            letter = "J";
        }
        if (GetNumberBetween(0,30) == 10) {
            letter = "K";
        }
        if (GetNumberBetween(0,30) == 11) {
            letter = "L";
        }
        if (GetNumberBetween(0,30) == 12) {
            letter = "M";
        }
        if (GetNumberBetween(0,30) == 13) {
            letter = "N";
        }
        if (GetNumberBetween(0,30) == 14) {
            letter = "O";
        }
        if (GetNumberBetween(0,30) == 15) {
            letter = "P";
        }
        if (GetNumberBetween(0,30) == 16) {
            letter = "Q";
        }
        if (GetNumberBetween(0,30) == 17) {
            letter = "R";
        }
        if (GetNumberBetween(0,30) == 18) {
            letter = "S";
        }
        if (GetNumberBetween(0,30) == 19) {
            letter = "T";
        }
        if (GetNumberBetween(0,30) == 20) {
            letter = "U";
        }
        if (GetNumberBetween(0,30) == 21) {
            letter = "V";
        }
        if (GetNumberBetween(0,30) == 22) {
            letter = "W";
        }
        if (GetNumberBetween(0,30) == 23) {
            letter = "X";
        }
        if (GetNumberBetween(0,30) == 24) {
            letter = "Y";
        }
        if (GetNumberBetween(0,30) == 25) {
            letter = "Z";
        }   
        //implementation 
        if (GetNumberBetween(0,30) == 26) {
            letter = ":)";
        }  
        if (GetNumberBetween(0,30) == 27) {
            letter = ":(";
        } 
        if (GetNumberBetween(0,30) == 28) {
            letter = ":|";
        }
        if (GetNumberBetween(0,30) == 29) {
            letter = "<3";
        }
        if (GetNumberBetween(0,30) == 30) {
            letter = "Hi";
        }     
    }
//creating method for getnumberbetween
    private static int GetNumberBetween(int min, int max) {
        Random myRandom = new Random();
        return min + myRandom.nextInt(max-min+1);
    }   
//graphics
     public void paintComponent(Graphics g) {
        super.paintComponent(g); 

        int panelWidth = getWidth();
        int panelHeight = getHeight();
//making it choose either a square or an oval
        choice = 0;
        if (GetNumberBetween(0,1) == 1) {
        g.setColor(new Color(red,green,blue));
        g.fillRect (10, 10, panelWidth-20, panelHeight-20);
        }
       else {
        g.setColor(new Color(red,green,blue));
        g.fillOval(10, 10,panelWidth-20, panelHeight-20);   
       }

        g.setColor(new Color(GetContrastingColor(red),GetContrastingColor(green),GetContrastingColor(blue)));
//selecting font and positioning the letter
        final int fontSize=40;
        g.setFont(new Font("TimesRoman", Font.PLAIN, fontSize));
        int stringX = (panelWidth/2)-15;
        int stringY = (panelHeight/2)+15;
        g.drawString(letter,stringX,stringY);
        System.out.format("\nLetter=%s, LetterX=%d, LetterY=%d,Shape=%d 0 is rectangle 1 is oval, Tile Height=%d, Tile Width=%d", letter, stringX, stringY, choice, getHeight(), getWidth());  
    }
//color contrast 
    private static int GetContrastingColor(int colorIn) {
        return ((colorIn+128)%256);
    }
}
//JFrame
class MosaicFrame extends JFrame implements ActionListener {
    private ArrayList<LetterTiles> tileList;

    public MosaicFrame() {
        setBounds(200,200,1200,800);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        Container contentPane = getContentPane();
        contentPane.setLayout(new BorderLayout());

        JPanel buttonPanel = new JPanel();
        contentPane.add(buttonPanel, BorderLayout.SOUTH);

        JButton randomize = new JButton("Randomize");
        buttonPanel.add(randomize);
        randomize.addActionListener(this);

        JPanel LetterGridPanel = new JPanel();
        contentPane.add(LetterGridPanel, BorderLayout.CENTER);
        //making it 12 by 12
        LetterGridPanel.setLayout(new GridLayout(12,12));

        tileList = new ArrayList<LetterTiles>();
        //making it do the random sequence enough for 12 by 12
        for(int i=1; i<145; i++) {
            LetterTiles tile = new LetterTiles();
            tileList.add(tile);
            LetterGridPanel.add(tile);
        }
    }
//Action Events
    public void actionPerformed(ActionEvent e) {
        for(LetterTiles tile : tileList) {
            tile.SetRandomValues();
        }
        repaint();
    }
}

public class Mosaic {
    public static void main(String[] args) {
        System.out.println("Mosaic Starting...");

        MosaicFrame myMosaicFrame = new MosaicFrame();
        myMosaicFrame.setVisible(true);
    }