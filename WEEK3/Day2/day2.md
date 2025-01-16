# **.NET & Angular Guide: Week 3 - Backend API Development**

## **🧩 Day 12: Authentication and Authorization**

Welcome to Day 12! Today, you’ll learn how to secure your API using **JWT authentication** and implement **role-based authorization**. These are crucial skills for building secure, scalable web applications.

---

## **🧩 What is Authentication and Authorization?**
- **Authentication:** Verifies the identity of a user.
- **Authorization:** Determines what actions a user is allowed to perform.

💡 **Why Use JWT?**
- Stateless authentication
- Compact, URL-safe format
- Easy integration with APIs

---

## **🧩 Steps to Implement JWT Authentication**

1️⃣ **Step 1: Install Required Packages**
- Open the **Package Manager Console** in Visual Studio and run:
```bash
Install-Package Microsoft.AspNetCore.Authentication.JwtBearer
```

2️⃣ **Step 2: Configure JWT in `Program.cs`**
- Add the following configuration:

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

var app = builder.Build();

app.UseAuthentication();
app.UseAuthorization();

app.Run();
```

3️⃣ **Step 3: Add JWT Configuration in `appsettings.json`**
```json
"Jwt": {
  "Key": "MySuperSecretKey12345",
  "Issuer": "https://localhost:5001",
  "Audience": "https://localhost:5001"
}
```

4️⃣ **Step 4: Create a Token Service**
- Add a new service called `TokenService`:

```csharp
using Microsoft.IdentityModel.Tokens;
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

    public string GenerateToken(string username, string role)
    {
        var claims = new[]
        {
            new Claim(ClaimTypes.Name, username),
            new Claim(ClaimTypes.Role, role)
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

5️⃣ **Step 5: Update the `AuthController`**
- Add an authentication controller:

```csharp
using Microsoft.AspNetCore.Mvc;

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
            var token = _tokenService.GenerateToken(login.Username, "Admin");
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

6️⃣ **Step 6: Protect Endpoints with `[Authorize]`**
- Use the `[Authorize]` attribute to secure API endpoints:

```csharp
[Authorize]
[HttpGet("secure-data")]
public IActionResult GetSecureData()
{
    return Ok("This is a protected resource.");
}
```

---

## **🧩 Practical Labs**

### **Lab 1: Secure Your API**
**Goal:** Implement JWT authentication and role-based authorization in your API.

🔧 **Tasks:**
1. Add JWT authentication.
2. Create roles (e.g., Admin, User).
3. Protect specific endpoints using `[Authorize(Roles = "RoleName")]`.

### **Lab 2: Test API Security**
**Goal:** Use Postman to test secure endpoints.

🔧 **Tasks:**
1. Login to get a JWT token.
2. Use the token to access protected endpoints.
3. Verify role-based restrictions.

---

Congratulations on completing Day 12! Tomorrow, you’ll learn about connecting your API to a database using Entity Framework Core.

