# **.NET & Angular Guide: Week 2 - Advanced ASP.NET Core and API Development**

## **🧩 Day 10: Revision and Exercises**

Welcome to Day 10! Today, you’ll take some time to review the key concepts you’ve learned in Week 2 and complete a set of exercises to reinforce your understanding. This revision day will help ensure that you’re confident in implementing secure, scalable APIs using ASP.NET Core.

---

## **🧩 Quick Recap of Week 2**

Here’s a summary of the topics covered in Week 2:

### **Day 6: Building a Basic CRUD API**
- Created a simple CRUD API using ASP.NET Core.
- Defined models, set up a `DbContext`, and created a controller.
- Used Postman to test API endpoints.

💡 **Key Takeaway:** CRUD operations are essential for managing data in any web application.

### **Day 7: Securing Your API with JWT Authentication**
- Implemented token-based authentication using JWT.
- Created a `TokenService` to generate tokens.
- Secured API endpoints using the `[Authorize]` attribute.

💡 **Key Takeaway:** JWT authentication provides a stateless, secure way to authenticate users.

### **Day 8: Role-Based Authorization**
- Assigned roles to users (e.g., Admin, User).
- Protected endpoints using role-based authorization.

💡 **Key Takeaway:** Role-based authorization allows you to control access based on user roles.

### **Day 9: Claims-Based Authorization**
- Added custom claims to tokens.
- Implemented claims-based authorization policies.
- Protected endpoints using custom policies.

💡 **Key Takeaway:** Claims-based authorization provides more granular control over access.

---

## **🧩 Revision Exercises**
Let’s put your knowledge to the test with these exercises. Try to complete each task without looking at the solutions right away.

### **Exercise 1: Build a Secure CRUD API**
**Task:**
1. Create a secure CRUD API for managing a list of books.
2. Implement JWT authentication to protect the API.
3. Use role-based authorization to control access:
   - Admin can add, update, and delete books.
   - User can only view books.

🔧 **Hints:**
- Use `TokenService` to generate JWT tokens.
- Use `[Authorize(Roles = "Admin")]` to protect admin endpoints.

### **Exercise 2: Add Claims-Based Authorization**
**Task:**
1. Modify your CRUD API to use claims-based authorization.
2. Add a custom claim `CanEditBooks`.
3. Protect the `EditBook` endpoint with a custom policy that requires the `CanEditBooks` claim.

🔧 **Hints:**
- Use `policy.RequireClaim("CanEditBooks", "true")` to create a custom policy.

### **Exercise 3: Test Your API with Postman**
**Task:**
1. Use Postman to test your secure API.
2. Log in as both an Admin and a User.
3. Attempt to access the protected endpoints with each token.

🔧 **Hints:**
- Use the **Authorization** tab in Postman to send the JWT token in the request header.

---

## **🧩 Bonus Challenge: Build a Role-Based and Claims-Based API**
**Task:**
1. Create an API for managing tasks with the following features:
   - Admin can manage all tasks.
   - Users can only manage their own tasks.
2. Use a combination of role-based and claims-based authorization to control access.

🔧 **Steps:**
1. Assign roles (Admin, User) during login.
2. Add claims to control task ownership.
3. Protect endpoints using both roles and claims.

---

## **🧩 Reflection Questions**
Take a moment to reflect on your learning progress.

1. What was the most challenging topic for you in Week 2?
2. What did you enjoy the most?
3. Are there any concepts you feel you need to review?
4. How can you apply what you’ve learned to real-world projects?

💡 **Tip:**
Use your answers to these questions to guide your next steps in learning.

---

Congratulations on completing Day 10! You’ve solidified your understanding of secure API development with ASP.NET Core. In the next session, you’ll begin integrating your backend API with an Angular frontend to build a full-stack application.

