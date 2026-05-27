import java.util.*;

class Student {
    int id;
    String name;
    double marks;

    Student(int id, String name, double marks) {
        this.id = id;
        this.name = name;
        this.marks = marks;
    }

    void display() {
        System.out.println("================================");
        System.out.println("Student ID    : " + id);
        System.out.println("Student Name  : " + name);
        System.out.println("Student Marks : " + marks);
        System.out.println("================================");
    }
}

public class Main {

    static ArrayList<Student> students = new ArrayList<>();
    static Scanner sc = new Scanner(System.in);

    // Colors
    public static final String RESET = "\u001B[0m";
    public static final String GREEN = "\u001B[32m";
    public static final String RED = "\u001B[31m";
    public static final String CYAN = "\u001B[36m";
    public static final String YELLOW = "\u001B[33m";

    public static void main(String[] args) {

        showWelcome();

        while (true) {

            System.out.println(CYAN);
            System.out.println("\n=====================================");
            System.out.println("   SMART STUDENT MANAGEMENT SYSTEM");
            System.out.println("=====================================");
            System.out.println(RESET);

            System.out.println(YELLOW + "1. Add Student");
            System.out.println("2. View All Students");
            System.out.println("3. Search Student");
            System.out.println("4. Delete Student");
            System.out.println("5. Sort Students by Name");
            System.out.println("6. Update Student Marks");
            System.out.println("7. Show Topper");
            System.out.println("8. Exit" + RESET);

            System.out.print("\nEnter Your Choice: ");

            int choice = sc.nextInt();

            switch (choice) {

                case 1:
                    addStudent();
                    break;

                case 2:
                    viewStudents();
                    break;

                case 3:
                    searchStudent();
                    break;

                case 4:
                    deleteStudent();
                    break;

                case 5:
                    sortStudents();
                    break;

                case 6:
                    updateMarks();
                    break;

                case 7:
                    showTopper();
                    break;

                case 8:
                    System.out.println(GREEN + "\nThank You For Using The System!" + RESET);
                    System.exit(0);

                default:
                    System.out.println(RED + "Invalid Choice!" + RESET);
            }
        }
    }

    // Welcome Screen
    static void showWelcome() {

        System.out.println(GREEN);
        System.out.println("****************************************");
        System.out.println("*                                      *");
        System.out.println("*     WELCOME TO JAVA DSA PROJECT      *");
        System.out.println("*                                      *");
        System.out.println("****************************************");
        System.out.println(RESET);
    }

    // Add Student
    static void addStudent() {

        System.out.print("Enter Student ID: ");
        int id = sc.nextInt();
        sc.nextLine();

        System.out.print("Enter Student Name: ");
        String name = sc.nextLine();

        System.out.print("Enter Student Marks: ");
        double marks = sc.nextDouble();

        students.add(new Student(id, name, marks));

        System.out.println(GREEN + "\nStudent Added Successfully!" + RESET);
    }

    // View Students
    static void viewStudents() {

        if (students.isEmpty()) {
            System.out.println(RED + "\nNo Students Found!" + RESET);
            return;
        }

        System.out.println(CYAN + "\n----- STUDENT LIST -----" + RESET);

        for (Student s : students) {
            s.display();
        }
    }

    // Search Student
    static void searchStudent() {

        System.out.print("Enter Student ID to Search: ");
        int id = sc.nextInt();

        for (Student s : students) {

            if (s.id == id) {

                System.out.println(GREEN + "\nStudent Found!" + RESET);
                s.display();
                return;
            }
        }

        System.out.println(RED + "\nStudent Not Found!" + RESET);
    }

    // Delete Student
    static void deleteStudent() {

        System.out.print("Enter Student ID to Delete: ");
        int id = sc.nextInt();

        Iterator<Student> iterator = students.iterator();

        while (iterator.hasNext()) {

            Student s = iterator.next();

            if (s.id == id) {

                iterator.remove();

                System.out.println(GREEN + "\nStudent Deleted Successfully!" + RESET);
                return;
            }
        }

        System.out.println(RED + "\nStudent Not Found!" + RESET);
    }

    // Sort Students
    static void sortStudents() {

        students.sort(Comparator.comparing(s -> s.name.toLowerCase()));

        System.out.println(GREEN + "\nStudents Sorted By Name!" + RESET);
    }

    // Update Marks
    static void updateMarks() {

        System.out.print("Enter Student ID: ");
        int id = sc.nextInt();

        for (Student s : students) {

            if (s.id == id) {

                System.out.print("Enter New Marks: ");
                s.marks = sc.nextDouble();

                System.out.println(GREEN + "\nMarks Updated Successfully!" + RESET);
                return;
            }
        }

        System.out.println(RED + "\nStudent Not Found!" + RESET);
    }

    // Show Topper
    static void showTopper() {

        if (students.isEmpty()) {

            System.out.println(RED + "\nNo Students Available!" + RESET);
            return;
        }

        Student topper = students.get(0);

        for (Student s : students) {

            if (s.marks > topper.marks) {
                topper = s;
            }
        }

        System.out.println(GREEN + "\n----- TOPPER DETAILS -----" + RESET);
        topper.display();
    }
}
