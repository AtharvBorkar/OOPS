# Explanation of `OOPS.java`

This file is a Java program that demonstrates **object-oriented programming (OOP)** concepts in Java. It defines two simple classes (`Pen` and `Student`) and uses them from a `main` method inside the public class `OOPS`.

---

## 1. `class Pen` (lines 1–12)

A `Pen` is a blueprint describing what a pen object is and what it can do.

### Fields (instance variables)

- `String color;` (line 2)
  - A field that stores the color of the pen (e.g., `"blue"`, `"black"`).
  - `String` is a Java type for text.
- `String type;` (line 3)
  - A field that stores the kind of pen (e.g., `"gel"`, `"ballpoint"`).
  - The comment `//ballpoint; gel` is just a note listing the expected values; it is not code.

### Methods (behaviors)

- `public void write()` (lines 5–7)
  - A method that does something: prints `"writing something"` to the console.
  - `public` means it can be called from anywhere.
  - `void` means it returns nothing.
- `public void printColor()` (lines 9–11)
  - A method that prints the pen's color.
  - `this.color` refers to the current object's `color` field — the instance the method was called on.

---

## 2. `class Student` (lines 14–22)

A `Student` is a blueprint describing a student object.

### Fields

- `String name;` (line 15)
  - Stores the student's name.
- `int age;` (line 16)
  - Stores the student's age as a whole number.

### Methods

- `public void printInfo()` (lines 18–21)
  - Prints the student's `name` and `age` to the console, each on its own line.
  - `this.name` and `this.age` refer to the current object's fields.

---

## 3. `public class OOPS` (lines 23–42)

The main program. In Java, the file must be named after the `public` class, so this file is `OOPS.java`. It contains the program's entry point.

### `public static void main(String args[])` (line 24)

The entry point of every Java application:

- `public` — accessible from anywhere.
- `static` — belongs to the class itself, not to any object; can be run without creating an instance.
- `void` — returns nothing.
- `String args[]` — command-line arguments passed to the program (an array of strings). Here it is unused.

### Inside `main` — creating and using `Pen` objects

```java
Pen pen1 = new Pen();
pen1.color = "blue";
pen1.type = "gel";
```

- `new Pen()` creates a new `Pen` object in memory.
- `pen1` is a reference (variable) pointing to that object.
- `pen1.color = "blue"` sets the object's `color` field.
- `pen1.type = "gel"` sets the object's `type` field.

The same pattern repeats for `pen2` (lines 29–31), with color `"black"` and type `"ballpoint"`. This shows that each object has its own independent copy of the fields.

```java
pen1.printColor();
pen2.printColor();
```

- Calls the `printColor()` method on each object.
- Because each object has its own `color`, it prints `blue` then `black`.

### Inside `main` — creating and using a `Student` object

```java
Student s1 = new Student();
s1.name = "John";
s1.age = 22;
s1.printInfo();
```

- Creates a `Student` object, sets its `name` to `"John"` and `age` to `22`.
- Calls `printInfo()`, which prints `John` then `22`.

---

## Key OOP concepts shown in this file

1. **Classes and objects** — `Pen`/`Student` are classes (blueprints); `pen1`, `pen2`, `s1` are objects (instances).
2. **Encapsulation of state** — each object holds its own `color`, `type`, `name`, `age`.
3. **Abstraction of behavior** — methods (`write`, `printColor`, `printInfo`) hide the internal detail ("just print") behind a simple name.
4. **`this` keyword** — refers to the current object whose method is running, used to distinguish a field from a same-named local variable (not strictly needed here, but good practice).

---

## Notes / observations

- There are no constructors; fields are set directly after object creation.
- No access modifiers (like `private`) are used, so all fields are package-visible.
- The `write()` method is defined but never called in `main`.
- The closing braces on line 42 (`}}`) close both the `main` method and the `OOPS` class.