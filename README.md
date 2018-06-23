import java.awt.*;

import java.awt.event.*;

import java.awt.geom.GeneralPath;

import java.awt.print.PageFormat;

import javax.swing.*;

import java.awt.print.Printable;

import java.awt.print.PrinterException;

import java.awt.print.PrinterJob;

import java.awt.Color;

public class Paint extends JPanel {
    /*Sets up the drawing area and row of buttons below it.*/

    public Paint() {  

        setBackground(Color.LIGHT_GRAY);

        JButton printButton = new JButton("Print"); // button for printing diagram
        
        JButton clearButton = new JButton("Clear All"); // button for clearing shapes
        
        JButton undoButton = new JButton("Undo Shape"); // button for undoing shapes
        
        JButton redoButton = new JButton("Redo Shape"); // button for redoing shapes
        
        JButton colorButtonBG = new JButton("Background Color"); //button to choose background color
        
        JButton colorButtonG = new JButton("Grid Color"); //button to choose grid color
        
        JButton colorButtonS = new JButton("Shape Color"); //button to choose shape color
        
        JButton colorButtonB = new JButton("Border Color"); //button to choose border color
        
        /*Listeners for buttons*/
        colorButtonBG.addActionListener(new ActionListener() {
         @Override
         public void actionPerformed(ActionEvent evt) {
            Color color = JColorChooser.showDialog(Paint.this,"Choose a background color", backgroundColor);
            if (color != null) { // new color selected
               backgroundColor = color;
            }
            canvas.repaint();
          }
        });
        
        colorButtonG.addActionListener(new ActionListener() {
         @Override
         public void actionPerformed(ActionEvent evt) {
            Color color = JColorChooser.showDialog(Paint.this,"Choose a gridline color", gridlineColor);
            if (color != null) { // new color selected
               gridlineColor = color;
            }
            canvas.repaint();
          }
        });
        
        colorButtonS.addActionListener(new ActionListener() {
         @Override
         public void actionPerformed(ActionEvent evt) {
            Color color = JColorChooser.showDialog(Paint.this,"Choose a shape color", shapeColor);
            if (color != null) { // new color selected
               shapeColor = color;
            }
          }
        });

        colorButtonB.addActionListener(new ActionListener() {
        @Override
        public void actionPerformed(ActionEvent evt) {
            Color color = JColorChooser.showDialog(Paint.this,"Choose a border color", borderColor);
            if (color != null) { // new color selected
               borderColor = color;
            }
           }
        });
        
        canvas.addMouseListener(new PopClickListener());
        
        printButton.addActionListener(new ActionListener() {
        @Override
        public void actionPerformed(ActionEvent e) {
            PrinterJob printJob = PrinterJob.getPrinterJob();
            printJob.setPrintable(canvas);
            if (printJob.printDialog()) {
                try {
                    printJob.print();
                } catch (PrinterException p) {
                    System.out.println("Error printing: " + p);
                }
            }
           }
        });
        
        clearButton.addActionListener(canvas);
        
        undoButton.addActionListener(canvas);
        
        redoButton.addActionListener(canvas);

        JPanel bottom = new JPanel();   // panel that holds buttons

        MyPanel top = new MyPanel();    // panel that shows the shapes

        top.setLayout(new GridLayout(1,4,3,3));

        bottom.setLayout(new GridLayout(1,4,3,3));
        
        bottom.add(colorButtonS);
        
        bottom.add(colorButtonB);
        
        bottom.add(colorButtonBG);
        
        bottom.add(colorButtonG);
        
        bottom.add(undoButton);
        
        bottom.add(redoButton);
        
        bottom.add(clearButton);
        
        bottom.add(printButton);
      
        top.add(new MyPanel ());

        setLayout(new BorderLayout(3,3));

        add(top,BorderLayout.NORTH); //add top panel

        add(canvas, BorderLayout.CENTER); //add canvas panel

        add(bottom, BorderLayout.SOUTH); //add button panel   
    } //end of constructor

Board canvas = new Board();  // creating the canvas

public Point startPoint, endPoint;
    int x1,y1,x2,y2;
    Shape[] shapes = new Shape[500]; // array that holds up to 500 shapes
    Line[] lines = new Line[500];
    
    int shapeCount = 0;  // the actual number of shapes in the array
    int lineCount = 0; // the actual number of lines in the array

    Color shapeColor = Color.black;  // default shape color
     
    Color borderColor = Color.black; // default border color
    
    Color backgroundColor = Color.WHITE; // default background color
     
    Color gridlineColor = Color.WHITE; // default gridline color
}
