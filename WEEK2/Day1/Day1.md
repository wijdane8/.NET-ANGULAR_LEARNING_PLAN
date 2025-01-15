# **.NET & Angular Guide: Week 2 - Advanced ASP.NET Core and API Development**

Welcome to Week 2 of your self-paced learning journey! This week, you will build on the foundational knowledge you gained in Week 1 by diving deeper into ASP.NET Core and learning how to create secure, scalable APIs. By the end of this week, you’ll be able to build a fully functional CRUD API and implement authentication using JSON Web Tokens (JWT).

Let’s start with Day 6!

---

## **🧩 Day 6: Building a Basic CRUD API with ASP.NET Core**

Today, you’ll learn how to create a simple API that performs CRUD (Create, Read, Update, Delete) operations using ASP.NET Core.

### **What is an API?**

An API (Application Programming Interface) allows different software applications to communicate with each other. In web development, APIs are often used to enable communication between the frontend and backend.

### **Steps to Create a Basic CRUD API:**

1️⃣ **Step 1: Create a New ASP.NET Core Web API Project**

- Open **Visual Studio**.
- Select **File > New > Project**.
- Choose **ASP.NET Core Web API**.
- Name your project (e.g., `ProductApi`) and click **Create**.

2️⃣ **Step 2: Define the Model**

- In the **Models** folder, create a new class called `Product`:

```csharp
public class Product
{
    public int Id { get; set; }
    public string Name { get; set; }
    public decimal Price { get; set; }
}
```

[3️⃣ ](https://visualstudio.microsoft.com/)**[Step 3: Set Up the DbContext](https://visualstudio.microsoft.com/)**

- In the **Data** folder, create a new class called `ApplicationDbContext`:

```csharp
using Microsoft.EntityFrameworkCore;

public class ApplicationDbContext : DbContext
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options) : base(options) { }

    public DbSet<Product> Products { get; set; }
}
```

4️⃣ **Step 4: Configure the Database Connection**

- In the `appsettings.json` file, add a connection string:

```json
"ConnectionStrings": {
    "DefaultConnection": "Server=(localdb)\\mssqllocaldb;Database=ProductApi;Trusted_Connection=True;"
}
```

- In the `Program.cs` file, add the DbContext to the service container:

```csharp
builder.Services.AddDbContext<ApplicationDbContext>(options =>
    options.UseSqlServer(builder.Configuration.GetConnectionString("DefaultConnection")));
```

5️⃣ **Step 5: Create the Controller**

- In the **Controllers** folder, create a new controller called `ProductsController`:

```csharp
using Microsoft.AspNetCore.Mvc;
using System.Collections.Generic;
using System.Linq;
using ProductApi.Models;

[ApiController]
[Route("api/[controller]")]
public class ProductsController : ControllerBase
{
    private readonly ApplicationDbContext _context;

    public ProductsController(ApplicationDbContext context)
    {
        _context = context;
    }

    // GET: api/products
    [HttpGet]
    public ActionResult<IEnumerable<Product>> GetProducts()
    {
        return _context.Products.ToList();
    }

    // GET: api/products/5
    [HttpGet("{id}")]
    public ActionResult<Product> GetProduct(int id)
    {
        var product = _context.Products.Find(id);

        if (product == null)
        {
            return NotFound();
        }

        return product;
    }

    // POST: api/products
    [HttpPost]
    public ActionResult<Product> PostProduct(Product product)
    {
        _context.Products.Add(product);
        _context.SaveChanges();

        return CreatedAtAction(nameof(GetProduct), new { id = product.Id }, product);
    }

    // PUT: api/products/5
    [HttpPut("{id}")]
    public IActionResult PutProduct(int id, Product product)
    {
        if (id != product.Id)
        {
            return BadRequest();
        }

        _context.Entry(product).State = EntityState.Modified;
        _context.SaveChanges();

        return NoContent();
    }

    // DELETE: api/products/5
    [HttpDelete("{id}")]
    public IActionResult DeleteProduct(int id)
    {
        var product = _context.Products.Find(id);
        if (product == null)
        {
            return NotFound();
        }

        _context.Products.Remove(product);
        _context.SaveChanges();

        return NoContent();
    }
}
```

6️⃣ **Step 6: Test the API**

- Use **Postman** to test your API endpoints.

### **End Points:**

| Method | URL             | Description         |
| ------ | --------------- | ------------------- |
| GET    | /api/products   | Get all products    |
| GET    | /api/products/1 | Get a product by ID |
| POST   | /api/products   | Add a new product   |
| PUT    | /api/products/1 | Update a product    |
| DELETE | /api/products/1 | Delete a product    |

---

## **🧩 Practical Labs**

### **Lab 1: Create a CRUD API**

**Goal:** Build a CRUD API for managing a list of products.

🔧 **Steps:**

1. Create a new ASP.NET Core Web API project.
2. Define the `Product` model.
3. Set up the `ApplicationDbContext`.
4. Create the `ProductsController`.
5. Test the API using Postman.

### **Lab 2: Enhance the API**

**Goal:** Add additional features to your API.

🔧 **Tasks:**

1. Implement input validation.
2. Add error handling.
3. Implement pagination for the GET endpoint.

---

Congratulations on completing Day 6! Tomorrow, you’ll learn how to secure your API using JWT authentication.

