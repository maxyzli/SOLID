# SOLID

SOLID Principles: Explanation and examples

## Single Responsibility Principle

*A class should have one and only one reason to change.*

Bad

```java
class Employee {
    int id;
    int name;
    public void calculateSalary() {} // Finance Team
    public void hireEmployee() {} // HR
     public void evaluateEmployee() {} // Manager
}
```

Good

```java
class Employee {
    int id;
    String name;
    public Employee(int id, String name) {
        this.id = id;
        this.name = name;
    }
}

// Finance Team
class CalculateSalary {
    public static void calculateSalary(Employee e) {}
}

// HR
class HireEmployee {
    public static void hireEmployee(Employee e) {}
}

// Manager
class EvaluateEmployee {
    public static void evaluateEmployee(Employee e) {}
}
```

## Open-Closed Principle

*A class should be open for extension and closed for modification. *

Bad

```java
class AnimalFeeder {
    public void feedDog() {}
    public void feedCat() {}
}
```

Good

```java
interface Animal {
    void feed();
}

class AnimalFeeder {
    public void feed(Animal a) {
        a.feed();
    }
}

class Dog implements Animal {
    public void feed() {}
}

class Cat implements Animal {
    public void feed() {}
}
```

## Liskov Substitution principle

*Substitute a superclass object reference with a subclasses, the program should not break.*

Bad

```java
```

Good

```java
```

## Interface Segregation Principle

*The clients shouldn’t be forced to implement the methods that they do not use.*

Bad

```java
interface Shape {
    int calculateArea();
    int calculateVolume();
}

class Square implements Shape {
    int width;
    int height;

    public Square(int width, int height) {
        this.width = width;
        this.height = height;
    }

    @Override
    public int calculateArea() {
        return width * height;
    }

    @Override
    public int calculateVolume() {
        return 0; // also not follow liskov substitution principle.
    }
}

class Cube implements Shape {
    int side;

    public Cube(int side) {
        this.side = side;
    }

    @Override
    public int calculateArea() {
        return side * side;
    }

    @Override
    public int calculateVolume() {
        return side * side * side;
    }
}
```

Good

```java

```

## Dependency Inversion Principle

*One should depend upon abstractions, not on the concrete implementation.*

Bad

```java
class Laptop {
    public void program() {};
}

class RemoteProgrammer {
    Laptop laptop;
    RemoteProgrammer(Laptop l) {
        laptop = l;
    }
    void code(){
        laptop.program();
    }
}
```

Good

```java
interface Programmable {
    void program();
}

class Computer implements Programmable {
    @Override
    public void program(){}
}

class Programmer {
    Programmable programmable;
    Programmer(Programmable p) {
        programmable = p;
    }
    void code(){
        programmable.program();
    }
}
```
