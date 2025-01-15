# **.NET & Angular Guide: Week 2 - Advanced ASP.NET Core and API Development**

## **🧩 Day 7: Securing Your API with JWT Authentication**

Welcome to Day 7! Today, you’ll learn how to secure your ASP.NET Core API using **JSON Web Tokens (JWT)** for authentication. JWT is a compact, URL-safe token format used for securely transmitting information between parties. By the end of this guide, you’ll be able to implement token-based authentication in your API.

---

## **🧩 What is JWT?**
JSON Web Tokens (JWT) are a secure way to represent claims between two parties. JWTs are often used in authentication systems to verify user identities and control access to protected resources.

### **Structure of a JWT:**
A JWT consists of three parts:
1. **Header:** Contains the token type and hashing algorithm.
2. **Payload:** Contains the claims (user information).
3. **Signature:** Verifies the integrity of the token.

Example JWT:
```text
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```

💡 **Why Use JWT?**
- Stateless authentication
- Compact and URL-safe
- Easy to integrate with APIs

---

## **🧩 Steps to Implement JWT Authentication**

1️⃣ **Step 1: Install the Required Packages**

Open the **Package Manager Console** in Visual Studio and run:
```bash
Install-Package Microsoft.AspNetCore.Authentication.JwtBearer
```

2️⃣ **Step 2: Add Authentication to `Program.cs`**

Modify the `Program.cs` file to configure JWT authentication:
```csharp
using Microsoft.AspNetCore.Authentication.JwtBearer;
using Microsoft.IdentityModel.Tokens;
using System.Text;

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
    .AddJwtBearer(options =>
    {
        options.TokenValidationParameters = new TokenValidationParameters
        {
            ValidateIssuer = true,
            ValidateAudience = true,
            ValidateLifetime = true,
            ValidateIssuerSigningKey = true,
            ValidIssuer = builder.Configuration["Jwt:Issuer"],
            ValidAudience = builder.Configuration["Jwt:Audience"],
            IssuerSigningKey = new SymmetricSecurityKey(Encoding.UTF8.GetBytes(builder.Configuration["Jwt:Key"]))
        };
    });

builder.Services.AddControllers();

var app = builder.Build();

app.UseAuthentication();
app.UseAuthorization();

app.MapControllers();

app.Run();
```

3️⃣ **Step 3: Add JWT Configuration in `appsettings.json`**

Add the following section to your `appsettings.json` file:
```json
"Jwt": {
  "Key": "MySuperSecretKey12345",
  "Issuer": "https://localhost:5001",
  "Audience": "https://localhost:5001"
}
```

4️⃣ **Step 4: Create a Token Service**

Create a new service class called `TokenService` in the **Services** folder:
```csharp
using Microsoft.IdentityModel.Tokens;
using System;
using System.IdentityModel.Tokens.Jwt;
using System.Security.Claims;
using System.Text;

public class TokenService
{
    private readonly IConfiguration _configuration;

    public TokenService(IConfiguration configuration)
    {
        _configuration = configuration;
    }

    public string GenerateToken(string username)
    {
        var claims = new[]
        {
            new Claim(JwtRegisteredClaimNames.Sub, username),
            new Claim(JwtRegisteredClaimNames.Jti, Guid.NewGuid().ToString())
        };

        var key = new SymmetricSecurityKey(Encoding.UTF8.GetBytes(_configuration["Jwt:Key"]));
        var creds = new SigningCredentials(key, SecurityAlgorithms.HmacSha256);

        var token = new JwtSecurityToken(
            issuer: _configuration["Jwt:Issuer"],
            audience: _configuration["Jwt:Audience"],
            claims: claims,
            expires: DateTime.Now.AddMinutes(30),
            signingCredentials: creds
        );

        return new JwtSecurityTokenHandler().WriteToken(token);
    }
}
```

5️⃣ **Step 5: Create an Authentication Controller**

Create a new controller called `AuthController` in the **Controllers** folder:
```csharp
using Microsoft.AspNetCore.Mvc;
using System.Collections.Generic;

[ApiController]
[Route("api/[controller]")]
public class AuthController : ControllerBase
{
    private readonly TokenService _tokenService;

    public AuthController(TokenService tokenService)
    {
        _tokenService = tokenService;
    }

    [HttpPost("login")]
    public IActionResult Login([FromBody] LoginModel login)
    {
        if (login.Username == "admin" && login.Password == "password")
        {
            var token = _tokenService.GenerateToken(login.Username);
            return Ok(new { token });
        }
        return Unauthorized();
    }
}

public class LoginModel
{
    public string Username { get; set; }
    public string Password { get; set; }
}
```

6️⃣ **Step 6: Test the Authentication API**

Use **Postman** to test the login endpoint:
- **POST** request to `https://localhost:5001/api/auth/login`
- Body:
```json
{
  "username": "admin",
  "password": "password"
}
```
- You should receive a JWT token in the response.

### **Protect an API Endpoint**
To secure an API endpoint, add the `[Authorize]` attribute to your controller or action method:
```csharp
[Authorize]
[HttpGet("secure-data")]
public IActionResult GetSecureData()
{
    return Ok("This is a secure endpoint.");
}
```

---

## **🧩 Practical Labs**

### **Lab 1: Secure Your API**
**Goal:** Implement JWT authentication in your existing CRUD API.

🔧 **Tasks:**
1. Install the necessary packages.
2. Add JWT configuration.
3. Create a `TokenService`.
4. Create an `AuthController`.
5. Secure an API endpoint using `[Authorize]`.

### **Lab 2: Test the Secure API**
**Goal:** Use Postman to test your secure API.

🔧 **Tasks:**
1. Login to get a JWT token.
2. Use the token to access a protected endpoint.

---

Congratulations on completing Day 7! You’ve learned how to implement token-based authentication to secure your ASP.NET Core API. Tomorrow, you’ll learn about role-based authorization to further enhance your API’s security.

