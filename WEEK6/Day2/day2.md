# **.NET & Angular Guide: Week 6 - Advanced Topics**

## **🧩 Day 27: Advanced Middleware in ASP.NET Core**

Welcome to Day 27! Today, you will explore middleware in ASP.NET Core—a powerful feature for handling HTTP requests and responses. Middleware allows you to build pipelines that process requests and responses in a modular way.

---

## **🧩 What is Middleware?**

### **Definition**
Middleware is software that is assembled into an application pipeline to handle requests and responses. Each component can:
- Process the request before passing it to the next component.
- Process the response on its way back.

### **Examples of Built-in Middleware**
1. **Static Files Middleware:** Serves static files like images, CSS, and JavaScript.
2. **Routing Middleware:** Matches incoming requests to endpoints.
3. **Authentication Middleware:** Validates and manages user authentication.
4. **Exception Handling Middleware:** Handles unhandled exceptions globally.

---

## **🧩 Building a Middleware Pipeline**
Middleware components are added to the pipeline in `Program.cs` or `Startup.cs`.

#### **Example Pipeline**
```csharp
var app = builder.Build();

app.UseExceptionHandler("/error");
app.UseRouting();
app.UseAuthentication();
app.UseAuthorization();
app.UseStaticFiles();
app.UseEndpoints(endpoints => {
    endpoints.MapControllers();
});

app.Run();
```

---

## **🧩 Creating Custom Middleware**

### **Step 1: Create a Middleware Class**
Define a class that implements the `Invoke` or `InvokeAsync` method.

#### **Example:** Logging Middleware
```csharp
public class LoggingMiddleware {
    private readonly RequestDelegate _next;

    public LoggingMiddleware(RequestDelegate next) {
        _next = next;
    }

    public async Task InvokeAsync(HttpContext context) {
        Console.WriteLine($"Request: {context.Request.Method} {context.Request.Path}");
        await _next(context);
        Console.WriteLine($"Response: {context.Response.StatusCode}");
    }
}
```

### **Step 2: Register the Middleware**
Use the `UseMiddleware` extension method to add it to the pipeline.

```csharp
app.UseMiddleware<LoggingMiddleware>();
```

---

## **🧩 Common Middleware Scenarios**

### **1. Error Handling**
Handle errors gracefully with custom middleware.

#### **Example:**
```csharp
public class ErrorHandlingMiddleware {
    private readonly RequestDelegate _next;

    public ErrorHandlingMiddleware(RequestDelegate next) {
        _next = next;
    }

    public async Task InvokeAsync(HttpContext context) {
        try {
            await _next(context);
        } catch (Exception ex) {
            context.Response.StatusCode = 500;
            await context.Response.WriteAsync($"An error occurred: {ex.Message}");
        }
    }
}
```

### **2. Caching Middleware**
Improve performance by caching responses.

#### **Example:**
```csharp
public class CachingMiddleware {
    private readonly RequestDelegate _next;

    public CachingMiddleware(RequestDelegate next) {
        _next = next;
    }

    public async Task InvokeAsync(HttpContext context) {
        if (context.Request.Path == "/cache") {
            context.Response.Headers["Cache-Control"] = "public, max-age=60";
        }
        await _next(context);
    }
}
```

---

## **🧩 Practical Labs**

### **Lab 1: Create a Logging Middleware**
**Goal:** Build and test a middleware that logs request and response details.

🔧 **Tasks:**
1. Create a `LoggingMiddleware` class.
2. Register it in the pipeline.
3. Verify the logs in the console.

---

### **Lab 2: Implement Error Handling Middleware**
**Goal:** Create middleware to handle unhandled exceptions gracefully.

🔧 **Tasks:**
1. Define an `ErrorHandlingMiddleware` class.
2. Catch exceptions and return a user-friendly error message.
3. Test the middleware by simulating an exception.

---

## **🧩 Reflection Questions**
1. How does middleware improve the modularity of an application?
2. What are the potential pitfalls of using custom middleware?
3. How can middleware be combined to create powerful pipelines?

---

🎉 **Congratulations on completing Day 27!** You’ve learned how to use middleware to enhance request and response handling in your ASP.NET Core applications. Tomorrow, you’ll delve into SignalR for real-time communication.

