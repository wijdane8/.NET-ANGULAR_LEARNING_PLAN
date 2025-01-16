# **.NET & Angular Guide: Week 5 - Full Stack Integration**

## **🧩 Day 21: Introduction to Full Stack Integration**

Welcome to Day 21! This week, you’ll begin integrating Angular with a .NET backend to create full-stack applications. Today’s focus is on setting up the project architecture, ensuring both the frontend and backend are ready to communicate effectively.

---

## **🧩 Understanding Full Stack Integration**

### **What is Full Stack Integration?**
- Combining a backend server (ASP.NET Core) and a frontend framework (Angular) to create complete applications.
- The backend handles data processing, authentication, and APIs.
- The frontend provides a user interface and consumes backend services.

### **Key Concepts**
1. **RESTful APIs:** Used by the frontend to interact with backend services.
2. **CORS (Cross-Origin Resource Sharing):** Ensures secure communication between the frontend and backend hosted on different domains.
3. **Shared Data Models:** Ensures consistent data representation between the two layers.

---

## **🧩 Setting Up the Full Stack Environment**

### **Step 1: Prepare the Backend**
1. **Create a New ASP.NET Core API Project:**
   ```bash
   dotnet new webapi -n TaskManagerAPI
   ```

2. **Set Up a Model:**
   Define a `Task` model in the backend:
   ```csharp
   public class Task {
       public int Id { get; set; }
       public string Title { get; set; }
       public string Description { get; set; }
       public bool IsCompleted { get; set; }
   }
   ```

3. **Create a Controller:**
   Add a `TasksController` with CRUD endpoints:
   ```csharp
   [Route("api/[controller]")]
   [ApiController]
   public class TasksController : ControllerBase {
       private static List<Task> tasks = new List<Task>();

       [HttpGet]
       public IActionResult GetTasks() => Ok(tasks);

       [HttpPost]
       public IActionResult AddTask(Task task) {
           tasks.Add(task);
           return Ok(task);
       }
   }
   ```

4. **Enable CORS:**
   Add the following to `Startup.cs` or `Program.cs`:
   ```csharp
   builder.Services.AddCors(options => {
       options.AddPolicy("AllowAngularApp", policy => {
           policy.WithOrigins("http://localhost:4200")
                 .AllowAnyMethod()
                 .AllowAnyHeader();
       });
   });

   app.UseCors("AllowAngularApp");
   ```

### **Step 2: Prepare the Frontend**

1. **Create a New Angular Project:**
   ```bash
   ng new task-manager
   cd task-manager
   ng generate component tasks
   ```

2. **Install `HttpClientModule`:**
   Ensure the `HttpClientModule` is imported in `AppModule`:
   ```typescript
   import { HttpClientModule } from '@angular/common/http';

   @NgModule({
     imports: [
       BrowserModule,
       HttpClientModule,
     ],
   })
   export class AppModule {}
   ```

3. **Create a Service to Call the API:**
   ```typescript
   @Injectable({ providedIn: 'root' })
   export class TaskService {
       private apiUrl = 'http://localhost:5000/api/tasks';

       constructor(private http: HttpClient) {}

       getTasks(): Observable<Task[]> {
           return this.http.get<Task[]>(this.apiUrl);
       }

       addTask(task: Task): Observable<Task> {
           return this.http.post<Task>(this.apiUrl, task);
       }
   }
   ```

4. **Display Tasks in the Component:**
   Use the service in the `TasksComponent`:
   ```typescript
   export class TasksComponent {
       tasks: Task[] = [];

       constructor(private taskService: TaskService) {}

       ngOnInit(): void {
           this.taskService.getTasks().subscribe(data => this.tasks = data);
       }
   }
   ```

---

## **🧩 Practical Labs**

### **Lab 1: Backend Setup**

**Goal:** Set up a basic ASP.NET Core API with CORS enabled and CRUD endpoints.

🔧 **Tasks:**
1. Create an API project and add a `Task` model.
2. Implement CRUD operations in the `TasksController`.
3. Test the endpoints using Postman.

---

### **Lab 2: Frontend Integration**

**Goal:** Set up an Angular application and consume the backend API.

🔧 **Tasks:**
1. Create an Angular project and a `TaskService`.
2. Fetch tasks from the backend and display them in a component.
3. Add a form to add new tasks via the API.

---

## **🧩 Reflection Questions**
1. Why is enabling CORS necessary for frontend-backend communication?
2. How do shared data models improve consistency in a full-stack app?
3. What challenges did you face while integrating the Angular frontend with the .NET backend?

---

🎉 **Congratulations on completing Day 21!** You’ve set up the foundation for a full-stack application by integrating Angular with a .NET Core API. Tomorrow, you’ll expand this project with user authentication and enhanced features.

