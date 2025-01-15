# **.NET & Angular Guide: Week 2 - Advanced ASP.NET Core and API Development**

## **🧩 Day 8: Role-Based Authorization in ASP.NET Core**

Welcome to Day 8! Today, you’ll learn how to implement **role-based authorization** in your ASP.NET Core API. Role-based authorization allows you to control access to specific endpoints based on a user’s role (e.g., Admin, User). By the end of this guide, you’ll know how to assign roles to users and protect your API endpoints accordingly.

---

## **🧩 What is Role-Based Authorization?**
Role-based authorization is a method of controlling access to specific resources in an application based on the user’s assigned roles.

💡 **Example Use Case:**
- **Admin:** Can manage users and view all data.
- **User:** Can only view their own data.

---

## **🧩 Steps to Implement Role-Based Authorization**

1️⃣ **Step 1: Add Roles to Your Token**

Modify the `TokenService` to include roles in the JWT:

```csharp
public string GenerateToken(string username, string role)
{
    var claims = new[]
    {
        new Claim(JwtRegisteredClaimNames.Sub, username),
        new Claim(ClaimTypes.Role, role),
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
```

2️⃣ **Step 2: Update the `AuthController` to Accept Roles**

Modify the `AuthController` to assign roles during login:

```csharp
[HttpPost("login")]
public IActionResult Login([FromBody] LoginModel login)
{
    if (login.Username == "admin" && login.Password == "password")
    {
        var token = _tokenService.GenerateToken(login.Username, "Admin");
        return Ok(new { token });
    }
    else if (login.Username == "user" && login.Password == "password")
    {
        var token = _tokenService.GenerateToken(login.Username, "User");
        return Ok(new { token });
    }

    return Unauthorized();
}
```

3️⃣ **Step 3: Protect Endpoints with Roles**

Use the `[Authorize]` attribute with roles to protect your endpoints:

```csharp
[Authorize(Roles = "Admin")]
[HttpGet("admin-data")]
public IActionResult GetAdminData()
{
    return Ok("This is protected data for Admins only.");
}

[Authorize(Roles = "User")]
[HttpGet("user-data")]
public IActionResult GetUserData()
{
    return Ok("This is protected data for Users only.");
}
```

4️⃣ **Step 4: Test the Role-Based Authorization**

Use **Postman** to test the role-based endpoints:
- **POST** to `https://localhost:5001/api/auth/login` to get a token.
- Use the token to access the protected endpoints:
  - `/api/admin-data`
  - `/api/user-data`

### **Expected Behavior:**
- Admin token can access both `/admin-data` and `/user-data` endpoints.
- User token can only access `/user-data` endpoint.

---

## **🧩 Practical Labs**

### **Lab 1: Implement Role-Based Authorization**
**Goal:** Add role-based authorization to your existing API.

🔧 **Tasks:**
1. Modify the `TokenService` to include roles.
2. Update the `AuthController` to assign roles.
3. Protect specific endpoints using `[Authorize(Roles = "RoleName")]`.

### **Lab 2: Create a Multi-Role API**
**Goal:** Create an API that supports multiple roles (Admin, User, Manager).

🔧 **Tasks:**
1. Create new endpoints for each role.
2. Test the API using different tokens.

---

## **🧩 Reflection Questions**
1. How would you handle additional roles in your application?
2. What are the security implications of role-based authorization?
3. How can you combine role-based authorization with claims-based authorization for more granular control?

---

Congratulations on completing Day 8! You’ve learned how to implement role-based authorization to secure your ASP.NET Core API further. In the next session, you’ll learn about advanced authorization techniques using policies and claims.

