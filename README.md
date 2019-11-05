# GUI-Construction-Sample-of-Revision-App
University Year 1 Project (Coursework), Using Java:  

package coursework;

import java.awt.BorderLayout;
import java.awt.Color;
import java.awt.Dimension;
import java.awt.Font;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.KeyEvent;
import java.awt.event.KeyListener;
import java.io.File;
import java.util.ArrayList;
import javax.swing.BorderFactory;
import javax.swing.Box;
import javax.swing.BoxLayout;
import javax.swing.Icon;
import javax.swing.ImageIcon;
import javax.swing.JButton;
import javax.swing.JComboBox;
import javax.swing.JFrame;
import javax.swing.JMenu;
import javax.swing.JMenuBar;
import javax.swing.JMenuItem;
import javax.swing.JPanel;
import javax.swing.JTextArea;
import javax.swing.JTextField;
import javax.swing.JToolBar;

public class Coursework extends JFrame implements ActionListener, KeyListener {
    CommonCode cc = new CommonCode();
    JPanel pnl = new JPanel(new BorderLayout());
    JTextArea txtNewNote = new JTextArea();
    JTextArea txtDisplayNotes = new JTextArea();
    JTextField search = new JTextField();
    ArrayList<String> note = new ArrayList<>();
    ArrayList<String> course = new ArrayList<>();
    JComboBox courseList = new JComboBox();
    String crse = "";
    AllNotes allNotes = new AllNotes();
  
   public static void main(String[] args) {
      Coursework prg = new Coursework();
    }

   // Using MVC
   public Coursework() {
       model();
       view();
       controller();
   }

   @Override
   public void actionPerformed(ActionEvent ae) {
       if ("Coursework".equals(ae.getActionCommand())) {
           CWDetails cw = new CWDetails();
       }
       if ("Course".equals(ae.getActionCommand())) {
           crse = courseList.getSelectedItem().toString();
           System.out.println(crse);
       }
       if ("Exit".equals(ae.getActionCommand())) {
           System.exit(0);
       }
       if ("NewNote".equals(ae.getActionCommand())) {
           addNote(txtNewNote.getText());
           txtNewNote.setText("");
       }
       if ("SearchKeyword".equals(ae.getActionCommand())) {
           String lyst = allNotes.searchAllNotesByKeyword("", 0, search.getText());
           txtDisplayNotes.setText(lyst);
       }
   }

   @Override
   public void keyTyped(KeyEvent ke) {
      System.out.println("keyTyped has not been coded yet.");
   }

   @Override
   public void keyPressed(KeyEvent ke) {
       System.out.println("keyPressed has not been coded yet.");
   }

   @Override
   public void keyReleased(KeyEvent ke) {
       System.out.println("keyReleased has not been coded yet.");
   }

   private void model() {
        course.add("COMP1713 - Database System Development");
        course.add("COMP1715 - Scholarly And Academic Practice");
        course.add("COMP1752 - Object Orientated Programming");
        course.add("COMP1753 - Programming Foundations");
        course.add("COMP1765 - Computer Communication Systems");
        course.add("COMP1771 - Smart Systems");
        course.add("MATH1110 - Logical Foundations");
        course.add("MATH1111 - Analytic, Numeric And Statistical Methods");
        crse = course.get(0);
    }

   private void view() {
       Font fnt = new Font("Times New Roman", Font.PLAIN, 26);

   JMenuBar menuBar = new JMenuBar();
   JMenu kurs = new JMenu();
   kurs = new JMenu("Course");
   kurs.setToolTipText("Course tasks");
   kurs.setFont(fnt);
   kurs.add(makeMenuItem("Add", "AddCourse", "Add a new course.", fnt));
   kurs.add(makeMenuItem("Amend", "AmendCourse", "Amend an existing course.", fnt));
   kurs.add(makeMenuItem("Delete", "DeleteCourse", "Delete an existing course.", fnt));
   kurs.addSeparator();
   kurs.add(makeMenuItem("Coursework Screen", "Coursework", "Go to the coursework screen.", fnt));
   menuBar.add(kurs);

   JMenu note = new JMenu();
   note = new JMenu("Note");
   note.setToolTipText("Note tasks");
   note.setFont(fnt);
   note.add(makeMenuItem("New", "NewNote", "Create a new note.", fnt));
   note.addSeparator();
   note.add(cc.makeMenuItem("Close", "Close", "Clear the current note.", fnt));
   menuBar.add(note);
   menuBar.add(makeMenuItem("Exit", "Exit", "Close this program", fnt));

  
   // This will add each course to the combobox
        for (String crse : course) {
            courseList.addItem(crse);
        }
        courseList.setFont(fnt);
        courseList.setMaximumSize(courseList.getPreferredSize());
        courseList.addActionListener(this);
        courseList.setActionCommand("Course");
        menuBar.add(courseList);
        this.setJMenuBar(menuBar);
        JToolBar toolBar = new JToolBar();
        
   // Setting up the ButtonBar
        JButton button = null;
        button = makeButton("Document", "Coursework",
                "Open the coursework window.",
                "Coursework");
        toolBar.add(button);
        button = makeButton("Create", "NewNote",
                "Create a new note.",
                "New");
        toolBar.add(button);
        button = makeButton("closed door", "Close",
                "Close this note.",
                "Close");
        toolBar.add(button);
        toolBar.addSeparator();
        button = makeButton("exit", "Exit",
                "Exit from this program.",
                "Exit");
        toolBar.add(button);
        toolBar.addSeparator();
        
   // This forces anything after it to the right.
        toolBar.add(Box.createHorizontalGlue());
        search.setMaximumSize(new Dimension(6900, 50));
        search.setFont(fnt);
        toolBar.add(search);
        toolBar.addSeparator();
        button = makeButton("search", "SearchKeyword",
                "Search for this text.",
                "Search");
        toolBar.add(button);
        add(toolBar, BorderLayout.NORTH);
        JPanel pnlWest = new JPanel();
        pnlWest.setLayout(new BoxLayout(pnlWest, BoxLayout.Y_AXIS));
        pnlWest.setBorder(BorderFactory.createLineBorder(Color.black));
        txtNewNote.setFont(fnt);
        pnlWest.add(txtNewNote);
        JButton btnAddNote = new JButton("Add note");
        btnAddNote.setActionCommand("NewNote");
        btnAddNote.addActionListener(this);
        pnlWest.add(btnAddNote);
        add(pnlWest, BorderLayout.WEST);
        JPanel cen = new JPanel();
        cen.setLayout(new BoxLayout(cen, BoxLayout.Y_AXIS));
        cen.setBorder(BorderFactory.createLineBorder(Color.black));
        txtDisplayNotes.setFont(fnt);
        cen.add(txtDisplayNotes);
        add(cen, BorderLayout.CENTER);
        setExtendedState(JFrame.MAXIMIZED_BOTH);
        setTitle("Coursework - Safa Butt");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setVisible(true);  // Needed to ensure that the items can be seen.
    }

   private void controller() {
        addAllNotes();
   }

   private void addNote(String text) {
        allNotes.addNote(allNotes.getMaxID(), crse, text);
        addAllNotes();
   }

   private void addAllNotes() {
       String txtNotes = "";

   for (Note n : allNotes.getAllNotes()) {
            txtNotes += n.getNote() + "\n";
   }

   txtDisplayNotes.setText(txtNotes);
    
   }

   protected JMenuItem makeMenuItem(String txt,
           String actionCommand,
           String toolTipText,
           Font fnt) {
        JMenuItem mnuItem = new JMenuItem();
        mnuItem.setText(txt);
        mnuItem.setActionCommand(actionCommand);
        mnuItem.setToolTipText(toolTipText);
        mnuItem.setFont(fnt);
        mnuItem.addActionListener(this);
        return mnuItem;
    }

   protected JButton makeButton(String imageName,
            String actionCommand,
            String toolTipText,
            String altText) {

   //Look for the image.
        String imgLocation = System.getProperty("user.dir") + "\\icons\\"
                + imageName
                + ".png";

   //Create and initialize the button.
        JButton button = new JButton();
        button.setToolTipText(toolTipText);
        button.setActionCommand(actionCommand);
        button.addActionListener(this);
        File fyle = new File(imgLocation);
        if (fyle.exists() && !fyle.isDirectory()) {
            // image found
            Icon img;
            img = new ImageIcon(imgLocation);
            button.setIcon(img);
        } else {
            // image NOT found
            button.setText(altText);
            System.err.println("Resource not found: " + imgLocation);
        }
        return button;
    }
}
