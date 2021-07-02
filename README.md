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

*A class should be open for extension and closed for modification.*

Bad

```java
class AnimalFeeder {
    public void feedDog() {}
    public void feedCat() {}
    public void feedBird() {}
    // ...
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

*Objects of a superclass shall be replaceable with objects of its subclasses without breaking the application.*

Bad

```java
interface Cat {
    void drink();
    void makeSound();
}

class PetCat implements Cat {
    @Override
    public void drink() {
        System.out.println("drinking mike");
    }

    @Override
    public void makeSound() {
        System.out.println("meow");
    }
}

class ToyCat implements Cat {
    @Override
    public void drink() {
        throw new RuntimeException("cannot drink milk");
    }

    @Override
    public void makeSound() {
        System.out.println("meow");
    }
}
```

Good

```java
interface MechanicalCat {
    void makeSound();
}

interface LivingCat extends MechanicalCat {
    void drink();
}

class PetCat implements LivingCat {
    @Override
    public void drink() {
        System.out.println("drinking mike");
    }

    @Override
    public void makeSound() {
        System.out.println("meow");
    }
}

class ToyCat implements MechanicalCat {
    @Override
    public void makeSound() {
        System.out.println("meow");
    }
}
```

## Interface Segregation Principle

*The clients shouldn't be forced to implement the methods that they do not use.*

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
interface TwoDimensionalShape {
    int calculateArea();
}

interface ThreeDimensionalShape extends TwoDimensionalShape {
    int calculateVolume();
}

class Square implements TwoDimensionalShape {
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
}

class Cube implements ThreeDimensionalShape {
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

## Dependency Inversion Principle

*High-level modules should not depend on low-level modules. Both should depend on abstractions.*

![image](https://user-images.githubusercontent.com/11765228/123595239-42bbf000-d823-11eb-9427-17dc12a3edb3.png)

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
