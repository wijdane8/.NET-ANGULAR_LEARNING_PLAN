# **Self-Learning Guide: Day 1 - Introduction to C#**

Welcome to your self-paced journey to learn C#! This guide will walk you through essential concepts in a structured way. Follow the instructions step-by-step to grasp the basics of C# and apply what you learn through practical tasks and coding exercises. Let's get started!

---

## **🧩 1: Understand the .NET Platform**
### **What is .NET?**
.NET is a development framework created by Microsoft. It allows developers to build various types of applications like web, desktop, mobile, cloud, and IoT applications.

1️⃣ **Key Concepts:**
- **Cross-platform:** You can run .NET applications on Windows, macOS, and Linux.
- **Multi-language support:** You can write code in C#, F#, or VB.NET.
- **Unified Development:** .NET includes tools and libraries for web development (ASP.NET), desktop apps (WPF), mobile apps (Xamarin), and more.

📝 **Task:**
- Take a moment to explore the official .NET documentation [here](https://docs.microsoft.com/en-us/dotnet/).
- Write down in your own words what .NET is and list three types of applications you can build using it.

---

## **🧩 2: Learn the Basic Syntax of C#**
### **Structure of a C# Program**
1️⃣ **Write your first C# program:**
Follow these steps to create your first program:

1. Open **Visual Studio** or **Visual Studio Code**.
2. Create a new console project by selecting **File > New > Project**.
3. Write the following code:

```csharp
using System;

namespace HelloWorldApp
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello, World!");
        }
    }
}
```

4. Run your program by pressing **F5** or **Ctrl + F5**.

💡 **Explanation:**
- `using System;` – Provides basic functionalities like reading input and displaying output.
- `namespace` – A way to group related classes.
- `class` – The blueprint for creating objects.
- `Main` – The entry point of your application.

---

## **🧩 3: Variables, Data Types, and Operators**
### **What are Variables?**
Variables are containers used to store data in a program. Every variable in C# must have a data type.

🛠 **Common Data Types:**
| Data Type   | Description          | Example         |
|-------------|----------------------|-----------------|
| `int`       | Integer numbers      | `int age = 25;` |
| `double`    | Decimal numbers      | `double price = 99.99;` |
| `string`    | Text                 | `string name = "John";` |
| `bool`      | Boolean values       | `bool isActive = true;` |

💡 **Exercise:**
1. Declare a variable for your name, age, and whether you are a student.
2. Print these variables to the console using `Console.WriteLine()`.

---

## **🧩 4: Control Flow (If Statements, Loops)**
### **If-Else Statement**
Control the flow of your program based on conditions.

🔧 **Example:**
```csharp
int number = 10;
if (number > 0)
{
    Console.WriteLine("Positive number");
}
else
{
    Console.WriteLine("Negative number");
}
```

💡 **Task:**
1. Write a program that checks if a number is positive, negative, or zero.

---

## **🧩 5: Functions and Methods**
### **What are Functions?**
Functions (or methods) are blocks of code that perform a specific task. They can take input, process it, and return a result.

🔧 **Example:**
```csharp
static int AddNumbers(int a, int b)
{
    return a + b;
}

static void Main(string[] args)
{
    int result = AddNumbers(5, 3);
    Console.WriteLine("Result: " + result);
}
```

💡 **Exercise:**
1. Create a function to multiply two numbers.
2. Call the function in `Main()` and display the result.

---

## **🧩 6: Practical Labs**

### **Lab 1: Personalized Message Application**
**Goal:** Create a console application that:
- Takes the user's name and age as input.
- Displays a personalized message.

🔧 **Steps:**
1. Create a new console project.
2. Use `Console.ReadLine()` to take input from the user.
3. Display a message like "Hello, John! You are 25 years old."

### **Lab 2: Simple Calculator Application**
**Goal:** Create a calculator that performs basic arithmetic operations.

🔧 **Steps:**
1. Create a new console project.
2. Use `Console.ReadLine()` to take two numbers as input.
3. Use a switch statement to perform addition, subtraction, multiplication, or division based on the user's choice.

### **Lab 3: Library Management System**
**Goal:** Create a library management system to:
- Add books to the library.
- Borrow books from the library.
- Return books to the library.

🔧 **Steps:**
1. Create a list to store available books.
2. Create another list to store borrowed books.
3. Use a loop to display a menu and perform actions based on the user's choice.

**Sample Code:**
```csharp
using System;
using System.Collections.Generic;

namespace LibraryManagementSystem
{
    class Program
    {
        static List<string> books = new List<string>();
        static List<string> borrowedBooks = new List<string>();

        static void Main(string[] args)
        {
            while (true)
            {
                Console.WriteLine("\nLibrary Management System");
                Console.WriteLine("1. Add Book");
                Console.WriteLine("2. Borrow Book");
                Console.WriteLine("3. Return Book");
                Console.WriteLine("4. Exit");
                Console.Write("Choose an option: ");

                int choice = int.Parse(Console.ReadLine());
                switch (choice)
                {
                    case 1:
                        AddBook();
                        break;
                    case 2:
                        BorrowBook();
                        break;
                    case 3:
                        ReturnBook();
                        break;
                    case 4:
                        return;
                    default:
                        Console.WriteLine("Invalid choice.");
                        break;
                }
            }
        }

        static void AddBook()
        {
            Console.Write("Enter book name: ");
            string book = Console.ReadLine();
            books.Add(book);
            Console.WriteLine($"'{book}' has been added to the library.");
        }

        static void BorrowBook()
        {
            Console.Write("Enter book name to borrow: ");
            string book = Console.ReadLine();
            if (books.Contains(book))
            {
                books.Remove(book);
                borrowedBooks.Add(book);
                Console.WriteLine($"You have borrowed '{book}'.");
            }
            else
            {
                Console.WriteLine("Book not available.");
            }
        }

        static void ReturnBook()
        {
            Console.Write("Enter book name to return: ");
            string book = Console.ReadLine();
            if (borrowedBooks.Contains(book))
            {
                borrowedBooks.Remove(book);
                books.Add(book);
                Console.WriteLine($"'{book}' has been returned to the library.");
            }
            else
            {
                Console.WriteLine("You haven't borrowed this book.");
            }
        }
    }
}
```

---

Congratulations! You’ve completed Day 1 of your self-paced C# learning journey. Keep practicing and exploring new concepts to solidify your understanding.

