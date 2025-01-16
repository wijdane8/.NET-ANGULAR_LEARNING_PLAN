# **.NET & Angular Guide: Week 5 - Full Stack Integration**

## **🧩 Day 24: Building User Profiles and Dashboard**

Welcome to Day 24! Today, you will implement user profiles and create a user dashboard to display personalized information. This will help improve user engagement and provide a better user experience.

---

## **🧩 Understanding User Profiles**

### **What is a User Profile?**
A user profile stores personalized information about a user, such as their name, email, preferences, and activity data.

### **Why Create a User Dashboard?**
- Centralizes user-specific data.
- Enhances user experience by providing relevant information.
- Allows users to manage their accounts more effectively.

---

## **🧩 Backend Implementation**

### **Step 1: Extend the User Model**
1. Update the `User` model to include profile information:
   ```csharp
   public class User {
       public int Id { get; set; }
       public string Username { get; set; }
       public string Email { get; set; }
       public string FullName { get; set; }
       public DateTime DateOfBirth { get; set; }
       public string ProfilePictureUrl { get; set; }
   }
   ```

2. Add a method to retrieve user profiles in `UserController`:
   ```csharp
   [HttpGet("profile")]
   [Authorize]
   public IActionResult GetProfile() {
       var userId = User.FindFirstValue(ClaimTypes.NameIdentifier);
       var user = _context.Users.FirstOrDefault(u => u.Id.ToString() == userId);
       if (user == null) return NotFound("User not found");
       return Ok(user);
   }
   ```

### **Step 2: Add an Update Profile Endpoint**
Allow users to update their profile details:
```csharp
[HttpPut("profile")]
[Authorize]
public IActionResult UpdateProfile([FromBody] User updatedProfile) {
    var userId = User.FindFirstValue(ClaimTypes.NameIdentifier);
    var user = _context.Users.FirstOrDefault(u => u.Id.ToString() == userId);
    if (user == null) return NotFound("User not found");

    user.FullName = updatedProfile.FullName;
    user.DateOfBirth = updatedProfile.DateOfBirth;
    user.ProfilePictureUrl = updatedProfile.ProfilePictureUrl;
    _context.SaveChanges();

    return Ok(user);
}
```

---

## **🧩 Frontend Implementation**

### **Step 1: Create a Profile Service**
1. Generate a service for managing user profiles:
   ```bash
   ng generate service profile
   ```

2. Implement methods to fetch and update user profiles:
   ```typescript
   @Injectable({ providedIn: 'root' })
   export class ProfileService {
       private apiUrl = 'http://localhost:5000/api/profile';

       constructor(private http: HttpClient) {}

       getProfile(): Observable<User> {
           return this.http.get<User>(this.apiUrl);
       }

       updateProfile(profile: User): Observable<User> {
           return this.http.put<User>(this.apiUrl, profile);
       }
   }
   ```

### **Step 2: Create a Profile Component**
1. Generate a component for the user profile:
   ```bash
   ng generate component profile
   ```

2. Display the profile in the template:
   ```html
   <div *ngIf="user">
       <img [src]="user.profilePictureUrl" alt="Profile Picture">
       <h2>{{ user.fullName }}</h2>
       <p>Email: {{ user.email }}</p>
       <p>Date of Birth: {{ user.dateOfBirth | date }}</p>
   </div>

   <button (click)="editProfile()">Edit Profile</button>
   ```

3. Fetch and update user data in the component:
   ```typescript
   export class ProfileComponent {
       user: User | null = null;

       constructor(private profileService: ProfileService) {}

       ngOnInit(): void {
           this.profileService.getProfile().subscribe(data => this.user = data);
       }

       editProfile(): void {
           // Navigate to an edit profile form.
       }
   }
   ```

### **Step 3: Create an Edit Profile Form**
1. Add a form to update user details:
   ```html
   <form (ngSubmit)="onSubmit()">
       <input [(ngModel)]="user.fullName" name="fullName" placeholder="Full Name">
       <input [(ngModel)]="user.dateOfBirth" name="dateOfBirth" placeholder="Date of Birth" type="date">
       <input [(ngModel)]="user.profilePictureUrl" name="profilePictureUrl" placeholder="Profile Picture URL">
       <button type="submit">Save</button>
   </form>
   ```

2. Handle the update logic:
   ```typescript
   onSubmit(): void {
       if (this.user) {
           this.profileService.updateProfile(this.user).subscribe(updatedUser => this.user = updatedUser);
       }
   }
   ```

---

## **🧩 Practical Labs**

### **Lab 1: Create User Profiles**
**Goal:** Set up endpoints to fetch and update user profiles.

🔧 **Tasks:**
1. Extend the `User` model to include profile information.
2. Add endpoints for fetching and updating user profiles.
3. Test the endpoints using Postman.

---

### **Lab 2: Build a Profile Component**
**Goal:** Display and update user profiles in the Angular app.

🔧 **Tasks:**
1. Create a profile component and fetch user data from the API.
2. Implement a form to update profile details.
3. Style the profile page for a better user experience.

---

## **🧩 Reflection Questions**
1. How can user profiles enhance the usability of your application?
2. What security measures should you consider when handling user profiles?
3. How would you scale user profiles for applications with millions of users?

---

🎉 **Congratulations on completing Day 24!** You’ve successfully implemented user profiles and created a personalized dashboard. Tomorrow, you’ll focus on enhancing the user experience further with additional features.

