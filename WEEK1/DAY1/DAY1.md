# **.NET and Angular Guide: Day 1 - Introduction to C#**

Welcome to your self-paced journey to learn C#! This guide will walk you through essential concepts in a structured way. Follow the instructions step-by-step to grasp the basics of C# and apply what you learn through practical tasks and coding exercises. Let’s get started!

---

## **🧺 1: Understand the .NET Platform**

### **What is .NET?**
.NET is a development framework created by Microsoft. It allows developers to build various types of applications like web, desktop, mobile, cloud, and IoT applications.

1⃣ **Key Concepts:**

- **Cross-platform:** .NET applications can run on Windows, macOS, and Linux.
- **Multi-language support:** Write code in C#, F#, or VB.NET.
- **Unified Development:** Includes tools and libraries for web development (ASP.NET), desktop apps (WPF), mobile apps (Xamarin), and more.

2⃣ **Components of .NET:**

- **.NET Runtime:** The environment for running applications.
- **ASP.NET:** Framework for building web applications and APIs.
- **Entity Framework:** An ORM for database interaction.
- **Xamarin:** For building cross-platform mobile applications.

3⃣ **Ecosystem Highlights:**

- **NuGet:** Package manager for .NET libraries.
- **Visual Studio:** An integrated development environment (IDE) for .NET development.
- **CLI (Command Line Interface):** Tools for managing .NET applications through terminal commands.

### **🖋 Task:**
- Explore the official .NET documentation [here](https://docs.microsoft.com/en-us/dotnet/).
- Write in your own words what .NET is and list three types of applications you can build using it.

---

## **🧺 2: Learn the Basic Syntax of C#**

### **Structure of a C# Program**

1⃣ **Write Your First C# Program**

Follow these steps:

1. Open **Visual Studio** or **Visual Studio Code**.
2. Create a new console project:
   - In Visual Studio: **File > New > Project** > **Console App**.
   - In Visual Studio Code: Use the terminal command: `dotnet new console`.
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

4. Run your program:
   - In Visual Studio: Press **F5** or **Ctrl + F5**.
   - In Visual Studio Code: Use the terminal command: `dotnet run`.

### **💡 Explanation:**

- `using System;`: Provides basic functionalities like reading input and displaying output.
- `namespace`: A way to group related classes.
- `class`: The blueprint for creating objects.
- `Main`: The entry point of your application.

### **Best Practices and Tips for Clean Code:**
- Always use meaningful names for classes, methods, and variables.
- Keep methods small and focused on a single task.
- Add comments where necessary but avoid over-commenting obvious code.
- Use proper indentation and spacing for better readability.

---

## **🧺 3: Variables, Data Types, and Operators**

### **What are Variables?**
Variables are containers used to store data in a program. Every variable in C# must have a data type.

### **How to Declare Variables in C#**

```csharp
int age = 25; // Declares an integer variable
string name = "John"; // Declares a string variable
bool isStudent = true; // Declares a boolean variable
```

### **🔧 Common Data Types**

| Data Type   | Description          | Example              |
|-------------|----------------------|----------------------|
| `int`       | Integer numbers      | `int age = 25;`      |
| `double`    | Decimal numbers      | `double price = 99.99;` |
| `string`    | Text                 | `string name = "John";` |
| `bool`      | Boolean values       | `bool isActive = true;` |
| `char`      | Single character     | `char grade = 'A';`  |

### **Features of Variables**
- **Scope:** Variables can be local, global, or static based on their declaration.
- **Type Safety:** C# enforces type safety to ensure variables hold only specified types of data.
- **Initialization:** Always initialize variables before use to avoid errors.

### **💡 Operators in C#: Basics**

| Operator Type  | Examples          | Description                 |
|----------------|-------------------|-----------------------------|
| Arithmetic     | `+`, `-`, `*`, `/` | Perform mathematical calculations. |
| Comparison     | `==`, `!=`, `>`, `<` | Compare values.            |
| Logical        | `&&`, `||`, `!`   | Combine or negate conditions. |

### **Text Formatting and Concatenation in C#:**

#### **String Concatenation:**
Combining multiple strings into one.

```csharp
string firstName = "John";
string lastName = "Doe";
string fullName = firstName + " " + lastName;
Console.WriteLine("Full Name: " + fullName);
```

#### **String Interpolation:**
Simpler and more readable than concatenation.

```csharp
string name = "Alice";
int age = 30;
Console.WriteLine($"Name: {name}, Age: {age}");
```

#### **String Formatting:**
Customizes the appearance of output.

```csharp
double price = 29.99;
Console.WriteLine("Price: {0:C}", price); // Displays as currency
```

### **Best Practices:**
- Use string interpolation (`$""`) over concatenation for better readability.
- Avoid excessive use of string concatenation in loops to improve performance.
- Use `StringBuilder` for dynamic and frequent string modifications.

### **🖋 Exercise:**
1. Declare variables for first name, last name, and age.
2. Print a formatted sentence using both string concatenation and interpolation.

---

## **🧺 4: Data Structures (Lists, Arrays)**

### **Arrays in C#:**
Arrays are fixed-size collections that hold elements of the same data type.

#### **How to Declare and Initialize Arrays:**

```csharp
int[] numbers = {1, 2, 3, 4, 5}; // Array of integers
string[] names = new string[3]; // Array of strings with size 3
names[0] = "Alice";
names[1] = "Bob";
names[2] = "Charlie";
```

#### **Accessing Array Elements:**

```csharp
Console.WriteLine(numbers[0]); // Access the first element
numbers[1] = 10; // Modify the second element
```

### **Lists in C#:**
Lists are dynamic collections that can grow or shrink in size and hold elements of the same data type.

#### **How to Declare and Initialize Lists:**

```csharp
using System.Collections.Generic;

List<int> numbers = new List<int>();
numbers.Add(1); // Add elements to the list
numbers.Add(2);
numbers.Add(3);
```

#### **Accessing and Modifying Lists:**

```csharp
Console.WriteLine(numbers[0]); // Access the first element
numbers[1] = 10; // Modify the second element
numbers.Remove(3); // Remove an element
```

#### **Iterating Through Lists and Arrays:**

```csharp
// Using a for loop with an array
for (int i = 0; i < numbers.Length; i++)
{
    Console.WriteLine(numbers[i]);
}

// Using a foreach loop with a list
foreach (int number in numbers)
{
    Console.WriteLine(number);
}
```

### **Differences Between Arrays and Lists:**

| Feature        | Array                         | List                        |
|----------------|-------------------------------|-----------------------------|
| Size           | Fixed                         | Dynamic                     |
| Performance    | Faster for fixed-size data    | Slower but flexible         |
| Methods        | No built-in methods for manipulation | Rich set of methods like Add, Remove, etc. |

### **Built-in Functions for Data Structures**

#### **Array Functions:**

- **`Array.Sort()`**: Sorts the elements of an array.
  ```csharp
  int[] numbers = {3, 1, 4, 1, 5};
  Array.Sort(numbers);
  ```

- **`Array.Reverse()`**: Reverses the order of elements in an array.
  ```csharp
  Array.Reverse(numbers);
  ```

- **`Array.IndexOf()`**: Finds the index of a specific value.
  ```csharp
  int index = Array.IndexOf(numbers, 4);
  ```

#### **List Functions:**

- **`Add()`**: Adds an element to the list.
  ```csharp
  numbers.Add(6);
  ```

- **`Remove()`**: Removes the first occurrence of a specific element.
  ```csharp
  numbers.Remove(4);
  ```

- **`Contains()`**: Checks if an element exists in the list.
  ```csharp
  bool exists = numbers.Contains(3);
  ```

- **`Count`**: Gets the number of elements in the list.
  ```csharp
  int count = numbers.Count;
  ```

### **Best Practices for Data Structures:**
- Use arrays for fixed-size collections and performance-critical tasks.
- Use lists when you need a dynamic collection with rich functionalities.
- Prefer strongly-typed collections (`List<int>`) to avoid runtime errors.

### **🖋 Task:**
1. Create an array to store 5 integers and print their sum.
2. Create a list to store names of 3 people. Add two more names and print all names.
3. Use `Array.Sort()` and `Array.Reverse()` on an integer array and print the results.

---

## **🧺 5: Control Flow (If Statements, Switch, Loops)**

### **If-Else Statement**
Control the flow of your program based on conditions.

🔧 **Example:**

```csharp
int number = 10;
if (number > 0)
{
    Console.WriteLine("Positive number");
}
else if (number < 0)
{
    Console.WriteLine("Negative number");
}
else
{
    Console.WriteLine("Zero");
}
```

### **Switch Statement**
The `switch` statement is used to execute different parts of code based on the value of a variable.

#### **Syntax and Example:**

```csharp
int day = 3;
switch (day)
{
    case 1:
        Console.WriteLine("Monday");
        break;
    case 2:
        Console.WriteLine("Tuesday");
        break;
    case 3:
        Console.WriteLine("Wednesday");
        break;
    case 4:
        Console.WriteLine("Thursday");
        break;
    case 5:
        Console.WriteLine("Friday");
        break;
    case 6:
        Console.WriteLine("Saturday");
        break;
    case 7:
        Console.WriteLine("Sunday");
        break;
    default:
        Console.WriteLine("Invalid day");
        break;
}
```

#### **Key Points:**
- The `case` keyword checks the value of the variable.
- Each `case` ends with a `break;` to prevent fall-through.
- Use the `default` case to handle unexpected values.

### **Loops in C#: Basics**

| Loop Type  | Syntax Example            | Description                     |
|------------|---------------------------|---------------------------------|
| `for`      | `for(int i = 0; i < 5; i++)` | Executes a block a specific number of times. |
| `while`    | `while(condition)`        | Executes while the condition is true. |
| `do-while` | `do { } while(condition)` | Executes at least once, then checks the condition. |

### **Best Practices for Loops:**
- Use meaningful variable names like `counter` instead of `i` for better readability.
- Avoid infinite loops by ensuring the condition is modified within the loop.
- Use `break` and `continue` sparingly to maintain clear logic flow.

### **🖋 Task:**
1. Write a program that checks if a number is positive, negative, or zero.
2. Use a `switch` statement to print the day of the week based on a number input.
3. Use a `for` loop to print numbers from 1 to 10.

---
## **Functions and Methods in C#**

### **Overview**
Functions (also called methods in C#) are blocks of code designed to perform a specific task. They help in reusing code, making programs modular, and improving readability. Functions can accept input (parameters) and return a result or simply perform an action without returning a value.

---

### **Structure of a Function**

```csharp
returnType FunctionName(parameter1Type parameter1Name, parameter2Type parameter2Name)
{
    // Function body
    return value; // (if applicable)
}
```

#### **Example**

```csharp
static int AddNumbers(int a, int b)
{
    return a + b;
}

static void Main(string[] args)
{
    int result = AddNumbers(5, 10);
    Console.WriteLine("The sum is: " + result);
}
```

---

### **Types of Functions**

1. **Functions with Parameters and a Return Value**
   - Accept parameters as input and return a computed result.
   - Example:
   ```csharp
   static int Multiply(int x, int y)
   {
       return x * y;
   }
   ```

2. **Functions with Parameters and No Return Value**
   - Accept parameters but do not return a value. Use `void` as the return type.
   - Example:
   ```csharp
   static void GreetUser(string name)
   {
       Console.WriteLine($"Hello, {name}!");
   }
   ```

3. **Functions without Parameters and a Return Value**
   - Perform a task and return a result without requiring input parameters.
   - Example:
   ```csharp
   static string GetGreeting()
   {
       return "Welcome to C#!";
   }
   ```

4. **Functions without Parameters and No Return Value**
   - Perform a task without requiring input parameters or returning a value.
   - Example:
   ```csharp
   static void DisplayMessage()
   {
       Console.WriteLine("This is a message from the DisplayMessage function.");
   }
   ```

---

### **Key Components of a Function**

| Component      | Description                                           |
|----------------|-------------------------------------------------------|
| **Return Type** | Specifies the type of value the function returns. Use `void` if no value is returned. |
| **Function Name** | A descriptive name that indicates the purpose of the function. |
| **Parameters**  | Input values required by the function, defined within parentheses. |
| **Body**        | The block of code executed when the function is called. |
| **Return Statement** | (Optional) Used to return a value to the calling code. |

---

### **Best Practices for Functions**

- **Keep Functions Small:** Each function should perform one specific task.
- **Use Descriptive Names:** Clearly indicate the function's purpose.
- **Avoid Global Variables:** Pass data using parameters to ensure functions are reusable and testable.
- **Error Handling:** Include error checks and validations where necessary.
- **Use Comments:** Add meaningful comments to explain the logic in complex functions.
- **Avoid Side Effects:** Functions should not change global state unnecessarily.
- **Follow Naming Conventions:** Use PascalCase for function names.

---

### **Common Use Cases of Functions**

#### **Mathematical Calculations**
```csharp
static double CalculateArea(double radius)
{
    const double pi = 3.14159;
    return pi * radius * radius;
}
```

#### **String Manipulation**
```csharp
static string FormatName(string firstName, string lastName)
{
    return $"{firstName} {lastName}".ToUpper();
}
```

#### **Decision Making**
```csharp
static bool IsEven(int number)
{
    return number % 2 == 0;
}
```

#### **Control Flow**
Use functions to encapsulate control flow logic:
```csharp
static void PrintNumberCategory(int number)
{
    if (number > 0)
    {
        Console.WriteLine("Positive number");
    }
    else if (number < 0)
    {
        Console.WriteLine("Negative number");
    }
    else
    {
        Console.WriteLine("Zero");
    }
}
```

---

### **Built-in Methods in C#: Examples and Usage**

#### **String Methods**
| Method           | Description                       | Example                             |
|------------------|-----------------------------------|-------------------------------------|
| `ToUpper()`      | Converts string to uppercase.     | `"hello".ToUpper();`               |
| `ToLower()`      | Converts string to lowercase.     | `"HELLO".ToLower();`               |
| `Contains()`     | Checks if string contains a value.| `"hello".Contains("ll");`         |
| `Substring()`    | Extracts part of a string.        | `"hello".Substring(0, 2);`         |
| `Trim()`         | Removes whitespace.              | `" hello ".Trim();`                |

#### **Math Methods**
| Method        | Description                            | Example              |
|---------------|----------------------------------------|----------------------|
| `Math.Abs()`  | Returns absolute value of a number.    | `Math.Abs(-5);`      |
| `Math.Pow()`  | Raises a number to the power of another.| `Math.Pow(2, 3);`    |
| `Math.Sqrt()` | Calculates the square root of a number.| `Math.Sqrt(16);`     |
| `Math.Max()`  | Returns the larger of two numbers.     | `Math.Max(5, 10);`   |
| `Math.Min()`  | Returns the smaller of two numbers.    | `Math.Min(5, 10);`   |

#### **Array Methods**
| Method            | Description                          | Example                      |
|-------------------|--------------------------------------|------------------------------|
| `Sort()`          | Sorts the elements in ascending order.| `Array.Sort(numbers);`      |
| `Reverse()`       | Reverses the order of elements.       | `Array.Reverse(numbers);`   |
| `IndexOf()`       | Finds the index of a value.          | `Array.IndexOf(numbers, 3);`|

---

### **Exercise**

1. Write a function `CalculateSum` that accepts an array of integers and returns the sum of its elements.
2. Create a function `IsPrime` to check if a number is prime. The function should return `true` if the number is prime, and `false` otherwise.
3. Implement a function `ReverseString` that takes a string as input and returns the reversed string.
4. Write a function `GetDayOfWeek` that accepts an integer (1-7) and returns the corresponding day of the week.

---

### **Conclusion**

Functions are the backbone of modular programming in C#. Mastering them will significantly enhance your ability to write clean, reusable, and efficient code. Keep practicing different types of functions and experiment with their use in various scenarios.


---

## **🧺 7: Practical Labs**

### **Lab 1: Personalized Message Application**

**Goal:** Create a console application that:
- Takes the user’s name and age as input.
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
3. Use a switch statement to perform addition, subtraction, multiplication, or division based on the user’s choice.

#### **Improved Example Code:**

```csharp
using System;

namespace SimpleCalculator
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Enter the first number:");
            double num1 = Convert.ToDouble(Console.ReadLine());

            Console.WriteLine("Enter the second number:");
            double num2 = Convert.ToDouble(Console.ReadLine());

            Console.WriteLine("Choose an operation: 1.Add 2.Subtract 3.Multiply 4.Divide");
            int choice = Convert.ToInt32(Console.ReadLine());

            switch (choice)
            {
                case 1:
                    Console.WriteLine($"Result: {Add(num1, num2)}");
                    break;
                case 2:
                    Console.WriteLine($"Result: {Subtract(num1, num2)}");
                    break;
                case 3:
                    Console.WriteLine($"Result: {Multiply(num1, num2)}");
                    break;
                case 4:
                    if (num2 != 0)
                        Console.WriteLine($"Result: {Divide(num1, num2)}");
                    else
                        Console.WriteLine("Division by zero is not allowed.");
                    break;
                default:
                    Console.WriteLine("Invalid choice.");
                    break;
            }
        }

        static double Add(double a, double b) => a + b;
        static double Subtract(double a, double b) => a - b;
        static double Multiply(double a, double b) => a * b;
        static double Divide(double a, double b) => a / b;
    }
}
```

### **Lab 3: Library Management System**

**Goal:** Create a library management system to:
- Add books to the library.
- Borrow books from the library.
- Return books to the library.

🔧 **Steps:**
1. Create a list to store available books.
2. Create another list to store borrowed books.
3. Use a loop to display a menu and perform actions based on the user’s choice.

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
                        Console.WriteLine("Exiting the Library Management System.");
                        return;
                    default:
                        Console.WriteLine("Invalid choice.");
                        break;
                }
            }
        }

        static void AddBook()
        {
            Console.Write("Enter the name of the book to add: ");
            string book = Console.ReadLine();
            if (!string.IsNullOrWhiteSpace(book))
            {
                books.Add(book);
                Console.WriteLine($"'{book}' has been added to the library.");
            }
            else
            {
                Console.WriteLine("Book name cannot be empty.");
            }
        }

        static void BorrowBook()
        {
            Console.Write("Enter the name of the book to borrow: ");
            string book = Console.ReadLine();
            if (books.Contains(book))
            {
                books.Remove(book);
                borrowedBooks.Add(book);
                Console.WriteLine($"You have borrowed '{book}'.");
            }
            else
            {
                Console.WriteLine("Book not available in the library.");
            }
        }

        static void ReturnBook()
        {
            Console.Write("Enter the name of the book to return: ");
            string book = Console.ReadLine();
            if (borrowedBooks.Contains(book))
            {
                borrowedBooks.Remove(book);
                books.Add(book);
                Console.WriteLine($"'{book}' has been returned to the library.");
            }
            else
            {
                Console.WriteLine("You haven’t borrowed this book.");
            }
        }
    }
}
```

---

### **Additional Notes:**
- Use exception handling (`try-catch`) to handle invalid inputs and unexpected errors.
- Apply modular functions for each operation to enhance readability and maintainability.
- Ensure input validation (e.g., check for empty or null strings).
- Use meaningful messages to guide users throughout the application.

---

Congratulations! You’ve completed Day 1 of your self-paced C# learning journey. Keep practicing and exploring new concepts to solidify your understanding.
