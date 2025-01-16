# **.NET & Angular Guide: Week 5 - Full Stack Integration**

## **🧩 Day 23: Implementing Roles and Permissions**

Welcome to Day 23! Today, you’ll build upon your authentication system by introducing roles and permissions. This will allow you to restrict access to specific resources based on user roles, such as Admin or User.

---

## **🧩 Understanding Roles and Permissions**

### **What Are Roles and Permissions?**
- **Roles:** A high-level categorization of users (e.g., Admin, User, Manager).
- **Permissions:** Granular actions that users can perform (e.g., Edit, View, Delete).
- Roles typically group multiple permissions for easier management.

### **Why Are Roles and Permissions Important?**
- Enhance security by ensuring users can only access what they are authorized to.
- Simplify management of access control in applications.

---

## **🧩 Backend Implementation**

### **Step 1: Update the Login Endpoint to Include Roles**
1. Modify the `LoginController` to assign roles:
   ```csharp
   [HttpPost("login")]
   public IActionResult Login([FromBody] LoginRequest request) {
       if (request.Username == "admin" && request.Password == "password") {
           var token = GenerateJwtToken(request.Username, "Admin");
           return Ok(new { Token = token });
       } else if (request.Username == "user" && request.Password == "password") {
           var token = GenerateJwtToken(request.Username, "User");
           return Ok(new { Token = token });
       }
       return Unauthorized();
   }

   private string GenerateJwtToken(string username, string role) {
       var claims = new[] {
           new Claim(JwtRegisteredClaimNames.Sub, username),
           new Claim(ClaimTypes.Role, role),
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
   ```

### **Step 2: Protect Endpoints with Roles**
1. Use the `[Authorize]` attribute with roles:
   ```csharp
   [Authorize(Roles = "Admin")]
   [HttpPost("admin/task")]
   public IActionResult AdminTask() {
       return Ok("Admin task performed.");
   }

   [Authorize(Roles = "User")]
   [HttpGet("user/task")]
   public IActionResult UserTask() {
       return Ok("User task performed.");
   }
   ```

2. Ensure middleware is configured to validate roles.

---

## **🧩 Frontend Implementation**

### **Step 1: Decode JWT to Access Role Information**
1. Install a library to decode JWTs:
   ```bash
   npm install jwt-decode
   ```

2. Extract roles from the token:
   ```typescript
   import jwtDecode from 'jwt-decode';

   export class AuthService {
       getRoleFromToken(): string {
           const token = localStorage.getItem('token');
           if (!token) return '';
           const decoded: any = jwtDecode(token);
           return decoded["http://schemas.microsoft.com/ws/2008/06/identity/claims/role"];
       }
   }
   ```

### **Step 2: Role-Based Navigation**
1. Use role information to customize the navigation menu:
   ```typescript
   export class AppComponent {
       role = '';

       constructor(private authService: AuthService) {
           this.role = this.authService.getRoleFromToken();
       }
   }
   ```

2. Update the template to show menu items conditionally:
   ```html
   <nav>
       <a *ngIf="role === 'Admin'" routerLink="/admin">Admin Panel</a>
       <a *ngIf="role === 'User'" routerLink="/user">User Dashboard</a>
   </nav>
   ```

### **Step 3: Protect Routes Based on Roles**
1. Update the `AuthGuard` to include role validation:
   ```typescript
   @Injectable({ providedIn: 'root' })
   export class RoleGuard implements CanActivate {
       constructor(private authService: AuthService, private router: Router) {}

       canActivate(route: ActivatedRouteSnapshot): boolean {
           const expectedRole = route.data["role"];
           const tokenRole = this.authService.getRoleFromToken();

           if (tokenRole === expectedRole) {
               return true;
           }
           this.router.navigate(['/login']);
           return false;
       }
   }
   ```

2. Apply the guard to routes:
   ```typescript
   const routes: Routes = [
       { path: 'admin', component: AdminComponent, canActivate: [RoleGuard], data: { role: 'Admin' } },
       { path: 'user', component: UserComponent, canActivate: [RoleGuard], data: { role: 'User' } }
   ];
   ```

---

## **🧩 Practical Labs**

### **Lab 1: Backend Role Management**
**Goal:** Add role-based authorization to your ASP.NET Core API.

🔧 **Tasks:**
1. Modify the JWT generation to include roles.
2. Protect endpoints using the `[Authorize(Roles = "RoleName")]` attribute.
3. Test role-based access with Postman.

---

### **Lab 2: Frontend Role Management**
**Goal:** Customize the Angular app to support role-based navigation and route protection.

🔧 **Tasks:**
1. Decode JWTs on the frontend to extract role information.
2. Show navigation items based on user roles.
3. Protect routes using a custom `RoleGuard`.

---

## **🧩 Reflection Questions**
1. What are the advantages of role-based authorization over permission-based authorization?
2. How can roles be dynamically assigned or updated in a real-world application?
3. What additional security measures can you implement to secure roles and permissions?

---

🎉 **Congratulations on completing Day 23!** You’ve successfully implemented roles and permissions in your full-stack application. Tomorrow, you’ll work on enhancing the user experience with additional features.

