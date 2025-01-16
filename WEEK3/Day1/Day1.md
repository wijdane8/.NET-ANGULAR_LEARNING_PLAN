# **.NET & Angular Guide: Week 3 - Backend API Development**

## **🧩 Day 11: REST APIs with ASP.NET Core**

Welcome to Day 11! Today, you’ll learn how to build **REST APIs** using ASP.NET Core. RESTful APIs are the backbone of modern web applications, enabling seamless communication between the frontend and backend. By the end of this guide, you’ll have created an API for managing users and tested it using Postman.

---

## **🧩 What is a RESTful API?**
A RESTful API follows the principles of **Representational State Transfer (REST)**, a design architecture for building scalable web services.

### **Key Principles of REST:**
1. **Stateless:** Each request contains all the information needed for processing.
2. **Resource-Based:** API endpoints represent resources (e.g., `/users`).
3. **HTTP Methods:**
   - **GET:** Retrieve resources.
   - **POST:** Create new resources.
   - **PUT:** Update existing resources.
   - **DELETE:** Delete resources.

---

## **🧩 Steps to Build a REST API**

1️⃣ **Step 1: Create a New ASP.NET Core Web API Project**
- Open **Visual Studio**.
- Select **File > New > Project**.
- Choose **ASP.NET Core Web API**.
- Name your project (e.g., `UserApi`) and click **Create**.

2️⃣ **Step 2: Define the User Model**
- In the **Models** folder, create a new class called `User`:

```csharp
public class User
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string Email { get; set; }
}
```

3️⃣ **Step 3: Set Up the DbContext**
- In the **Data** folder, create a new class called `ApplicationDbContext`:

```csharp
using Microsoft.EntityFrameworkCore;

public class ApplicationDbContext : DbContext
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options) : base(options) { }

    public DbSet<User> Users { get; set; }
}
```

4️⃣ **Step 4: Configure the Database Connection**
- In the `appsettings.json` file, add a connection string:

```json
"ConnectionStrings": {
    "DefaultConnection": "Server=(localdb)\\mssqllocaldb;Database=UserApi;Trusted_Connection=True;"
}
```

- In the `Program.cs` file, add the DbContext to the service container:

```csharp
builder.Services.AddDbContext<ApplicationDbContext>(options =>
    options.UseSqlServer(builder.Configuration.GetConnectionString("DefaultConnection")));
```

5️⃣ **Step 5: Create the Users Controller**
- In the **Controllers** folder, create a new controller called `UsersController`:

```csharp
using Microsoft.AspNetCore.Mvc;
using System.Collections.Generic;
using System.Linq;
using UserApi.Models;

[ApiController]
[Route("api/[controller]")]
public class UsersController : ControllerBase
{
    private readonly ApplicationDbContext _context;

    public UsersController(ApplicationDbContext context)
    {
        _context = context;
    }

    // GET: api/users
    [HttpGet]
    public ActionResult<IEnumerable<User>> GetUsers()
    {
        return _context.Users.ToList();
    }

    // GET: api/users/5
    [HttpGet("{id}")]
    public ActionResult<User> GetUser(int id)
    {
        var user = _context.Users.Find(id);

        if (user == null)
        {
            return NotFound();
        }

        return user;
    }

    // POST: api/users
    [HttpPost]
    public ActionResult<User> PostUser(User user)
    {
        _context.Users.Add(user);
        _context.SaveChanges();

        return CreatedAtAction(nameof(GetUser), new { id = user.Id }, user);
    }

    // PUT: api/users/5
    [HttpPut("{id}")]
    public IActionResult PutUser(int id, User user)
    {
        if (id != user.Id)
        {
            return BadRequest();
        }

        _context.Entry(user).State = EntityState.Modified;
        _context.SaveChanges();

        return NoContent();
    }

    // DELETE: api/users/5
    [HttpDelete("{id}")]
    public IActionResult DeleteUser(int id)
    {
        var user = _context.Users.Find(id);
        if (user == null)
        {
            return NotFound();
        }

        _context.Users.Remove(user);
        _context.SaveChanges();

        return NoContent();
    }
}
```

6️⃣ **Step 6: Test the API Using Postman**
- Use **Postman** to test the following endpoints:
  - **GET:** `/api/users` to retrieve all users.
  - **GET:** `/api/users/{id}` to retrieve a specific user by ID.
  - **POST:** `/api/users` to create a new user.
  - **PUT:** `/api/users/{id}` to update an existing user.
  - **DELETE:** `/api/users/{id}` to delete a user.

---

## **🧩 Practical Labs**

### **Lab 1: Create a CRUD API for Users**
**Goal:** Build an API to manage user data.

🔧 **Tasks:**
1. Define a `User` model.
2. Set up a `DbContext` for database operations.
3. Create a `UsersController` with CRUD endpoints.
4. Test the API using Postman.

### **Lab 2: Enhance the API**
**Goal:** Add additional features to the API.

🔧 **Tasks:**
1. Implement input validation for user data.
2. Add error handling for invalid requests.
3. Implement sorting and filtering for the GET endpoint.

---

Congratulations on completing Day 11! Tomorrow, you’ll learn about securing your API using JWT authentication.

