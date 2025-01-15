# .NET and Angular Self-Learning Plan: Week 1-12 - Comprehensive Guide 

## **Weeks 1-2: Setting Foundations**

### **Week 1: .NET Foundations**

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

## **Weeks 3-4: Backend API Development**

### **Week 3: Building Secure APIs**

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

### **Week 4: Database Integration with Entity Framework**

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

## **Weeks 5-6: Angular Frontend Development**

### **Week 5: Angular Routing and Forms**

#### **Day 1: Routing in Angular**
- **Topics Covered:**
  - Setting up routes
  - Navigating between pages

**Lab:**
1. Create a multi-page Angular app with Home, Products, and About pages.

#### **Day 2: Forms in Angular**
- **Topics Covered:**
  - Template-driven and reactive forms
  - Form validation

**Lab:**
1. Create a form for adding new products.
2. Validate the form inputs.

### **Week 6: HTTP Client and State Management**

#### **Day 3: Making HTTP Requests**
- **Topics Covered:**
  - Using HttpClient to fetch data
  - Error handling for HTTP requests

**Lab:**
1. Fetch product data from your API and display it in your Angular app.

#### **Day 4: State Management**
- **Topics Covered:**
  - Using services to manage state
  - Sharing data between components

**Lab:**
1. Create a shopping cart feature that uses a service to manage state.
2. **Include UI/UX best practices:**
   - Use Angular Material for UI components.
   - Ensure the application is responsive and mobile-first.

---

## **Weeks 7-8: Full Stack Integration**

### **Project: Task Management System or Expense Tracker**
- **Goal:**
  - Build a full-stack application that includes a .NET Core API and an Angular frontend.
  - Implement user authentication, CRUD operations, and form validation.

**Lab:**
1. Set up the backend API.
2. Connect the Angular frontend to the API.
3. Implement a complete workflow for managing tasks or expenses.

---

## **Weeks 9-10: Advanced Topics**

### **Week 9: .NET Advanced Topics**

#### **Day 1: Dependency Injection**
- **Topics Covered:**
  - What is Dependency Injection?
  - Implementing DI in ASP.NET Core

**Lab:**
1. Refactor your API to use Dependency Injection.

#### **Day 2: Middleware and SignalR**
- **Topics Covered:**
  - Creating custom middleware
  - Real-time communication with SignalR

**Lab:**
1. Implement a chat feature using SignalR.

### **Week 10: Angular Advanced Topics**

#### **Day 3: Advanced RxJS**
- **Topics Covered:**
  - Observables and operators

**Lab:**
1. Use RxJS to handle complex data streams.

#### **Day 4: Lazy Loading and Custom Directives**
- **Topics Covered:**
  - Optimizing performance with lazy loading
  - Creating custom directives

**Lab:**
1. Implement lazy loading in your Angular app.
2. Create a custom directive for input validation.

---

## **Weeks 11-12: DevOps & Deployment**

### **Week 11: Dockerizing Applications and Kubernetes Basics**

#### **Day 1: Docker Basics**
- **Topics Covered:**
  - Creating Dockerfiles
  - Building and running Docker containers

**Lab:**
1. Dockerize your .NET API.
2. Dockerize your Angular app.

#### **Day 2: Introduction to Kubernetes**
- **Topics Covered:**
  - What is Kubernetes?
  - Deploying a Dockerized app to a Kubernetes cluster

**Lab:**
1. Deploy your Dockerized app to a Kubernetes cluster.

### **Week 12: CI/CD Pipelines and Final Project Deployment**

#### **Day 3: Setting Up CI/CD**
- **Topics Covered:**
  - Using GitHub Actions
  - Automating builds and deployments

**Lab:**
1. Create a CI/CD pipeline for your project.

#### **Day 4: Final Project Deployment**
- **Topics Covered:**
  - Finalizing and deploying the capstone project

**Lab:**
1. Fully deploy your health care system project.

---

## **Capstone Project Ideas: Health Care System (With Improvements)**

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

