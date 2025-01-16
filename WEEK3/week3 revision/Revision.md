# **.NET & Angular Guide: Week 3 - Backend API Development**

## **🧩 Day 15: Revision and Exercises**

Welcome to Day 15! Today is a dedicated revision day where you’ll consolidate your knowledge of backend API development in ASP.NET Core. By revisiting key concepts and completing targeted exercises, you’ll reinforce your learning and build confidence in applying what you’ve learned.

---

## **🧩 Quick Recap of Week 3**

Here’s a summary of the topics covered in Week 3:

### **Day 11: REST APIs with ASP.NET Core**
- Learned the principles of RESTful APIs.
- Created CRUD endpoints for managing users.
- Tested the API using Postman.

💡 **Key Takeaway:** RESTful APIs are the backbone of web applications, enabling communication between frontend and backend.

### **Day 12: Authentication and Authorization**
- Implemented JWT authentication to secure the API.
- Added role-based authorization to control access to endpoints.
- Tested secure endpoints using Postman.

💡 **Key Takeaway:** Authentication verifies user identity, while authorization determines their permissions.

### **Day 13: Database Integration with Entity Framework Core**
- Connected the API to a database using EF Core.
- Performed CRUD operations on the database.
- Used migrations to create and update the database schema.

💡 **Key Takeaway:** EF Core simplifies database interactions by allowing developers to use C# code instead of SQL queries.

### **Day 14: Advanced API Features**
- Implemented pagination and filtering to manage large datasets.
- Added global error handling for better API reliability.
- Wrote unit tests using xUnit and Moq to ensure code quality.

💡 **Key Takeaway:** Advanced API features and testing improve the robustness and user experience of your application.

---

## **🧩 Revision Exercises**

### **Exercise 1: Build a Secure User Management API**
**Task:**
1. Create a secure API for managing users.
2. Implement JWT authentication and role-based authorization.
3. Add endpoints for creating, retrieving, updating, and deleting users.

🔧 **Hints:**
- Use the `[Authorize]` attribute to secure endpoints.
- Assign roles (Admin, User) during login.

### **Exercise 2: Add Pagination and Filtering**
**Task:**
1. Modify the API to include pagination for the `GetUsers` endpoint.
2. Add a search endpoint to filter users by name or email.

🔧 **Hints:**
- Use LINQ’s `Skip`, `Take`, and `Where` methods.

### **Exercise 3: Write Unit Tests for the API**
**Task:**
1. Write unit tests for the `UsersController`.
2. Mock the `ApplicationDbContext` using Moq.
3. Test the `GetUsers` and `AddUser` endpoints.

🔧 **Hints:**
- Use xUnit for writing and running tests.
- Use `Assert` methods to validate test outcomes.

---

## **🧩 Bonus Challenge: Build a Product Management API**
**Task:**
1. Create an API for managing products.
2. Implement secure endpoints for Admin users.
3. Add features for pagination, filtering, and error handling.

🔧 **Steps:**
1. Define a `Product` model with properties like `Id`, `Name`, and `Price`.
2. Use EF Core to create a database table for products.
3. Secure the API with JWT and role-based authorization.

---

## **🧩 Reflection Questions**
Take a moment to reflect on your learning progress.

1. What was the most challenging topic for you in Week 3?
2. What did you enjoy the most?
3. Are there any concepts you feel you need to review?
4. How can you apply what you’ve learned to real-world projects?

💡 **Tip:**
Use your answers to these questions to guide your next steps in learning.

---

Congratulations on completing Day 15 and wrapping up Week 3! You’ve solidified your understanding of backend API development, including REST principles, authentication, database integration, and testing. In the next week, you’ll start focusing on Angular frontend development.

