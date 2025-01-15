# **.NET & Angular Guide: Week 2 - Advanced ASP.NET Core and API Development**

## **🧩 Day 9: Claims-Based Authorization in ASP.NET Core**

Welcome to Day 9! Today, you’ll explore **claims-based authorization**, an advanced authorization technique in ASP.NET Core that allows you to control access based on user claims. Claims are key-value pairs that provide additional information about the user, such as their role, email, or permissions. By the end of this guide, you’ll know how to implement claims-based authorization to add more granular access control to your API.

---

## **🧩 What is Claims-Based Authorization?**
Claims-based authorization is a flexible way to control access by checking specific claims within a user's identity. Claims can include information like:
- **Role**: Admin, User, Manager
- **Permission**: Read, Write, Delete
- **Email**: user@example.com

💡 **Example Use Case:**
- A user with the claim `"CanEditProducts": true` can access the product editing endpoint.
- A user without this claim will be denied access.

---

## **🧩 Steps to Implement Claims-Based Authorization**

1️⃣ **Step 1: Add Claims to Your Token**

Modify the `TokenService` to include custom claims:

```csharp
public string GenerateToken(string username, string role, Dictionary<string, string> additionalClaims)
{
    var claims = new List<Claim>
    {
        new Claim(JwtRegisteredClaimNames.Sub, username),
        new Claim(ClaimTypes.Role, role),
        new Claim(JwtRegisteredClaimNames.Jti, Guid.NewGuid().ToString())
    };

    foreach (var claim in additionalClaims)
    {
        claims.Add(new Claim(claim.Key, claim.Value));
    }

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

2️⃣ **Step 2: Update the `AuthController` to Accept Claims**

Modify the `AuthController` to include additional claims during login:

```csharp
[HttpPost("login")]
public IActionResult Login([FromBody] LoginModel login)
{
    var additionalClaims = new Dictionary<string, string>();

    if (login.Username == "admin" && login.Password == "password")
    {
        additionalClaims.Add("CanEditProducts", "true");
        var token = _tokenService.GenerateToken(login.Username, "Admin", additionalClaims);
        return Ok(new { token });
    }
    else if (login.Username == "user" && login.Password == "password")
    {
        additionalClaims.Add("CanEditProducts", "false");
        var token = _tokenService.GenerateToken(login.Username, "User", additionalClaims);
        return Ok(new { token });
    }

    return Unauthorized();
}
```

3️⃣ **Step 3: Protect Endpoints with Claims**

Create a custom policy that checks for specific claims:

```csharp
services.AddAuthorization(options =>
{
    options.AddPolicy("EditProductsPolicy", policy =>
        policy.RequireClaim("CanEditProducts", "true"));
});
```

Use the `[Authorize]` attribute with the custom policy:

```csharp
[Authorize(Policy = "EditProductsPolicy")]
[HttpPost("edit-product")]
public IActionResult EditProduct(Product product)
{
    return Ok("Product edited successfully.");
}
```

4️⃣ **Step 4: Test Claims-Based Authorization**

Use **Postman** to test the endpoint:
- **POST** to `https://localhost:5001/api/auth/login` to get a token.
- Use the token to access the protected endpoint `/api/edit-product`.

### **Expected Behavior:**
- A user with the claim `"CanEditProducts": "true"` can access the endpoint.
- A user with the claim `"CanEditProducts": "false"` will be denied access.

---

## **🧩 Practical Labs**

### **Lab 1: Implement Claims-Based Authorization**
**Goal:** Add claims-based authorization to your existing API.

🔧 **Tasks:**
1. Modify the `TokenService` to include claims.
2. Update the `AuthController` to assign claims during login.
3. Create custom policies to protect specific endpoints.

### **Lab 2: Create a Claims-Based API**
**Goal:** Create an API that uses claims-based authorization to control access.

🔧 **Tasks:**
1. Add claims to your token.
2. Protect endpoints with custom policies.
3. Test the API using different tokens.

---

## **🧩 Reflection Questions**
1. How can you combine claims-based and role-based authorization?
2. What are some scenarios where claims-based authorization is more appropriate than role-based authorization?
3. How can you dynamically manage claims for users?

---

Congratulations on completing Day 9! You’ve learned how to implement claims-based authorization for more granular access control in your ASP.NET Core API. In the next session, you’ll learn about integrating your API with a frontend Angular application.

