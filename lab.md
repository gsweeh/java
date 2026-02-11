# Java Lab Exam Preparation (Programs 1 to 10)

## Program 1: Calculator Using Scope of Variables and `this` Keyword
**Description:** Demonstrates arithmetic operations and variable scope: static variable, instance variable, local variable, and block variable.

**Code:**
```java
import java.util.Scanner;

class Calculator {
    static int operations = 0; // static variable
    int a, b; // instance variables

    Calculator(int a, int b) {
        this.a = a;
        this.b = b;
    }

    int calculate(char op) {
        int result; // local variable
        switch (op) {
            case '+': {
                int temp = this.a + this.b; // block variable
                result = temp;
                break;
            }
            case '-': {
                int temp = this.a - this.b;
                result = temp;
                break;
            }
            case '*': {
                int temp = this.a * this.b;
                result = temp;
                break;
            }
            case '/': {
                if (this.b == 0) throw new ArithmeticException("Cannot divide by zero");
                int temp = this.a / this.b;
                result = temp;
                break;
            }
            default:
                throw new IllegalArgumentException("Invalid operator");
        }
        operations++;
        return result;
    }
}

public class Program1 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        while (true) {
            System.out.print("Enter first number: ");
            int x = sc.nextInt();
            System.out.print("Enter second number: ");
            int y = sc.nextInt();

            System.out.print("Enter operator (+,-,*,/, q to quit): ");
            String op = sc.next();
            if (op.equalsIgnoreCase("q")) break;

            Calculator c = new Calculator(x, y);
            try {
                System.out.println("Result = " + c.calculate(op.charAt(0)));
                System.out.println("Operations done = " + Calculator.operations);
            } catch (Exception e) {
                System.out.println("Error: " + e.getMessage());
            }

            System.out.print("Continue? (y/n): ");
            if (!sc.next().equalsIgnoreCase("y")) break;
        }

        sc.close();
    }
}
```

**Expected Output:**
```text
Enter first number: 5
Enter second number: 3
Enter operator (+,-,*,/, q to quit): +
Result = 8
Operations done = 1
Continue? (y/n): n
```

**Viva Questions:**
1. What is the use of `this` keyword? - It refers to the current object, used to access instance variables when names clash.
2. Difference between static and instance variable? - Static belongs to class (shared), instance belongs to each object.
3. What is variable scope? - Scope is the region where a variable is visible (local/block/method/class).

**Key Concepts:** `this`, variable scope, static variable, switch-case, exception handling.

---

## Program 2: Constructor Overloading in Bank Account
**Description:** Demonstrates default and parameterized constructors, deposit/withdraw methods, and static account count.

**Code:**
```java
class BankAccount {
    static int totalAccounts = 0;
    String name;
    int balance;

    BankAccount(String name) {
        this(name, 0); // constructor overloading
    }

    BankAccount(String name, int balance) {
        this.name = name;
        this.balance = balance;
        totalAccounts++;
        System.out.println("Account created for " + name + " with balance " + balance);
    }

    void deposit(int amount) {
        balance += amount;
        System.out.println(amount + " deposited. Balance = " + balance);
    }

    void withdraw(int amount) {
        if (amount <= balance) {
            balance -= amount;
            System.out.println(amount + " withdrawn. Balance = " + balance);
        } else {
            System.out.println("Insufficient balance for " + name);
        }
    }

    static void showTotalAccounts() {
        System.out.println("Total accounts = " + totalAccounts);
    }
}

public class Program2 {
    public static void main(String[] args) {
        BankAccount user1 = new BankAccount("Pankaj");
        BankAccount user2 = new BankAccount("Prem", 500);

        user1.deposit(300);
        user2.deposit(1000);
        user1.withdraw(50);
        user2.withdraw(200);

        BankAccount.showTotalAccounts();
    }
}
```

**Expected Output:**
```text
Account created for Pankaj with balance 0
Account created for Prem with balance 500
300 deposited. Balance = 300
1000 deposited. Balance = 1500
50 withdrawn. Balance = 250
200 withdrawn. Balance = 1300
Total accounts = 2
```

**Viva Questions:**
1. What is constructor overloading? - Multiple constructors in the same class with different parameter lists.
2. Why `this(name, 0)` is used? - To reuse another constructor and avoid duplicate initialization code.
3. Why `totalAccounts` is static? - Because it is shared across all objects.

**Key Concepts:** constructor overloading, static members, object initialization, encapsulated behavior.

---

## Program 3: Abstract Class for Shape Area Calculation
**Description:** Uses abstract class `Shape` and concrete classes `Square`, `Triangle`, and `Circle` to compute areas.

**Code:**
```java
import java.util.Scanner;

abstract class Shape {
    abstract double area();

    void show(String name) {
        System.out.println(name + " instance is called");
    }
}

class Square extends Shape {
    double side;

    Square(double side) {
        this.side = side;
    }

    double area() {
        return side * side;
    }
}

class Triangle extends Shape {
    double base, height;

    Triangle(double base, double height) {
        this.base = base;
        this.height = height;
    }

    double area() {
        return 0.5 * base * height;
    }
}

class Circle extends Shape {
    double radius;

    Circle(double radius) {
        this.radius = radius;
    }

    double area() {
        return Math.PI * radius * radius;
    }
}

public class Program3 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter side of square: ");
        Square s = new Square(sc.nextDouble());
        System.out.println("Area of Square = " + s.area());
        s.show("Square");

        System.out.print("Enter base of triangle: ");
        double b = sc.nextDouble();
        System.out.print("Enter height of triangle: ");
        double h = sc.nextDouble();
        Triangle t = new Triangle(b, h);
        System.out.println("Area of Triangle = " + t.area());
        t.show("Triangle");

        System.out.print("Enter radius of circle: ");
        Circle c = new Circle(sc.nextDouble());
        System.out.println("Area of Circle = " + c.area());
        c.show("Circle");

        sc.close();
    }
}
```

**Expected Output:**
```text
Enter side of square: 2
Area of Square = 4.0
Square instance is called
Enter base of triangle: 2
Enter height of triangle: 2
Area of Triangle = 2.0
Triangle instance is called
Enter radius of circle: 5
Area of Circle = 78.53981633974483
Circle instance is called
```

**Viva Questions:**
1. Can we create object of abstract class? - No, abstract classes cannot be instantiated directly.
2. Why use abstract method `area()`? - To force each child class to provide its own area logic.
3. Is `show()` abstract? - No, it is a concrete method inside abstract class.

**Key Concepts:** abstraction, inheritance, runtime binding, polymorphism.

---

## Program 4: Abstraction and Runtime Polymorphism
**Description:** Demonstrates abstraction using `Printer` abstract class and runtime polymorphism using `Vehicle` interface.

**Code:**
```java
abstract class Printer {
    abstract void configure();
    abstract void print(String text);
}

class DotMatrix extends Printer {
    void configure() {
        System.out.println("Starting DotMatrix configuration...");
        System.out.println("Checking paper alignment...");
        System.out.println("Setting print head position...");
        System.out.println("DotMatrix configured successfully.");
    }

    void print(String text) {
        System.out.println("Preparing DotMatrix to print...");
        System.out.println("DotMatrix print: " + text);
        System.out.println("DotMatrix printing completed.");
    }
}

class LaserJet extends Printer {
    void configure() {
        System.out.println("Starting LaserJet configuration...");
        System.out.println("Warming up laser unit...");
        System.out.println("Calibrating toner levels...");
        System.out.println("LaserJet configured successfully.");
    }

    void print(String text) {
        System.out.println("Sending data to LaserJet...");
        System.out.println("LaserJet print: " + text);
        System.out.println("LaserJet printing completed.");
    }
}

interface Vehicle {
    void drive();
}

class Car implements Vehicle {
    public void drive() {
        System.out.println("Starting car engine...");
        System.out.println("Car is driving on road.");
        System.out.println("Car reached destination.");
    }
}

class Motorcycle implements Vehicle {
    public void drive() {
        System.out.println("Starting motorcycle engine...");
        System.out.println("Motorcycle is moving fast.");
        System.out.println("Motorcycle ride completed.");
    }
}

public class Program4 {
    public static void main(String[] args) {

        System.out.println("--- Abstraction Demo ---");

        Printer p1 = new DotMatrix();
        Printer p2 = new LaserJet();

        p1.configure();
        p1.print("Hello");

        System.out.println();

        p2.configure();
        p2.print("World");

        System.out.println("\n--- Runtime Polymorphism Demo ---");

        Vehicle v;

        v = new Car();
        v.drive();

        System.out.println();

        v = new Motorcycle();
        v.drive();
    }
}

```

**Expected Output:**
```text
--- Abstraction Demo ---
DotMatrix configured
DotMatrix print: Hello
LaserJet configured
LaserJet print: World
--- Runtime Polymorphism Demo ---
Car is driving on road
Motorcycle is moving fast
```

**Viva Questions:**
1. What is runtime polymorphism? - Method call resolved at runtime based on actual object type.
2. Why use abstract class in printer example? - Common structure with mandatory specialized implementation.
3. Difference between interface and abstract class? - Interface defines contract; abstract class can have both abstract and concrete methods.

**Key Concepts:** abstraction, interface, runtime polymorphism, dynamic method dispatch.

---

## Program 5: Multiple Interfaces (`Personal` and `Official`)
**Description:** Creates `Employee` class implementing two interfaces to display personal and official details.

**Code:**
```java
import java.util.Scanner;

interface Personal {
    void displayPersonal();
}

interface Official {
    void displayOfficial();
}

class Employee implements Personal, Official {
    String name, gender, phone;
    int age;
    String empId, designation, department;
    double salary;

    Employee(String name, String gender, String phone, int age,
             String empId, String designation, String department, double salary) {
        this.name = name;
        this.gender = gender;
        this.phone = phone;
        this.age = age;
        this.empId = empId;
        this.designation = designation;
        this.department = department;
        this.salary = salary;
    }

    public void displayPersonal() {
        System.out.println("Name: " + name);
        System.out.println("Gender: " + gender);
        System.out.println("Age: " + age);
        System.out.println("Phone: " + phone);
    }

    public void displayOfficial() {
        System.out.println("Employee ID: " + empId);
        System.out.println("Designation: " + designation);
        System.out.println("Department: " + department);
        System.out.println("Salary: " + salary);
    }
}

public class Program5 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter name: ");
        String name = sc.nextLine();
        System.out.print("Enter age: ");
        int age = sc.nextInt();
        sc.nextLine();
        System.out.print("Enter gender: ");
        String gender = sc.nextLine();
        System.out.print("Enter phone: ");
        String phone = sc.nextLine();
        System.out.print("Enter employee ID: ");
        String empId = sc.nextLine();
        System.out.print("Enter designation: ");
        String designation = sc.nextLine();
        System.out.print("Enter department: ");
        String department = sc.nextLine();
        System.out.print("Enter salary: ");
        double salary = sc.nextDouble();

        Employee e = new Employee(name, gender, phone, age, empId, designation, department, salary);

        System.out.println("\nEmployee Details");
        e.displayPersonal();
        e.displayOfficial();

        sc.close();
    }
}
```

**Expected Output:**
```text
Enter name: Pankaj
Enter age: 22
Enter gender: Male
Enter phone: 9876543210
Enter employee ID: E101
Enter designation: Developer
Enter department: IT
Enter salary: 50000

Employee Details
Name: Pankaj
Gender: Male
Age: 22
Phone: 9876543210
Employee ID: E101
Designation: Developer
Department: IT
Salary: 50000.0
```

**Viva Questions:**
1. Can a class implement multiple interfaces in Java? - Yes, Java supports multiple interface inheritance.
2. Why use interfaces here? - To separate concerns (personal vs official data behavior).
3. Why methods are `public` in implementation? - Interface methods are implicitly `public`, so implementation cannot reduce visibility.

**Key Concepts:** multiple interfaces, data modeling, method overriding.

---

## Program 6: User-Defined Exception with `throw` and `throws`
**Description:** Validates age using custom exception and validates division using predefined `ArithmeticException`.

**Code:**
```java
import java.util.Scanner;

class InvalidAgeException extends Exception {
    InvalidAgeException(String message) {
        super(message);
    }
}

public class Program6 {
    static void validateAge(int age) throws InvalidAgeException {
        if (age < 18) {
            throw new InvalidAgeException("Error: Enter valid age (18 or above)");
        }
        System.out.println("Registration Successful");
    }

    static int divideNumbers(int dividend, int divisor) {
        if (divisor == 0) {
            throw new ArithmeticException("Error: Divisor should not be zero");
        }
        return dividend / divisor;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int choice;

        while (true) {
            System.out.println("\n1. Age validation");
            System.out.println("2. Arithmetic validation");
            System.out.println("3. Exit");
            System.out.print("Enter your choice: ");
            choice = sc.nextInt();

            try {
                switch (choice) {
                    case 1:
                        System.out.print("Enter age: ");
                        validateAge(sc.nextInt());
                        break;
                    case 2:
                        System.out.print("Enter dividend: ");
                        int a = sc.nextInt();
                        System.out.print("Enter divisor: ");
                        int b = sc.nextInt();
                        System.out.println("Result = " + divideNumbers(a, b));
                        break;
                    case 3:
                        System.out.println("Program Ended");
                        sc.close();
                        return;
                    default:
                        System.out.println("Invalid Option");
                }
            } catch (InvalidAgeException | ArithmeticException e) {
                System.out.println(e.getMessage());
            }
        }
    }
}
```

**Expected Output:**
```text
1. Age validation
2. Arithmetic validation
3. Exit
Enter your choice: 1
Enter age: 5
Error: Enter valid age (18 or above)

1. Age validation
2. Arithmetic validation
3. Exit
Enter your choice: 2
Enter dividend: 5
Enter divisor: 0
Error: Divisor should not be zero
```

**Viva Questions:**
1. Why do we use `throws` in `validateAge`? - It declares that the method may throw `InvalidAgeException`.
2. Difference between `throw` and `throws`? - `throw` actually throws exception; `throws` declares possible exception.
3. Is `ArithmeticException` checked or unchecked? - Unchecked (runtime exception).

**Key Concepts:** custom exception, `throw`, `throws`, try-catch, menu-driven program.

---

## Program 7: Thread Life Cycle Demonstration
**Description:** Uses two threads with `start()`, `sleep()`, `yield()`, and `wait()/notify()` to show lifecycle transitions.

**Code:**
```java
class Thread1 extends Thread {
    private final Object lock;

    Thread1(Object lock) {
        this.lock = lock;
    }

    public void run() {
        synchronized (lock) {
            try {
                for (int i = 1; i <= 5; i++) {
                    System.out.println("Thread1 value: " + i);
                    Thread.sleep(500);
                    Thread.yield();
                }
                lock.notify();
                System.out.println("Thread1 notifies Thread2");
            } catch (InterruptedException e) {
                System.out.println("Thread1 interrupted");
            }
        }
    }
}

class Thread2 extends Thread {
    private final Object lock;

    Thread2(Object lock) {
        this.lock = lock;
    }

    public void run() {
        synchronized (lock) {
            try {
                System.out.println("Thread2 is waiting...");
                lock.wait();
                for (int i = 10; i <= 15; i++) {
                    System.out.println("Thread2 value: " + i);
                    Thread.sleep(500);
                    Thread.yield();
                }
            } catch (InterruptedException e) {
                System.out.println("Thread2 interrupted");
            }
        }
    }
}

public class Program7 {
    public static void main(String[] args) throws InterruptedException {
        Object lock = new Object();

        Thread1 t1 = new Thread1(lock);
        Thread2 t2 = new Thread2(lock);

        System.out.println("Before start: " + t1.getState());

        t2.start();
        Thread.sleep(200); // ensure Thread2 enters waiting state
        t1.start();

        System.out.println("After start: " + t1.getState());

        t1.join();
        t2.join();

        System.out.println("After completion: " + t1.getState() + ", " + t2.getState());
    }
}
```

**Expected Output:**
```text
Before start: NEW
Thread2 is waiting...
After start: RUNNABLE
Thread1 value: 1
Thread1 value: 2
Thread1 value: 3
Thread1 value: 4
Thread1 value: 5
Thread1 notifies Thread2
Thread2 value: 10
Thread2 value: 11
Thread2 value: 12
Thread2 value: 13
Thread2 value: 14
Thread2 value: 15
After completion: TERMINATED, TERMINATED
```

**Viva Questions:**
1. What does `start()` do? - Creates a new call stack and invokes `run()` in a new thread.
2. Why call `wait()` inside synchronized block? - `wait()` needs monitor lock of object.
3. Why not use `stop()`? - `stop()` is deprecated and unsafe; use interruption/flags instead.

**Key Concepts:** threads, lifecycle states, synchronization, inter-thread communication.

---

## Program 8: Producer-Consumer Using `wait()` and `notifyAll()`
**Description:** Implements classic producer-consumer problem using synchronized methods and one shared buffer.

**Code:**
```java
import java.util.Scanner;

class Buffer {
    private int item;
    private boolean available = false;
    private int next = 0;

    synchronized void produce() throws InterruptedException {
        while (available) {
            wait();
        }
        item = next++;
        System.out.println("Producer put: " + item);
        available = true;
        notifyAll();
    }

    synchronized void consume(String consumerName) throws InterruptedException {
        while (!available) {
            wait();
        }
        System.out.println(consumerName + " got: " + item);
        available = false;
        notifyAll();
    }
}

class Producer extends Thread {
    private final Buffer buffer;
    private final int n;

    Producer(Buffer buffer, int n) {
        this.buffer = buffer;
        this.n = n;
    }

    public void run() {
        try {
            for (int i = 0; i < n; i++) {
                buffer.produce();
                Thread.sleep(300);
            }
        } catch (InterruptedException e) {
            System.out.println("Producer interrupted");
        }
    }
}

class Consumer extends Thread {
    private final Buffer buffer;
    private final int n;

    Consumer(Buffer buffer, int n) {
        this.buffer = buffer;
        this.n = n;
    }

    public void run() {
        try {
            for (int i = 0; i < n; i++) {
                buffer.consume("Consumer");
                Thread.sleep(300);
            }
        } catch (InterruptedException e) {
            System.out.println("Consumer interrupted");
        }
    }
}

public class Program8 {
    public static void main(String[] args) throws InterruptedException {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter number of items to produce: ");
        int n = sc.nextInt();

        Buffer buffer = new Buffer();
        Producer p = new Producer(buffer, n);
        Consumer c = new Consumer(buffer, n);

        p.start();
        c.start();

        p.join();
        c.join();

        System.out.println("Done");
        sc.close();
    }
}
```

**Expected Output:**
```text
Enter number of items to produce: 3
Producer put: 0
Consumer got: 0
Producer put: 1
Consumer got: 1
Producer put: 2
Consumer got: 2
Done
```

**Viva Questions:**
1. Why use `while` before `wait()`? - To re-check condition after wake-up and avoid spurious wakeups.
2. Difference between `notify()` and `notifyAll()`? - `notify()` wakes one waiting thread, `notifyAll()` wakes all waiting threads.
3. Why methods are synchronized? - To ensure mutual exclusion on shared buffer state.

**Key Concepts:** producer-consumer, synchronization, wait-notify, shared resource, race condition prevention.

---

## Program 9: Generic Class and Generic Method
**Description:** Implements generic class `Storage<T>` and generic method `printArray<E>` for multiple data types.

**Code:**
```java
class Storage<T> {
    private T item;

    void setItem(T item) {
        this.item = item;
    }

    T getItem() {
        return item;
    }

    static <E> void printArray(E[] array) {
        for (E element : array) {
            System.out.print(element + " ");
        }
        System.out.println();
    }
}

public class Program9 {
    public static void main(String[] args) {
        Storage<Integer> intStore = new Storage<>();
        intStore.setItem(100);
        System.out.println("Stored Integer: " + intStore.getItem());

        Storage<String> strStore = new Storage<>();
        strStore.setItem("Generics in Java");
        System.out.println("Stored String: " + strStore.getItem());

        Storage<Double> dblStore = new Storage<>();
        dblStore.setItem(300.0);
        System.out.println("Stored Double: " + dblStore.getItem());

        Integer[] intArr = {1, 2, 3, 4, 5};
        String[] strArr = {"Integer", "String", "Double"};
        Double[] dblArr = {10.9, 20.9, 30.9, 40.0};
        Character[] charArr = {'a', 'b', 'c', 'd'};

        System.out.println("Integer Array:");
        Storage.printArray(intArr);
        System.out.println("String Array:");
        Storage.printArray(strArr);
        System.out.println("Double Array:");
        Storage.printArray(dblArr);
        System.out.println("Character Array:");
        Storage.printArray(charArr);
    }
}
```

**Expected Output:**
```text
Stored Integer: 100
Stored String: Generics in Java
Stored Double: 300.0
Integer Array:
1 2 3 4 5
String Array:
Integer String Double
Double Array:
10.9 20.9 30.9 40.0
Character Array:
a b c d
```

**Viva Questions:**
1. Why generics are used? - For type safety and code reusability.
2. What is type parameter `<T>`? - Placeholder for actual type at compile time.
3. Can static methods use class type parameter directly? - No, use method-level generic parameter like `<E>`.

**Key Concepts:** generics, type safety, reusable code, generic methods.

---

## Program 10: RESTful API with GET, POST, PUT, DELETE (Java 17)
**Description:** Builds a simple REST-style API for `Student` resource using Java 17 built-in `HttpServer`.

**Code:**
```java
import com.sun.net.httpserver.HttpExchange;
import com.sun.net.httpserver.HttpServer;

import java.io.IOException;
import java.net.InetSocketAddress;
import java.net.URLDecoder;
import java.nio.charset.StandardCharsets;
import java.util.Map;
import java.util.concurrent.ConcurrentHashMap;

public class Program10 {
    static class Student {
        int id;
        String name;
        int age;

        Student(int id, String name, int age) {
            this.id = id;
            this.name = name;
            this.age = age;
        }

        public String toString() {
            return "{\"id\":" + id + ",\"name\":\"" + name + "\",\"age\":" + age + "}";
        }
    }

    private static final Map<Integer, Student> DB = new ConcurrentHashMap<>();

    public static void main(String[] args) throws IOException {
        HttpServer server = HttpServer.create(new InetSocketAddress(8080), 0);
        server.createContext("/students", Program10::handleRequest);
        server.start();
        System.out.println("Server running at http://localhost:8080/students");
        System.out.println("Use GET, POST, PUT, DELETE with query params id,name,age");
    }

    private static void handleRequest(HttpExchange exchange) throws IOException {
        String method = exchange.getRequestMethod();
        Map<String, String> q = parseQuery(exchange.getRequestURI().getRawQuery());

        try {
            switch (method) {
                case "GET":
                    handleGet(exchange, q);
                    break;
                case "POST":
                    handlePost(exchange, q);
                    break;
                case "PUT":
                    handlePut(exchange, q);
                    break;
                case "DELETE":
                    handleDelete(exchange, q);
                    break;
                default:
                    send(exchange, 405, "Method Not Allowed");
            }
        } catch (Exception e) {
            send(exchange, 400, "Error: " + e.getMessage());
        }
    }

    private static void handleGet(HttpExchange exchange, Map<String, String> q) throws IOException {
        if (q.containsKey("id")) {
            int id = Integer.parseInt(q.get("id"));
            Student s = DB.get(id);
            send(exchange, 200, s == null ? "No record found" : s.toString());
        } else {
            if (DB.isEmpty()) {
                send(exchange, 200, "No records found");
            } else {
                StringBuilder sb = new StringBuilder();
                for (Student s : DB.values()) sb.append(s).append("\n");
                send(exchange, 200, sb.toString().trim());
            }
        }
    }

    private static void handlePost(HttpExchange exchange, Map<String, String> q) throws IOException {
        int id = Integer.parseInt(required(q, "id"));
        String name = required(q, "name");
        int age = Integer.parseInt(required(q, "age"));
        DB.put(id, new Student(id, name, age));
        send(exchange, 201, "Student added");
    }

    private static void handlePut(HttpExchange exchange, Map<String, String> q) throws IOException {
        int id = Integer.parseInt(required(q, "id"));
        Student s = DB.get(id);
        if (s == null) {
            send(exchange, 404, "Student not found");
            return;
        }
        if (q.containsKey("name")) s.name = q.get("name");
        if (q.containsKey("age")) s.age = Integer.parseInt(q.get("age"));
        send(exchange, 200, "Student updated");
    }

    private static void handleDelete(HttpExchange exchange, Map<String, String> q) throws IOException {
        int id = Integer.parseInt(required(q, "id"));
        Student removed = DB.remove(id);
        send(exchange, 200, removed == null ? "Student not found" : "Student deleted");
    }

    private static String required(Map<String, String> q, String key) {
        String value = q.get(key);
        if (value == null || value.isBlank()) throw new IllegalArgumentException("Missing parameter: " + key);
        return value;
    }

    private static Map<String, String> parseQuery(String query) {
        Map<String, String> map = new ConcurrentHashMap<>();
        if (query == null || query.isBlank()) return map;
        for (String pair : query.split("&")) {
            String[] parts = pair.split("=", 2);
            String key = URLDecoder.decode(parts[0], StandardCharsets.UTF_8);
            String val = parts.length > 1 ? URLDecoder.decode(parts[1], StandardCharsets.UTF_8) : "";
            map.put(key, val);
        }
        return map;
    }

    private static void send(HttpExchange exchange, int code, String body) throws IOException {
        byte[] bytes = body.getBytes(StandardCharsets.UTF_8);
        exchange.getResponseHeaders().set("Content-Type", "application/json; charset=UTF-8");
        exchange.sendResponseHeaders(code, bytes.length);
        exchange.getResponseBody().write(bytes);
        exchange.close();
    }
}
```

**Expected Output:**
```text
Server running at http://localhost:8080/students
Use GET, POST, PUT, DELETE with query params id,name,age

POST  /students?id=1&name=Rohit&age=27   -> Student added
POST  /students?id=2&name=Suresh&age=30  -> Student added
GET   /students                           -> {"id":1,"name":"Rohit","age":27} ...
PUT   /students?id=2&name=Pavi&age=28    -> Student updated
GET   /students?id=2                      -> {"id":2,"name":"Pavi","age":28}
DELETE /students?id=1                     -> Student deleted
GET   /students?id=1                      -> No record found
```

**Viva Questions:**
1. What is REST? - Architectural style where resources are accessed via URIs using HTTP methods.
2. Why different HTTP methods? - GET read, POST create, PUT update, DELETE remove.
3. Why `ConcurrentHashMap` used? - Thread-safe in-memory storage for concurrent requests.

**Key Concepts:** REST API, HTTP methods, web resource, Java 17 `HttpServer`, CRUD operations.

---

## Quick Exam Tips (Write Fast + Explain Clearly)
- Write class/method skeleton first, then fill logic.
- Use clear naming (`validateAge`, `printArray`, `produce`) so viva becomes easy.
- In viva, always mention where OOP concept appears in your code.
- Keep one short sample input/output ready for each program.
