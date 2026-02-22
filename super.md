## The super keyword in Java is used to refer to the immediate parent class object in an inheritance hierarchy. It allows a subclass to explicitly access parent class members when they are hidden or overridden. This keyword helps maintain clarity and control while working with inheritance.

- Used to call parent class constructors using super().
- Helps access parent class methods and variables when overridden or hidden.
- Ensures proper inheritance behavior and code reusability.


# Super with variables

```java
// Base class vehicle
class Vehicle {
    int maxSpeed = 120;
}

// sub class Car extending vehicle
class Car extends Vehicle {
    int maxSpeed = 180;

    void display()
    {
        // print maxSpeed from the vehicle class 
        // using super
        System.out.println("Maximum Speed: "
                           + super.maxSpeed);
    }
}

// Driver Program
class Test {
    public static void main(String[] args)
    {
        Car small = new Car();
        small.display();
    }
}
```

# Super with methods
```java
// superclass Person
class Person {
    void message()
    {
        System.out.println("This is person class\n");
    }
}

// Subclass Student
class Student extends Person {
    void message()
    {
        System.out.println("This is student class");
    }
    
    // Note that display() is
    // only in Student class
    void display()
    {
        // will invoke or call current
        // class message() method
        message();

        // will invoke or call parent
        // class message() method
        super.message();
    }
}

// Driver Program
class Test {
    public static void main(String args[])
    {
        Student s = new Student();

        // calling display() of Student
        s.display();
    }
}
```
