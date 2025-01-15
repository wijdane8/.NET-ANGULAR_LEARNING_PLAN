# **Self-Learning Guide: Day 4 - Entity Framework Core**

Welcome to Day 4 of your self-paced C# learning journey! Today, you’ll explore **Entity Framework Core (EF Core)**, a powerful Object-Relational Mapping (ORM) tool that simplifies database interactions in your ASP.NET Core applications. By the end of this guide, you'll know how to set up a database, create models, and perform CRUD (Create, Read, Update, Delete) operations. Let’s dive in!

---

## **🧩 What is Entity Framework Core?**
Entity Framework Core is an ORM that allows developers to work with databases using C# code instead of SQL queries. EF Core maps your C# classes to database tables, making it easier to manage data.

### **Key Features:**
- **Cross-platform:** Works on Windows, macOS, and Linux.
- **Code-first approach:** You can create databases directly from your C# classes.
- **Database-first approach:** You can generate C# classes from an existing database.
- **Supports LINQ:** Allows you to write database queries using C# syntax.

💡 **Why Use EF Core?**
- Reduces the need to write raw SQL queries.
- Simplifies database management.
- Integrates seamlessly with ASP.NET Core.

---

## **🧩 Setting Up Entity Framework Core**
To use EF Core in your ASP.NET Core project, follow these steps:

### **Steps:**
1. **Open your ASP.NET Core project.**
2. **Install the EF Core packages:**
   Open the **Package Manager Console** in Visual Studio and run:
   ```bash
   Install-Package Microsoft.EntityFrameworkCore.SqlServer
   Install-Package Microsoft.EntityFrameworkCore.Tools
   ```
3. **Add a connection string to your `appsettings.json` file:**
   ```json
   "ConnectionStrings": {
       "DefaultConnection": "Server=(localdb)\\mssqllocaldb;Database=MyFirstDatabase;Trusted_Connection=True;"
   }
   ```
4. **Create a `DbContext` class:**
   Create a new class called `ApplicationDbContext` in the **Data** folder:
   ```csharp
   using Microsoft.EntityFrameworkCore;

   public class ApplicationDbContext : DbContext
   {
       public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options) : base(options) { }

       public DbSet<Product> Products { get; set; }
   }
   ```

💡 **Explanation:**
- **DbContext:** Represents a session with the database.
- **DbSet:** Represents a table in the database.

---

## **🧩 Creating a Model**
A model represents the structure of your database table. Let’s create a `Product` model.

### **Steps:**
1. Create a new class called `Product` in the **Models** folder:
   ```csharp
   public class Product
   {
       public int Id { get; set; }
       public string Name { get; set; }
       public decimal Price { get; set; }
   }
   ```

2. **Add the model to your `ApplicationDbContext`:**
   ```csharp
   public DbSet<Product> Products { get; set; }
   ```

---

## **🧩 Performing Migrations**
Migrations are used to create and update the database schema.

### **Steps:**
1. **Add a migration:**
   Open the **Package Manager Console** and run:
   ```bash
   Add-Migration InitialCreate
   ```

2. **Update the database:**
   Run the following command to apply the migration:
   ```bash
   Update-Database
   ```

💡 **Explanation:**
- **Add-Migration:** Creates a migration file that describes the changes to the database schema.
- **Update-Database:** Applies the migration to the database.

---

## **🧩 Performing CRUD Operations**
Let’s perform basic CRUD operations using EF Core.

### **Create Operation:**
Add a new product to the database.
```csharp
using (var context = new ApplicationDbContext())
{
    var product = new Product { Name = "Laptop", Price = 999.99M };
    context.Products.Add(product);
    context.SaveChanges();
}
```

### **Read Operation:**
Retrieve products from the database.
```csharp
using (var context = new ApplicationDbContext())
{
    var products = context.Products.ToList();
    foreach (var product in products)
    {
        Console.WriteLine($"Name: {product.Name}, Price: {product.Price}");
    }
}
```

### **Update Operation:**
Update an existing product.
```csharp
using (var context = new ApplicationDbContext())
{
    var product = context.Products.First();
    product.Price = 899.99M;
    context.SaveChanges();
}
```

### **Delete Operation:**
Delete a product from the database.
```csharp
using (var context = new ApplicationDbContext())
{
    var product = context.Products.First();
    context.Products.Remove(product);
    context.SaveChanges();
}
```

---

## **🧩 Practical Labs**

### **Lab 1: Set Up a Database with EF Core**
**Goal:** Create a new ASP.NET Core project, set up EF Core, and create a database.

🔧 **Steps:**
1. Follow the steps to install EF Core packages.
2. Create a `Product` model.
3. Perform migrations and update the database.

### **Lab 2: Perform CRUD Operations**
**Goal:** Use EF Core to perform CRUD operations on the `Product` table.

🔧 **Steps:**
1. Add a new product to the database.
2. Retrieve and display all products.
3. Update a product’s price.
4. Delete a product from the database.

### **Lab 3: Build a Simple Product Management App**
**Goal:** Build a simple web app that allows users to manage products.

🔧 **Steps:**
1. Create a new ASP.NET Core MVC project.
2. Use EF Core to connect to the database.
3. Create a `ProductController` to handle CRUD operations.
4. Create views for displaying, adding, editing, and deleting products.

---

Congratulations! You’ve completed Day 4 of your self-paced C# learning journey. Keep practicing EF Core to build more data-driven applications.

