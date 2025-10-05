# PBLJ-Exp-2.3
import java.util.*;
import java.util.stream.*;

class Employee {
    int id;
    String name;
    double salary;

    Employee(int id, String name, double salary) {
        this.id = id;
        this.name = name;
        this.salary = salary;
    }

    public String toString() {
        return id + " - " + name + " - " + salary;
    }
}

class Student {
    String name;
    int marks;

    Student(String name, int marks) {
        this.name = name;
        this.marks = marks;
    }

    public String toString() {
        return name + " - " + marks;
    }
}

class Product {
    int id;
    String name;
    double price;

    Product(int id, String name, double price) {
        this.id = id;
        this.name = name;
        this.price = price;
    }

    public String toString() {
        return id + " - " + name + " - " + price;
    }
}

public class LambdaAndStreamDemo {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int choice;

        do {
            System.out.println("\n===== MENU =====");
            System.out.println("1. Sort Employees using Lambda");
            System.out.println("2. Filter and Sort Students using Streams");
            System.out.println("3. Stream Operations on Product Dataset");
            System.out.println("4. Exit");
            System.out.print("Enter your choice: ");
            choice = sc.nextInt();

            switch (choice) {
                case 1:
                    sortEmployees();
                    break;

                case 2:
                    processStudents();
                    break;

                case 3:
                    processProducts();
                    break;

                case 4:
                    System.out.println("Exiting program...");
                    break;

                default:
                    System.out.println("Invalid choice! Try again.");
            }
        } while (choice != 4);

        sc.close();
    }

    // Part (a)
    public static void sortEmployees() {
        List<Employee> employees = new ArrayList<>();
        employees.add(new Employee(101, "Alice", 55000));
        employees.add(new Employee(102, "Bob", 45000));
        employees.add(new Employee(103, "Charlie", 70000));

        employees.sort((e1, e2) -> Double.compare(e1.salary, e2.salary));

        System.out.println("\nEmployees sorted by salary:");
        employees.forEach(System.out::println);
    }

    // Part (b)
    public static void processStudents() {
        List<Student> students = Arrays.asList(
            new Student("Ravi", 85),
            new Student("Anu", 72),
            new Student("Kiran", 90),
            new Student("Priya", 65)
        );

        System.out.println("\nStudents with marks > 70 sorted by marks:");
        students.stream()
                .filter(s -> s.marks > 70)
                .sorted((s1, s2) -> Integer.compare(s1.marks, s2.marks))
                .forEach(System.out::println);
    }

    // Part (c)
    public static void processProducts() {
        List<Product> products = Arrays.asList(
            new Product(1, "Laptop", 85000),
            new Product(2, "Phone", 35000),
            new Product(3, "Headphones", 2500),
            new Product(4, "Monitor", 12000)
        );

        System.out.println("\nProducts cheaper than 20000:");
        products.stream()
                .filter(p -> p.price < 20000)
                .forEach(System.out::println);

        System.out.println("\nProducts sorted by price:");
        products.stream()
                .sorted(Comparator.comparingDouble(p -> p.price))
                .forEach(System.out::println);

        double avg = products.stream()
                             .mapToDouble(p -> p.price)
                             .average()
                             .orElse(0.0);
        System.out.println("\nAverage product price: " + avg);
    }
}
