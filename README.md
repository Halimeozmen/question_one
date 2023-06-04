# question_one

import java.awt.Color;
import java.awt.Font;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.ArrayList;
import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JPanel;
import javax.swing.JScrollPane;
import javax.swing.JTextArea;
import javax.swing.JTextField;



public class Employee implements ActionListener {

public static String div = "------------------------------------------";
public static ArrayList<Integer> ids, salary;
public static ArrayList<String> Name, position, Experience,Educational ;
public static JTextArea display;
public static JButton[] buttons = new JButton[3];
public static JLabel[] subTitles = new JLabel[6];
public static JTextField[] inputs = new JTextField[6];

public static void main(String[] args) {
    // Defining all array lists
    ids = new ArrayList();
    salary = new ArrayList();
    Experience = new ArrayList();
     Name = new ArrayList();
    position = new ArrayList();
    Educational = new ArrayList();

    // Fonts
    Font titleFont = new Font("Courier New", 1, 24);
    Font subFont = new Font("Courier New", 1, 16);

    // Frame
    JFrame frame = new JFrame("Employee Records");
    frame.setSize(550, 450);
    frame.setLocationRelativeTo(null);
    frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    frame.setResizable(false);

    // Container
    JPanel container = new JPanel();
    container.setLayout(null);
    frame.setContentPane(container);

    // Title
    JLabel title = new JLabel("Employee Records");
    title.setFont(titleFont);
    title.setForeground(Color.blue);
    title.setBounds(160, 10, 250, 24);

    // Lablels and text fields
    for (int i = 0; i < subTitles.length; i++) {
        subTitles[i] = new JLabel();
        subTitles[i].setFont(subFont);
        subTitles[i].setBounds(5, 50 + (i * 35), 190, 16);
    }
    subTitles[0].setText("Employee ID#: ");
    subTitles[1].setText("Name: ");
    subTitles[2].setText("position: ");
    subTitles[3].setText("Annual Salary: ");
    subTitles[4].setText("Experience: ");
    subTitles[5].setText("Educational: ");
   

    for (int i = 0; i < subTitles.length; i++) {
        inputs[i] = new JTextField();
        inputs[i].setBounds(160, 47 + (35 * i), 150, 22);
    }

    // Buttons
    for (int i = 0; i < buttons.length; i++) {
        buttons[i] = new JButton();
        buttons[i].addActionListener(new Employee());
        buttons[i].setBounds(330, 47 + (35 * i), 200, 20);
    }
    buttons[0].setText("Add (REQUIRES ALL FIELDS)");
    buttons[1].setText("Remove (by ID#)");
    buttons[2].setText("List");

    
    // Text area
    display = new JTextArea();
    display.setEditable(false);
    JScrollPane scrollPane = new JScrollPane(display);
    scrollPane.setBounds(5, 250, 535, 200);

    // Adding everything
    container.add(title);
    container.add(scrollPane);
    // Since # of textfields will always equal # of subtitles, we can use the
    // max value of subtitles for the loop
    for (int i = 0; i < subTitles.length; i++) {
        container.add(subTitles[i]);
        container.add(inputs[i]);
    }
    for (int i = 0; i < buttons.length; i++) {
        container.add(buttons[i]);
    }

    // Extras
    frame.toFront();
    frame.setVisible(true);
    
    
}

public void actionPerformed(ActionEvent event) {
    if (event.getSource().equals(buttons[0])) {
        // Pass boolean to check if the program should continue or not
        boolean pass = true;
        // Loop to check if all textfields have data
        for (int i = 0; i < inputs.length; i++) {
            if (inputs[i].getText().equals("")) {
                display.setText("Error: enter data for ALL fields.");
                pass = false;
            }
        }

        // If the user passed, the program continues
        if (pass == true) {
            // Checking if ID# already exists
            if (ids.contains(Integer.parseInt(inputs[0].getText()))) {
                // Displaying error message if entered ID# exists
                display.setText("Error: employee ID# exists, use another.");
                // If not, it adds all the data
            } else {
                // Adding all the info to the arrays
                ids.add(Integer.parseInt(inputs[0].getText()));
                Name.add(inputs[1].getText());
                position.add(inputs[2].getText());
                salary.add(Integer.parseInt(inputs[3].getText()));
                Experience.add(inputs[4].getText());
                Educational.add(inputs[5].getText());
                display.setText("Employee #" + inputs[0].getText() + " added to record(s).");
                // Loop to set all textfields to empty
                for (int i = 0; i < inputs.length; i++) {
                    inputs[i].setText(null);
                }
            }
        }
    } else if (event.getSource().equals(buttons[1])) {
        // Loop to search list for requested removal
        for (int i = ids.size() - 1; i >= 0; i--) {
            // If the request is found, it removes all data
            if (Integer.parseInt(inputs[0].getText()) == ids.get(i)) {
                display.setText("Employee #" + ids.get(i) + " has been removed from the records.");
                ids.remove(i);
                 Name.remove(i);
                position.remove(i);
                salary.remove(i);
                Experience.remove(i);
                Educational.remove(i);
                break;
                // If not, the ID# does not exist
            } else {
                display.setText("Error: employee ID# does not exist, try again.");
            }
        }
    } else {
        // Resets text area and lists all the data
        display.setText(null);
        for (int i = 0; i < ids.size(); i++) {
            display.append(div + "\nEmployee ID#: " + ids.get(i) + "\n Name: " +  Name.get(i)
                    + "\nLast Name: " + position.get(i) + "\nAnnual Salary: $" + salary.get(i)
                    + "\nExperience: " + Experience.get(i) + "\n"+"\nEducational: " + Educational.get(i) + "\n");
        }
    }
}
}
