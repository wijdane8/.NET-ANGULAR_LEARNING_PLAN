# **.NET & Angular Guide: Week 3 - Backend API Development**

## **🧩 Day 13: Database Integration with Entity Framework Core**

Welcome to Day 13! Today, you’ll learn how to connect your ASP.NET Core API to a database using **Entity Framework Core (EF Core)**. By the end of this guide, you’ll know how to perform CRUD operations with a database.

---

## **🧩 What is Entity Framework Core?**
Entity Framework Core (EF Core) is an Object-Relational Mapping (ORM) tool that allows developers to work with databases using C# code instead of SQL queries.

💡 **Key Features:**
- **Cross-platform:** Works on Windows, macOS, and Linux.
- **Code-First Approach:** Create databases directly from your C# classes.
- **Database-First Approach:** Generate C# classes from an existing database.
- **LINQ Support:** Write database queries using LINQ.

---

## **🧩 Steps to Integrate a Database**

1️⃣ **Step 1: Add the EF Core Package**
- Open the **Package Manager Console** in Visual Studio and run:
```bash
Install-Package Microsoft.EntityFrameworkCore.SqlServer
Install-Package Microsoft.EntityFrameworkCore.Tools
```

2️⃣ **Step 2: Configure the Database Connection**
- In the `appsettings.json` file, add a connection string:
```json
"ConnectionStrings": {
    "DefaultConnection": "Server=(localdb)\\mssqllocaldb;Database=MyApiDb;Trusted_Connection=True;"
}
```

- In the `Program.cs` file, add the DbContext to the service container:
```csharp
builder.Services.AddDbContext<ApplicationDbContext>(options =>
    options.UseSqlServer(builder.Configuration.GetConnectionString("DefaultConnection")));
```

3️⃣ **Step 3: Create a DbContext**
- Add a new class called `ApplicationDbContext`:
```csharp
using Microsoft.EntityFrameworkCore;

public class ApplicationDbContext : DbContext
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options) : base(options) { }

    public DbSet<Customer> Customers { get; set; }
}
```

4️⃣ **Step 4: Create a Model**
- Add a new class called `Customer` in the **Models** folder:
```csharp
public class Customer
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string Email { get; set; }
}
```

5️⃣ **Step 5: Add and Apply Migrations**
- Add a migration to create the database schema:
```bash
Add-Migration InitialCreate
```

- Apply the migration to the database:
```bash
Update-Database
```

6️⃣ **Step 6: Create a Controller**
- Add a new controller called `CustomersController`:
```csharp
using Microsoft.AspNetCore.Mvc;
using System.Collections.Generic;
using System.Linq;

[ApiController]
[Route("api/[controller]")]
public class CustomersController : ControllerBase
{
    private readonly ApplicationDbContext _context;

    public CustomersController(ApplicationDbContext context)
    {
        _context = context;
    }

    [HttpGet]
    public ActionResult<IEnumerable<Customer>> GetCustomers()
    {
        return _context.Customers.ToList();
    }

    [HttpPost]
    public IActionResult AddCustomer(Customer customer)
    {
        _context.Customers.Add(customer);
        _context.SaveChanges();
        return Ok(customer);
    }
}
```

---

## **🧩 Practical Labs**

### **Lab 1: Set Up a Database**
**Goal:** Configure your ASP.NET Core project to connect to a database using EF Core.

🔧 **Tasks:**
1. Add EF Core packages.
2. Configure the connection string.
3. Create a `Customer` model and DbContext.

### **Lab 2: Perform CRUD Operations**
**Goal:** Build a controller to perform CRUD operations on the `Customer` table.

🔧 **Tasks:**
1. Create a `CustomersController`.
2. Implement endpoints for retrieving and adding customers.
3. Test the endpoints using Postman.

---

Congratulations on completing Day 13! Tomorrow, you’ll learn about advanced API features like pagination and unit testing.
