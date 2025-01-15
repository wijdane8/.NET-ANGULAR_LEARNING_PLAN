# **.NET and Angular Guide: Day 2 - Object-Oriented Programming (OOP) in C#**

Welcome to Day 2 of your self-paced C# learning journey! Today, you’ll dive into the core concepts of Object-Oriented Programming (OOP), which is essential for writing efficient and maintainable code. You'll learn about classes, objects, properties, methods, inheritance, and polymorphism. Let's get started!

---

## **🧩 Understand the Basics of OOP**
Object-Oriented Programming (OOP) is a programming paradigm that uses objects and classes to organize code.

### **Key Concepts:**
1️⃣ **Class:** A blueprint for creating objects. It defines properties and methods.
2️⃣ **Object:** An instance of a class.
3️⃣ **Property:** A variable within a class that defines the characteristics of an object.
4️⃣ **Method:** A function inside a class that defines the behavior of an object.

💡 **Analogy:**
Think of a class as a template for a car. The template (class) defines properties like color and model and methods like start() or stop(). The actual car you drive is an object created from that template.

---

## **🧩 Create Your First Class and Object**
Follow these steps to create a simple class and object in C#.

1️⃣ **Steps to Create a Class:**
1. Open **Visual Studio** or **Visual Studio Code**.
2. Create a new console project.
3. Write the following code:

```csharp
using System;

namespace OOPExample
{
    class Car
    {
        public string Color { get; set; }
        public string Model { get; set; }

        public void Start()
        {
            Console.WriteLine($"The {Color} {Model} is starting.");
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            Car myCar = new Car();
            myCar.Color = "Red";
            myCar.Model = "Toyota";
            myCar.Start();
        }
    }
}
```

4. Run your program to see the output.

💡 **Explanation:**
- `public string Color { get; set; }` – This defines a property with getters and setters.
- `public void Start()` – This is a method that prints a message to the console.
- `Car myCar = new Car();` – This creates a new object from the `Car` class.

---

## **🧩 Properties and Methods**
Properties and methods are the building blocks of a class.

### **Properties:**
Properties define the characteristics of an object.

🔧 **Example:**
```csharp
public class Person
{
    public string Name { get; set; }
    public int Age { get; set; }
}
```

### **Methods:**
Methods define the behavior of an object.

🔧 **Example:**
```csharp
public class Person
{
    public string Name { get; set; }
    public void Introduce()
    {
        Console.WriteLine($"Hello, my name is {Name}.");
    }
}
```

💡 **Exercise:**
1. Create a `Person` class with properties `Name` and `Age`.
2. Create a method `Introduce()` that prints a message introducing the person.
3. In your `Main()` method, create a `Person` object and call the `Introduce()` method.

---

## **🧩 Constructors**
A constructor is a special method that is automatically called when an object is created.

### **Default Constructor:**
```csharp
public class Person
{
    public string Name { get; set; }
    public int Age { get; set; }

    // Default constructor
    public Person()
    {
        Name = "Unknown";
        Age = 0;
    }
}
```

### **Parameterized Constructor:**
```csharp
public class Person
{
    public string Name { get; set; }
    public int Age { get; set; }

    // Parameterized constructor
    public Person(string name, int age)
    {
        Name = name;
        Age = age;
    }
}
```

💡 **Exercise:**
1. Create a `Person` class with a parameterized constructor that takes `Name` and `Age` as parameters.
2. In your `Main()` method, create a `Person` object using the constructor and print the details to the console.

---

## **🧩 Inheritance**
Inheritance allows you to create a new class that reuses, extends, or modifies the behavior of another class.

### **Example:**
```csharp
public class Animal
{
    public void Eat()
    {
        Console.WriteLine("This animal is eating.");
    }
}

public class Dog : Animal
{
    public void Bark()
    {
        Console.WriteLine("The dog is barking.");
    }
}

class Program
{
    static void Main(string[] args)
    {
        Dog myDog = new Dog();
        myDog.Eat(); // Inherited from Animal class
        myDog.Bark();
    }
}
```

💡 **Exercise:**
1. Create a base class `Vehicle` with a method `Drive()`.
2. Create a derived class `Car` that inherits from `Vehicle` and adds a method `StartEngine()`.
3. In your `Main()` method, create a `Car` object and call both methods.

---

## **🧩 Polymorphism**
Polymorphism allows methods to have different implementations based on the object calling them.

### **Example:**
```csharp
public class Animal
{
    public virtual void Speak()
    {
        Console.WriteLine("The animal makes a sound.");
    }
}

public class Dog : Animal
{
    public override void Speak()
    {
        Console.WriteLine("The dog barks.");
    }
}

class Program
{
    static void Main(string[] args)
    {
        Animal myAnimal = new Animal();
        myAnimal.Speak();

        Animal myDog = new Dog();
        myDog.Speak(); // Polymorphic behavior
    }
}
```

💡 **Exercise:**
1. Create a base class `Shape` with a virtual method `Draw()`.
2. Create two derived classes `Circle` and `Rectangle` that override the `Draw()` method.
3. In your `Main()` method, use polymorphism to call `Draw()` on both objects.

---

## **🧩 Practical Labs**

### **Lab 1: Create a Class and Object**
1. Create a `Car` class with properties `Brand` and `Color`.
2. Add a method `Start()` that prints a message like "The red Toyota is starting."
3. In your `Main()` method, create a `Car` object and call the `Start()` method.

### **Lab 2: Implement Inheritance**
1. Create a base class `Employee` with a method `Work()`.
2. Create a derived class `Manager` that adds a method `ManageTeam()`.
3. In your `Main()` method, create a `Manager` object and call both methods.

### **Lab 3: Demonstrate Polymorphism**
1. Create a base class `Appliance` with a virtual method `TurnOn()`.
2. Create two derived classes `WashingMachine` and `Refrigerator` that override the `TurnOn()` method.
3. In your `Main()` method, use polymorphism to call `TurnOn()` on both objects.

---

Congratulations! You’ve completed Day 2 of your self-paced C# learning journey. Keep practicing to strengthen your understanding of Object-Oriented Programming concepts.

