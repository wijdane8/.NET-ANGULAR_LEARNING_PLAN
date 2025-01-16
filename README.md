# .NET and Angular Self-Learning Plan: Week 1-12 - Comprehensive Guide 

## **Week 1: Setting Foundations**

### **.NET Foundations**

#### **Day 1: Introduction to C#**
- **Topics Covered:**
  - Introduction to .NET platform
  - Basic syntax of C#
  - Variables, data types, and operators
  - Control flow (if statements, loops)
  - Functions and methods

**Lab:**
1. Write a C# console application that:
   - Takes user input (name, age)
   - Displays a personalized message
2. Create a simple calculator application with basic operations (add, subtract, multiply, divide).
3. **Practical Lab Addition:**
   - Create a library management system console app that includes:
     - Adding books
     - Borrowing books
     - Returning books

#### **Day 2: Object-Oriented Programming (OOP) in C#**
- **Topics Covered:**
  - Classes and objects
  - Properties, fields, and methods
  - Constructors
  - Inheritance and polymorphism

**Lab:**
1. Create a class `Person` with properties `Name`, `Age`, and a method `Introduce()` that prints a message.
2. Extend the `Person` class to create a `Student` class with an additional property `Grade` and override the `Introduce()` method.

#### **Day 3: Setting Up ASP.NET Core Project**
- **Topics Covered:**
  - What is ASP.NET Core?
  - Installing Visual Studio and setting up the environment
  - Creating a new ASP.NET Core web application
  - Understanding the project structure

**Lab:**
1. Create a basic ASP.NET Core web application that displays "Hello, World!" on the home page.
2. Modify the home page to accept a name as input and display a personalized welcome message.

#### **Day 4: Entity Framework Core**
- **Topics Covered:**
  - Introduction to Entity Framework Core
  - Creating a database context and models
  - Performing CRUD operations

**Lab:**
1. Create a model `Product` with properties `Id`, `Name`, and `Price`.
2. Use Entity Framework Core to create a database and perform CRUD operations on the `Product` table.

---

## **Week 2: Backend API Development**

### **Building Secure APIs**

#### **Day 1: REST APIs with ASP.NET Core**
- **Topics Covered:**
  - RESTful API principles
  - Creating endpoints
  - Handling HTTP requests and responses

**Lab:**
1. Build an API with endpoints for managing users.
2. Use Postman to test endpoints.

#### **Day 2: Authentication and Authorization**
- **Topics Covered:**
  - Introduction to JWT (JSON Web Tokens)
  - Securing APIs with authentication
  - Role-based authorization

**Lab:**
1. Implement JWT authentication in your API.
2. Create roles (e.g., Admin, User) and secure endpoints accordingly.

#### **Day 3: Database Connections**
- **Topics Covered:**
  - Connecting ASP.NET Core to SQL Server
  - Using Entity Framework for data operations

**Lab:**
1. Create a `Customer` model and perform CRUD operations.
2. Test your API with SQL Server as the database.

#### **Day 4: Advanced API Features**
- **Topics Covered:**
  - Pagination and filtering
  - Error handling
  - **Unit Testing with xUnit and Moq**

**Lab:**
1. Add pagination to your product API.
2. Implement error handling for invalid requests.
3. **Write unit tests for your CRUD API using xUnit.**
4. Use Moq for mocking dependencies.

---

## **Week 3: Angular Foundations**

### **Day 1: Getting Started with Angular**

**Goals:**
- Understand the basics of Angular.
- Set up the development environment.

**Topics:**
- What is Angular? Benefits and Use Cases.
- Installing Node.js and Angular CLI.
- Creating your first Angular app (`ng new`).
- Project structure overview.

**Exercises:**
1. Set up a new Angular project.
2. Run the app and explore its default setup.
3. Experiment with the Angular CLI commands (`ng serve`, `ng generate`, etc.).

---

### **Day 2: Components and Templates**

**Goals:**
- Learn about Angular components and their role in the framework.
- Work with templates for building the UI.

**Topics:**
- Creating components using Angular CLI.
- Component decorator, metadata, and lifecycle hooks.
- Binding data with `{{}}` and using directives like `*ngIf` and `*ngFor`.

**Exercises:**
1. Create a component for a basic profile card.
2. Use `*ngFor` to display a list of items (e.g., user names).
3. Experiment with conditional rendering using `*ngIf`.

---

### **Day 3: Data Binding and Event Handling**

**Goals:**
- Master the different types of data binding in Angular.
- Handle user interactions through events.

**Topics:**
- Property binding (`[]`) and Event binding (`()`).
- Two-way binding with `[(ngModel)]`.
- Forms and user input handling.

**Exercises:**
1. Build a simple form to collect user information.
2. Use two-way binding for real-time input reflection.
3. Add a button that triggers an event to log user data to the console.

---

### **Day 4: Services and Dependency Injection**

**Goals:**
- Understand how to use services to share data.
- Learn about Angular’s dependency injection system.

**Topics:**
- Creating and using services (`ng generate service`).
- Providing services at different levels (root vs. component-level).
- Using services to share data between components.

**Exercises:**
1. Create a service to manage a list of items (e.g., tasks in a to-do app).
2. Inject the service into two components to display and update the shared data.

---

## **Week 4: Angular Advanced Features**

### **Day 1: Routing and Navigation**

**Goals:**
- Build single-page applications with Angular’s routing module.

**Topics:**
- Setting up routes with `RouterModule`.
- Configuring routes and route parameters.
- Navigating between components using the `<router-outlet>`.

**Exercises:**
1. Create a navigation menu to switch between pages (e.g., Home, About, and Contact).
2. Pass parameters through the URL and retrieve them in the component.
3. Use route guards to control access to certain routes.

---

### **Day 2: HTTP Client and APIs**

**Goals:**
- Learn how to interact with REST APIs using Angular’s HTTP Client.

**Topics:**
- Using `HttpClientModule` to make HTTP requests.
- GET, POST, PUT, and DELETE requests.
- Handling errors with RxJS operators.

**Exercises:**
1. Fetch data from a public API and display it in a list.
2. Create a form to send data to an API.
3. Handle API errors and display appropriate messages to the user.

---

### **Day 3: Advanced Angular Concepts**

**Goals:**
- Dive deeper into Angular’s advanced features.

**Topics:**
- Lazy loading and module splitting.
- Observables and RxJS basics.
- Angular pipes (built-in and custom).

**Exercises:**
1. Implement lazy loading for a large module.
2. Create a custom pipe to format text (e.g., convert to uppercase).
3. Use RxJS to debounce user input in a search bar.

---

### **Day 4: Building a Mini Project**

**Goals:**
- Apply all the learned concepts in a hands-on project.

**Mini Project: Task Manager**
- Create a task manager app with the following features:
  - Add, edit, and delete tasks.
  - Display tasks in a list with filtering options.
  - Use routing for separate views (e.g., All Tasks, Completed Tasks).
  - Store data using a mock backend or local storage.

**Bonus:**
- Deploy the app using Angular CLI’s `ng deploy` to a free hosting service.

---

## **Week 5: Full Stack Integration**

### **Project: Task Management System or Expense Tracker**
- **Goal:**
  - Build a full-stack application that includes a .NET Core API and an Angular frontend.
  - Implement user authentication, CRUD operations, and form validation.

**Lab:**
1. Set up the backend API.
2. Connect the Angular frontend to the API.
3. Implement a complete workflow for managing tasks or expenses.

---

## **Week 6: Advanced Topics**

### **Day 1: Dependency Injection**
- **Topics Covered:**
  - What is Dependency Injection?
  - Implementing DI in ASP.NET Core

**Lab:**
1. Refactor your API to use Dependency Injection.

### **Day 2: Middleware and SignalR**
- **Topics Covered:**
  - Creating custom middleware
  - Real-time communication with SignalR

**Lab:**
1. Implement a chat feature using SignalR.

### **Day 3: Advanced RxJS**
- **Topics Covered:**
  - Observables and operators

**Lab:**
1. Use RxJS to handle complex data streams.

### **Day 4: Lazy Loading and Custom Directives**
- **Topics Covered:**
  - Optimizing performance with lazy loading
  - Creating custom directives

**Lab:**
1. Implement lazy loading in your Angular app.
2. Create a custom directive for input validation.

---

## **Week 7: DevOps & Deployment**

### **Day 1: Docker Basics**
- **Topics Covered:**
  - Creating Dockerfiles
  - Building and running Docker containers

**Lab:**
1. Dockerize your .NET API.
2. Dockerize your Angular app.

### **Day 2: Introduction to Kubernetes**
- **Topics Covered:**
  - What is Kubernetes?
  - Deploying a Dockerized app to a Kubernetes cluster

**Lab:**
1. Deploy your Dockerized app to a Kubernetes cluster.

### **Day 3: Setting Up CI/CD**
- **Topics Covered:**
  - Using GitHub Actions
  - Automating builds and deployments

**Lab:**
1. Create a CI/CD pipeline for your project.

### **Day 4: Final Project Deployment**
- **Topics Covered:**
  - Finalizing and deploying the capstone project

**Lab:**
1. Fully deploy your health care system project.

---

## **Capstone Project Ideas: Health Care System **

1. **Patient Management System:**
   - Add RBAC (Admin, Doctor, Patient) and implement JWT authentication.

2. **Telemedicine Platform:**
   - Integrate WebRTC for real-time video calls and chat using SignalR.

3. **Pharmacy Inventory System:**
   - Implement stock alerts via email notifications using .NET Mail.

4. **Health Monitoring Dashboard:**
   - Build a dashboard with wearable device integration and charting tools.

5. **Hospital Management System:**
   - Multi-user roles, appointment scheduling, billing, and inventory management.

