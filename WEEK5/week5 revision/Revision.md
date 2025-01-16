# **.NET & Angular Guide: Week 5 - Full Stack Integration**

## **🧩 Day 25: Enhancing User Experience and Project Wrap-Up**

Welcome to Day 25! Today, you will focus on improving the user experience (UX) of your full-stack application by adding advanced features and usability improvements. By the end of this session, you’ll also summarize Week 5 and finalize your project.

---

## **🧩 Key Enhancements to User Experience**

### **1. Add Notifications and Feedback**
- Provide feedback to users for actions like saving data, deleting items, or logging in.

#### **Backend: Notifications for Actions**
Add success or error messages to API responses:
```csharp
[HttpPost("add-task")]
public IActionResult AddTask(Task task) {
    tasks.Add(task);
    return Ok(new { message = "Task added successfully!", task });
}
```

#### **Frontend: Toast Notifications**
1. Install a notification library:
   ```bash
   npm install ngx-toastr
   ```

2. Import and configure it in `AppModule`:
   ```typescript
   import { ToastrModule } from 'ngx-toastr';
   
   @NgModule({
       imports: [
           BrowserAnimationsModule,
           ToastrModule.forRoot(),
       ],
   })
   export class AppModule {}
   ```

3. Display notifications in `TaskService`:
   ```typescript
   export class TaskService {
       constructor(private toastr: ToastrService) {}

       addTask(task: Task): Observable<Task> {
           return this.http.post<Task>(this.apiUrl, task).pipe(
               tap(() => this.toastr.success('Task added successfully!'))
           );
       }
   }
   ```

### **2. Improve Navigation and Layout**
- Ensure a seamless navigation experience with a responsive layout.

#### **Add a Sidebar Navigation Menu**
1. Create a `SidebarComponent`:
   ```bash
   ng generate component sidebar
   ```

2. Add links for navigation:
   ```html
   <nav>
       <a routerLink="/dashboard">Dashboard</a>
       <a routerLink="/profile">Profile</a>
       <a routerLink="/tasks">Tasks</a>
   </nav>
   ```

3. Include the sidebar in `AppComponent`:
   ```html
   <app-sidebar></app-sidebar>
   <router-outlet></router-outlet>
   ```

### **3. Add Search and Filtering Features**
Allow users to filter tasks or search for specific information.

#### **Frontend: Implement Search**
1. Add a search bar in `TasksComponent`:
   ```html
   <input [(ngModel)]="searchQuery" placeholder="Search tasks">
   <ul>
       <li *ngFor="let task of filteredTasks()">{{ task.title }}</li>
   </ul>
   ```

2. Filter tasks based on the query:
   ```typescript
   export class TasksComponent {
       searchQuery = '';

       filteredTasks(): Task[] {
           return this.tasks.filter(task => task.title.includes(this.searchQuery));
       }
   }
   ```

---

## **🧩 Project Summary for Week 5**

### **Accomplishments**
1. **Integrated Angular with .NET Core:**
   - Established frontend-backend communication.
   - Enabled CRUD operations using APIs.

2. **Implemented Authentication and Authorization:**
   - Secured endpoints with JWT tokens.
   - Managed roles and permissions for different user types.

3. **Built User Profiles:**
   - Allowed users to view and update their profiles.
   - Displayed personalized information on the dashboard.

4. **Enhanced User Experience:**
   - Added notifications for actions.
   - Improved navigation with a sidebar.
   - Included search and filtering capabilities.

---

## **🧩 Practical Labs**

### **Lab 1: Add Notifications**
**Goal:** Enhance user feedback by integrating toast notifications.

🔧 **Tasks:**
1. Install and configure `ngx-toastr`.
2. Add notifications for task addition and deletion.

---

### **Lab 2: Implement Search and Filtering**
**Goal:** Improve task management by adding a search feature.

🔧 **Tasks:**
1. Add a search bar to filter tasks by title.
2. Test the search functionality with a large task list.

---

## **🧩 Reflection Questions**
1. How do notifications enhance the user experience in a web application?
2. What challenges did you face when implementing search and filtering?
3. How can you optimize your application for better performance?

---

🎉 **Congratulations on completing Day 25 and wrapping up Week 5!** You’ve successfully built and enhanced a full-stack application with a focus on user experience. Next week, you’ll explore advanced topics to take your skills even further.

