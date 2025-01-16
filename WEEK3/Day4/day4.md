# **.NET & Angular Guide: Week 3 - Backend API Development**

## **🧩 Day 14: Advanced API Features**

Welcome to Day 14! Today, you’ll explore **advanced API features** such as pagination, filtering, and unit testing. These features are crucial for building robust and user-friendly APIs.

---

## **🧩 Pagination and Filtering**
Pagination and filtering are essential for managing large datasets efficiently and providing a better user experience.

### **Adding Pagination**
1️⃣ **Modify the `CustomersController` to Include Pagination**

```csharp
[HttpGet]
public ActionResult<IEnumerable<Customer>> GetCustomers([FromQuery] int page = 1, [FromQuery] int pageSize = 10)
{
    var customers = _context.Customers
        .Skip((page - 1) * pageSize)
        .Take(pageSize)
        .ToList();

    return customers;
}
```

💡 **Explanation:**
- Use `Skip` to bypass records from previous pages.
- Use `Take` to limit the number of records retrieved.

### **Adding Filtering**
2️⃣ **Filter Customers by Name**

```csharp
[HttpGet("search")]
public ActionResult<IEnumerable<Customer>> SearchCustomers([FromQuery] string name)
{
    var customers = _context.Customers
        .Where(c => c.Name.Contains(name))
        .ToList();

    return customers;
}
```

💡 **Explanation:**
- Use LINQ’s `Where` method to filter results based on the `name` query parameter.

---

## **🧩 Error Handling**
Error handling ensures that your API responds gracefully to unexpected situations.

### **Global Error Handling**
1️⃣ **Add Middleware for Global Error Handling**

```csharp
app.UseExceptionHandler(errorApp =>
{
    errorApp.Run(async context =>
    {
        context.Response.StatusCode = 500;
        await context.Response.WriteAsync("An unexpected error occurred.");
    });
});
```

---

## **🧩 Unit Testing with xUnit and Moq**
Unit testing ensures the reliability of your API by verifying individual components.

### **Setting Up Unit Testing**
1️⃣ **Install Testing Packages**
- Open the **Package Manager Console** and run:
```bash
Install-Package xunit
Install-Package Moq
```

2️⃣ **Write a Unit Test for the Controller**

```csharp
using Moq;
using Xunit;
using Microsoft.AspNetCore.Mvc;

public class CustomersControllerTests
{
    [Fact]
    public void GetCustomers_ReturnsListOfCustomers()
    {
        // Arrange
        var mockContext = new Mock<ApplicationDbContext>();
        var controller = new CustomersController(mockContext.Object);

        // Act
        var result = controller.GetCustomers();

        // Assert
        Assert.IsType<ActionResult<IEnumerable<Customer>>>(result);
    }
}
```

💡 **Explanation:**
- Use `Moq` to mock the `ApplicationDbContext`.
- Use `xUnit` to define and run tests.

---

## **🧩 Practical Labs**

### **Lab 1: Add Pagination and Filtering**
**Goal:** Implement pagination and filtering in your API.

🔧 **Tasks:**
1. Modify the `GetCustomers` endpoint to include pagination.
2. Add a search endpoint for filtering by name.

### **Lab 2: Write Unit Tests for Your API**
**Goal:** Ensure the reliability of your API with unit tests.

🔧 **Tasks:**
1. Set up a test project using `xUnit`.
2. Write unit tests for the `CustomersController`.
3. Use `Moq` to mock dependencies.

---

Congratulations on completing Day 14! Tomorrow, you’ll review Week 3 concepts and complete a set of exercises to reinforce your learning.

