# **.NET & Angular Guide: Week 6 - Advanced Topics**

## **🧩 Day 26: Advanced Dependency Injection in ASP.NET Core**

Welcome to Day 26! Today, you will explore advanced techniques for Dependency Injection (DI) in ASP.NET Core, enhancing the flexibility and maintainability of your backend application.

---

## **🧩 Recap of Dependency Injection**
- **What is DI?**
  - A design pattern used to achieve Inversion of Control (IoC).
  - It allows the application to inject dependencies rather than creating them explicitly.

- **Benefits of DI:**
  - Increases testability.
  - Reduces tight coupling between components.
  - Enhances scalability and flexibility.

---

## **🧩 Advanced Dependency Injection Techniques**

### **1. Service Lifetimes**
- **Transient**: Creates a new instance every time the service is requested.
- **Scoped**: Creates one instance per request.
- **Singleton**: Creates one instance for the entire application lifetime.

#### **Example:**
```csharp
builder.Services.AddTransient<ITransientService, TransientService>();
builder.Services.AddScoped<IScopedService, ScopedService>();
builder.Services.AddSingleton<ISingletonService, SingletonService>();
```

### **2. Using Factories for Complex Dependencies**
Factories can be used to customize how services are created.

#### **Example:**
```csharp
builder.Services.AddTransient<IMyService>(provider => {
    var configuration = provider.GetRequiredService<IConfiguration>();
    return new MyService(configuration["MyKey"]);
});
```

### **3. Conditional Dependency Resolution**
Register services based on specific conditions.

#### **Example:**
```csharp
if (env.IsDevelopment()) {
    builder.Services.AddSingleton<IMyService, DevelopmentService>();
} else {
    builder.Services.AddSingleton<IMyService, ProductionService>();
}
```

### **4. Named or Keyed Dependencies**
Provide different implementations based on a key.

#### **Example:**
Use a dictionary of implementations:
```csharp
builder.Services.AddSingleton<Func<string, IMyService>>(provider => key => {
    var services = new Dictionary<string, IMyService> {
        { "A", new ServiceA() },
        { "B", new ServiceB() },
    };
    return services[key];
});
```

### **5. Resolving Services Manually**
Use the service provider directly to resolve dependencies in rare cases.

#### **Example:**
```csharp
var myService = app.ApplicationServices.GetRequiredService<IMyService>();
```

---

## **🧩 Practical Labs**

### **Lab 1: Experiment with Service Lifetimes**
**Goal:** Understand the differences between transient, scoped, and singleton services.

🔧 **Tasks:**
1. Create a logging service and register it with all three lifetimes.
2. Log the service instance ID in a controller to observe the differences.

---

### **Lab 2: Implement Conditional Dependencies**
**Goal:** Use environment-based registration for a service.

🔧 **Tasks:**
1. Create two implementations of a service (`DevelopmentService` and `ProductionService`).
2. Register them conditionally based on the environment.
3. Test the application in both development and production modes.

---

## **🧩 Reflection Questions**
1. How do service lifetimes affect resource management in an application?
2. What scenarios might require the use of factories or conditional dependencies?
3. How can advanced DI techniques improve the scalability of your application?

---

🎉 **Congratulations on completing Day 26!** You’ve mastered advanced Dependency Injection techniques in ASP.NET Core. Tomorrow, you’ll delve into middleware and explore how it can be used to enhance your application.

