# Java OOPs Concepts - Complete Explanation

## 1. Classes and Objects

### Class

A blueprint/template for creating objects. It defines properties (variables) and behaviors (methods).

```java
class Student {
    // Properties/Fields
    String name;
    int rollNo;
    double marks;
    
    // Constructor
    Student(String name, int rollNo, double marks) {
        this.name = name;
        this.rollNo = rollNo;
        this.marks = marks;
    }
    
    // Method
    void displayInfo() {
        System.out.println("Name: " + name);
        System.out.println("Roll No: " + rollNo);
        System.out.println("Marks: " + marks);
    }
}
```

The `Student` class defines three properties: `name`, `rollNo`, and `marks`. It has a constructor that initializes these properties and a method `displayInfo()` that prints the student's information.

### Object

An instance of a class. Created using the `new` keyword.

```java
public class Main {
    public static void main(String[] args) {
        // Creating objects
        Student s1 = new Student("John", 101, 85.5);
        Student s2 = new Student("Jane", 102, 92.3);
        
        // Calling methods
        s1.displayInfo();
        s2.displayInfo();
    }
}
```

Here, we create two `Student` objects `s1` and `s2` using the `new` keyword and call the `displayInfo()` method on each object to print their information.

## 2. Encapsulation

Wrapping data (variables) and code (methods) together and hiding internal details.

**Key Points:**
- Use `private` access modifier for variables
- Provide public getter and setter methods
- Achieves data hiding

```java
class BankAccount {
    private double balance;  // Private - hidden from outside
    private String accountNo;
    
    public BankAccount(String accountNo, double initialBalance) {
        this.accountNo = accountNo;
        this.balance = initialBalance;
    }
    
    // Getter method
    public double getBalance() {
        return balance;
    }
    
    // Setter method with validation
    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            System.out.println("Deposited: " + amount);
        }
    }
    
    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            System.out.println("Withdrawn: " + amount);
        }
    }
}

// Usage
BankAccount acc = new BankAccount("123456", 1000.0);
acc.deposit(500);
System.out.println("Balance: " + acc.getBalance());
```

The `BankAccount` class encapsulates the `balance` and `accountNo` properties, making them private. It provides public methods `getBalance()`, `deposit()`, and `withdraw()` to interact with these properties, ensuring data hiding and controlled access.

## 3. Inheritance

A mechanism where a child class inherits properties and methods from a parent class.

**Keywords:** `extends`, `super`

```java
// Parent class
class Animal {
    String name;
    
    public Animal(String name) {
        this.name = name;
    }
    
    public void eat() {
        System.out.println(name + " is eating");
    }
    
    public void sleep() {
        System.out.println(name + " is sleeping");
    }
}

// Child class
class Dog extends Animal {
    String breed;
    
    public Dog(String name, String breed) {
        super(name);  // Call parent constructor
        this.breed = breed;
    }
    
    // Method overriding
    public void eat() {
        System.out.println(name + " the " + breed + " is eating dog food");
    }
    
    public void bark() {
        System.out.println(name + " says: Woof Woof!");
    }
}

// Another child class
class Cat extends Animal {
    public Cat(String name) {
        super(name);
    }
    
    public void meow() {
        System.out.println(name + " says: Meow!");
    }
}

// Usage
Dog myDog = new Dog("Buddy", "Golden Retriever");
myDog.eat();    // Calls overridden method
myDog.sleep();  // Inherited from parent
myDog.bark();   // Dog's own method

Cat myCat = new Cat("Whiskers");
myCat.eat();
myCat.meow();
```

The `Animal` class is the parent class with properties and methods that can be inherited by child classes. The `Dog` and `Cat` classes extend the `Animal` class and can override or add their own methods. The `super` keyword is used to call the parent class constructor.

**Types of Inheritance in Java:**
- ✅ Single Level: `A → B`
- ✅ Multilevel: `A → B → C`
- ✅ Hierarchical: `A → B, A → C`
- ❌ Multiple inheritance NOT supported with classes (use interfaces)

## 4. Polymorphism

"Many forms" - Same action performed in different ways.

### A. Compile-time Polymorphism (Method Overloading)

Same method name, different parameters.

```java
class Calculator {
    // Add two integers
    public int add(int a, int b) {
        return a + b;
    }
    
    // Add three integers (overloaded)
    public int add(int a, int b, int c) {
        return a + b + c;
    }
    
    // Add doubles (overloaded)
    public double add(double a, double b) {
        return a + b;
    }
}

// Usage
Calculator calc = new Calculator();
System.out.println(calc.add(5, 10));      // Calls first method
System.out.println(calc.add(5, 10, 15));  // Calls second method
System.out.println(calc.add(5.5, 10.5));  // Calls third method
```

The `Calculator` class demonstrates method overloading, where the same method name `add` is used with different parameters to perform different operations.

### B. Runtime Polymorphism (Method Overriding)

Parent and child class have same method signature. Decision made at runtime.

```java
class Shape {
    public void draw() {
        System.out.println("Drawing a shape");
    }
}

class Circle extends Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a circle");
    }
}

class Rectangle extends Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a rectangle");
    }
}

// Runtime polymorphism
Shape s1 = new Circle();
Shape s2 = new Rectangle();
s1.draw();  // Output: Drawing a circle
s2.draw();  // Output: Drawing a rectangle
```

The `Shape` class is the parent class with a method `draw()`. The `Circle` and `Rectangle` classes extend the `Shape` class and override the `draw()` method to provide their own implementation. At runtime, the appropriate method is called based on the object type.

## 5. Abstraction

Hiding implementation details and showing only essential features.

**Achieved by:**
- Abstract classes
- Interfaces

### Abstract Class

```java
abstract class Vehicle {
    String brand;
    
    public Vehicle(String brand) {
        this.brand = brand;
    }
    
    // Concrete method
    public void showBrand() {
        System.out.println("Brand: " + brand);
    }
    
    // Abstract method (no body - must be implemented by subclasses)
    public abstract void start();
    public abstract void stop();
}

class Car extends Vehicle {
    public Car(String brand) {
        super(brand);
    }
    
    @Override
    public void start() {
        System.out.println(brand + " car starting with key");
    }
    
    @Override
    public void stop() {
        System.out.println(brand + " car stopping with brakes");
    }
}

class Bike extends Vehicle {
    public Bike(String brand) {
        super(brand);
    }
    
    @Override
    public void start() {
        System.out.println(brand + " bike starting with kick");
    }
    
    @Override
    public void stop() {
        System.out.println(brand + " bike stopping with foot brake");
    }
}

// Usage
Vehicle v1 = new Car("Toyota");
Vehicle v2 = new Bike("Honda");
v1.start();  // Toyota car starting with key
v2.start();  // Honda bike starting with kick
```

The `Vehicle` abstract class defines a blueprint for vehicles with a concrete method `showBrand()` and abstract methods `start()` and `stop()`. The `Car` and `Bike` classes extend the `Vehicle` class and provide their own implementation for the abstract methods.

### Interface

Complete abstraction (all methods are abstract by default).

```java
interface PaymentGateway {
    // Constants (public static final by default)
    double TAX_RATE = 0.18;
    
    // Abstract methods (public abstract by default)
    void processPayment(double amount);
    boolean verifyTransaction(String transactionId);
    void generateReceipt();
}

class CreditCardPayment implements PaymentGateway {
    private String cardNumber;
    
    public CreditCardPayment(String cardNumber) {
        this.cardNumber = cardNumber;
    }
    
    @Override
    public void processPayment(double amount) {
        System.out.println("Processing credit card payment of $" + amount);
    }
    
    @Override
    public boolean verifyTransaction(String transactionId) {
        System.out.println("Verifying transaction: " + transactionId);
        return true;
    }
    
    @Override
    public void generateReceipt() {
        System.out.println("Generating receipt for credit card payment");
    }
}

class UPIPayment implements PaymentGateway {
    private String upiId;
    
    public UPIPayment(String upiId) {
        this.upiId = upiId;
    }
    
    @Override
    public void processPayment(double amount) {
        System.out.println("Processing UPI payment of $" + amount + " from " + upiId);
    }
    
    @Override
    public boolean verifyTransaction(String transactionId) {
        return true;
    }
    
    @Override
    public void generateReceipt() {
        System.out.println("Generating UPI payment receipt");
    }
}

// Usage
PaymentGateway pg1 = new CreditCardPayment("1234-5678-9012-3456");
pg1.processPayment(100.0);

PaymentGateway pg2 = new UPIPayment("user@upi");
pg2.processPayment(50.0);
```

The `PaymentGateway` interface defines a contract for payment processing with abstract methods `processPayment()`, `verifyTransaction()`, and `generateReceipt()`. The `CreditCardPayment` and `UPIPayment` classes implement the `PaymentGateway` interface and provide their own implementation for the abstract methods.

## 6. Constructors

Special methods used to initialize objects.

```java
class Employee {
    int id;
    String name;
    double salary;
    
    // Default constructor
    Employee() {
        id = 0;
        name = "Unknown";
        salary = 0.0;
    }
    
    // Parameterized constructor
    Employee(int id, String name, double salary) {
        this.id = id;
        this.name = name;
        this.salary = salary;
    }
    
    // Copy constructor
    Employee(Employee other) {
        this.id = other.id;
        this.name = other.name;
        this.salary = other.salary;
    }
    
    public void display() {
        System.out.println("ID: " + id + ", Name: " + name + ", Salary: " + salary);
    }
}

// Usage
Employee e1 = new Employee();                    // Default constructor
Employee e2 = new Employee(101, "John", 50000);  // Parameterized constructor
Employee e3 = new Employee(e2);                  // Copy constructor
e1.display();
e2.display();
e3.display();
```

The `Employee` class demonstrates different types of constructors: default, parameterized, and copy constructors. These constructors are used to initialize objects with different sets of values.

## 7. Access Modifiers

| Modifier    | Class | Package | Subclass | World |
|-------------|-------|---------|----------|-------|
| `public`    | ✅    | ✅      | ✅       | ✅    |
| `protected` | ✅    | ✅      | ✅       | ❌    |
| (default)   | ✅    | ✅      | ❌       | ❌    |
| `private`   | ✅    | ❌      | ❌       | ❌    |

```java
class AccessDemo {
    public int publicVar = 1;
    protected int protectedVar = 2;
    int defaultVar = 3;      // package-private
    private int privateVar = 4;
    
    public void showAll() {
        System.out.println(publicVar);
        System.out.println(protectedVar);
        System.out.println(defaultVar);
        System.out.println(privateVar);  // Accessible within same class
    }
}
```

The `AccessDemo` class demonstrates different access modifiers: `public`, `protected`, default (package-private), and `private`. These modifiers control the visibility of class members.

## 8. Static Keyword

Belongs to the class, not to any specific object.

```java
class Counter {
    static int count = 0;  // Shared among all objects
    int id;
    
    public Counter() {
        count++;
        id = count;
        System.out.println("Object " + id + " created");
    }
    
    static void showCount() {
        System.out.println("Total objects created: " + count);
    }
}

// Usage
Counter c1 = new Counter();
Counter c2 = new Counter();
Counter c3 = new Counter();
Counter.showCount();  // Total objects created: 3
```

The `Counter` class demonstrates the use of the `static` keyword. The `count` variable is shared among all objects of the class, and the `showCount()` method is a static method that can be called without creating an object.

## 9. Final Keyword

- `final variable`: Value cannot be changed (constant)
- `final method`: Cannot be overridden
- `final class`: Cannot be inherited

```java
final class ImmutableClass {
    final double PI = 3.14159;
    
    public final void showMessage() {
        System.out.println("Cannot override this method");
    }
}

// This will cause error:
// class Child extends ImmutableClass { }  // ERROR: Cannot inherit from final class
```

The `ImmutableClass` class demonstrates the use of the `final` keyword. The `PI` variable is a constant, and the `showMessage()` method cannot be overridden. The `ImmutableClass` class itself cannot be inherited.

## 10. Complete Example - Student Management System

```java
import java.util.ArrayList;

class Person {
    private String name;
    private int age;
    
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    public String getName() { return name; }
    public int getAge() { return age; }
    
    public void displayInfo() {
        System.out.println("Name: " + name + ", Age: " + age);
    }
}

interface Graded {
    void calculateGrade();
    String getGrade();
}

class Student extends Person implements Graded {
    private int rollNo;
    private double[] marks;
    private String grade;
    
    public Student(String name, int age, int rollNo, double[] marks) {
        super(name, age);
        this.rollNo = rollNo;
        this.marks = marks;
    }
    
    @Override
    public void calculateGrade() {
        double average = 0;
        for (double mark : marks) {
            average += mark;
        }
        average /= marks.length;
        
        if (average >= 90) grade = "A+";
        else if (average >= 80) grade = "A";
        else if (average >= 70) grade = "B";
        else if (average >= 60) grade = "C";
        else grade = "F";
    }
    
    @Override
    public String getGrade() { return grade; }
    
    @Override
    public void displayInfo() {
        super.displayInfo();
        System.out.println("Roll No: " + rollNo);
        System.out.println("Grade: " + grade);
        System.out.println("---");
    }
}

class Teacher extends Person {
    private String subject;
    private ArrayList<Student> students;
    
    public Teacher(String name, int age, String subject) {
        super(name, age);
        this.subject = subject;
        this.students = new ArrayList<>();
    }
    
    public void addStudent(Student student) {
        students.add(student);
    }
    
    public void displayAllStudents() {
        System.out.println("Students under " + getName() + ":");
        for (Student s : students) {
            s.displayInfo();
        }
    }
}

public class SchoolManagement {
    public static void main(String[] args) {
        // Create students
        double[] marks1 = {95, 87, 92, 88, 90};
        Student s1 = new Student("Alice", 20, 101, marks1);
        s1.calculateGrade();
        
        double[] marks2 = {78, 82, 75, 80, 85};
        Student s2 = new Student("Bob", 21, 102, marks2);
        s2.calculateGrade();
        
        // Create teacher
        Teacher t1 = new Teacher("Dr. Smith", 45, "Mathematics");
        t1.addStudent(s1);
        t1.addStudent(s2);
        
        // Display information
        t1.displayAllStudents();
    }
}
```

The `SchoolManagement` system demonstrates the use of classes, objects, inheritance, interfaces, and other OOP concepts. It includes the `Person`, `Student`, `Teacher`, and `Graded` classes, and the `SchoolManagement` class that creates and manages objects of these classes.

## Key Takeaways

1. **Encapsulation**: Data hiding using private variables + public getters/setters
2. **Inheritance**: Code reusability using `extends` keyword
3. **Polymorphism**: Same method, different behavior (overloading & overriding)
4. **Abstraction**: Hide complexity using abstract classes and interfaces
5. **Classes & Objects**: Blueprint and instances
6. **Constructors**: Initialize objects
7. **Access Modifiers**: Control visibility
8. **Static**: Class-level members
9. **Final**: Prevent modification/inheritance/overriding

## Best Practices

✅ Always use meaningful class and method names
✅ Follow encapsulation - keep fields private
✅ Use constructors for initialization
✅ Override `toString()`, `equals()` when needed
✅ Use interfaces for loose coupling
✅ Follow DRY principle (Don't Repeat Yourself)
✅ Use proper access modifiers
