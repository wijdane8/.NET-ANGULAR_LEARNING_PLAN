# **.NET & Angular Guide: Week 5 - Full Stack Integration**

## **🧩 Day 22: Adding Authentication to Your Full Stack Application**

Welcome to Day 22! Today, you’ll implement user authentication in your full-stack application. By the end of this session, your application will allow users to log in, receive a JWT token, and access protected resources.

---

## **🧩 Understanding Authentication**

### **What is Authentication?**
- Authentication is the process of verifying the identity of a user.
- In this guide, you’ll use JSON Web Tokens (JWTs) for stateless authentication.

### **Key Components of Authentication**
1. **Login Endpoint:** Validates user credentials and generates a JWT.
2. **JWT:** A token that contains user identity and claims.
3. **Authorization Header:** Used by the client to send the token with API requests.
4. **Middleware:** Validates the JWT and allows or denies access to endpoints.

---

## **🧩 Backend Implementation**

### **Step 1: Install JWT Authentication Packages**
1. Add the required NuGet packages to your ASP.NET Core project:
   ```bash
   dotnet add package Microsoft.AspNetCore.Authentication.JwtBearer
   dotnet add package System.IdentityModel.Tokens.Jwt
   ```

### **Step 2: Configure Authentication**
1. Update the `Program.cs` file:
   ```csharp
   builder.Services.AddAuthentication("Bearer")
       .AddJwtBearer(options => {
           options.TokenValidationParameters = new TokenValidationParameters {
               ValidateIssuer = true,
               ValidateAudience = true,
               ValidateLifetime = true,
               ValidateIssuerSigningKey = true,
               ValidIssuer = "https://yourapi.com",
               ValidAudience = "https://yourapi.com",
               IssuerSigningKey = new SymmetricSecurityKey(Encoding.UTF8.GetBytes("YourSecretKey"))
           };
       });

   app.UseAuthentication();
   app.UseAuthorization();
   ```

2. Define the secret key in your configuration file (e.g., `appsettings.json`):
   ```json
   {
       "Jwt": {
           "Key": "YourSecretKey",
           "Issuer": "https://yourapi.com",
           "Audience": "https://yourapi.com"
       }
   }
   ```

### **Step 3: Create the Login Endpoint**
1. Add a `LoginController` to your project:
   ```csharp
   [Route("api/[controller]")]
   [ApiController]
   public class LoginController : ControllerBase {
       [HttpPost("login")]
       public IActionResult Login([FromBody] LoginRequest request) {
           if (request.Username == "admin" && request.Password == "password") {
               var token = GenerateJwtToken(request.Username);
               return Ok(new { Token = token });
           }
           return Unauthorized();
       }

       private string GenerateJwtToken(string username) {
           var claims = new[] {
               new Claim(JwtRegisteredClaimNames.Sub, username),
               new Claim(JwtRegisteredClaimNames.Jti, Guid.NewGuid().ToString())
           };

           var key = new SymmetricSecurityKey(Encoding.UTF8.GetBytes("YourSecretKey"));
           var creds = new SigningCredentials(key, SecurityAlgorithms.HmacSha256);

           var token = new JwtSecurityToken(
               issuer: "https://yourapi.com",
               audience: "https://yourapi.com",
               claims: claims,
               expires: DateTime.Now.AddMinutes(30),
               signingCredentials: creds
           );

           return new JwtSecurityTokenHandler().WriteToken(token);
       }
   }
   ```

---

## **🧩 Frontend Implementation**

### **Step 1: Create an Authentication Service**
1. Add a `AuthService` to your Angular app:
   ```typescript
   @Injectable({ providedIn: 'root' })
   export class AuthService {
       private apiUrl = 'http://localhost:5000/api/login';

       constructor(private http: HttpClient) {}

       login(username: string, password: string): Observable<any> {
           return this.http.post(this.apiUrl, { username, password });
       }
   }
   ```

### **Step 2: Build a Login Component**
1. Create a `LoginComponent`:
   ```typescript
   @Component({
       selector: 'app-login',
       templateUrl: './login.component.html',
   })
   export class LoginComponent {
       username = '';
       password = '';

       constructor(private authService: AuthService) {}

       onLogin(): void {
           this.authService.login(this.username, this.password).subscribe(
               response => {
                   localStorage.setItem('token', response.token);
                   console.log('Login successful');
               },
               error => console.error('Login failed')
           );
       }
   }
   ```

### **Step 3: Protect Routes**
1. Implement a route guard to secure routes:
   ```typescript
   @Injectable({ providedIn: 'root' })
   export class AuthGuard implements CanActivate {
       constructor(private router: Router) {}

       canActivate(): boolean {
           const token = localStorage.getItem('token');
           if (token) {
               return true;
           }
           this.router.navigate(['/login']);
           return false;
       }
   }
   ```

2. Apply the guard to secure routes in `app-routing.module.ts`:
   ```typescript
   const routes: Routes = [
       { path: 'dashboard', component: DashboardComponent, canActivate: [AuthGuard] },
       { path: 'login', component: LoginComponent }
   ];
   ```

---

## **🧩 Practical Labs**

### **Lab 1: Backend Authentication**
**Goal:** Add JWT-based authentication to your ASP.NET Core API.

🔧 **Tasks:**
1. Install JWT packages and configure authentication.
2. Create a login endpoint that generates a JWT token.
3. Test the login endpoint using Postman.

---

### **Lab 2: Frontend Authentication**
**Goal:** Implement a login mechanism and protect routes in Angular.

🔧 **Tasks:**
1. Create an `AuthService` to handle login requests.
2. Build a `LoginComponent` with a login form.
3. Add a route guard to protect sensitive pages.

---

## **🧩 Reflection Questions**
1. What are the benefits of using JWTs for authentication?
2. How does a route guard enhance the security of your Angular app?
3. What additional features could you add to your authentication system?

---

🎉 **Congratulations on completing Day 22!** You’ve successfully implemented user authentication in your full-stack application. Tomorrow, you’ll focus on adding more advanced features, such as user roles and permissions.

