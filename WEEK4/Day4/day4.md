# **.NET & Angular Guide: Week 4 - Angular Advanced Features**

## **🧩 Day 19: Services and Dependency Injection**

Welcome to Day 19! Today, you will explore **Angular services** and **dependency injection** (DI), which are essential for building scalable and maintainable applications. Services enable components to share data, while DI provides a way to supply objects to components efficiently.

---

## **🧩 Understanding Angular Services**

### **What are Services?**
- Services in Angular are singleton classes designed to share logic or data across components.
- They provide a clean separation of concerns by isolating business logic from the UI.

### **Common Use Cases**
1. Sharing data between components.
2. Fetching data from APIs.
3. Managing application-wide state.

---

## **🧩 Creating and Using Services**

### **Step 1: Generate a Service**
Use Angular CLI to create a new service:
```bash
ng generate service data
```
This creates two files:
- `data.service.ts`: The service logic.
- `data.service.spec.ts`: The test file for the service.

### **Step 2: Define Logic in the Service**
Add methods and properties to the service class:
```typescript
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class DataService {
  private data: string[] = [];

  getData(): string[] {
    return this.data;
  }

  addData(item: string): void {
    this.data.push(item);
  }
}
```

### **Step 3: Inject the Service into a Component**
Use dependency injection to access the service in a component:
```typescript
import { Component } from '@angular/core';
import { DataService } from './data.service';

@Component({
  selector: 'app-data-list',
  template: `
    <ul>
      <li *ngFor="let item of data">{{ item }}</li>
    </ul>
    <button (click)="addItem()">Add Item</button>
  `
})
export class DataListComponent {
  data: string[] = [];

  constructor(private dataService: DataService) {}

  ngOnInit(): void {
    this.data = this.dataService.getData();
  }

  addItem(): void {
    this.dataService.addData('New Item');
    this.data = this.dataService.getData();
  }
}
```

---

## **🧩 Understanding Dependency Injection (DI)**

### **What is DI?**
- A design pattern where a class receives its dependencies from an external source rather than creating them internally.
- Angular’s DI system provides services to components or other services.

### **DI Hierarchy**
- **Root Injector:** Services provided at the root level are singleton and available throughout the application.
- **Component-Level Injector:** Services provided at a specific component level are limited to that component and its children.

---

## **🧩 Practical Labs**

### **Lab 1: Share Data Between Components Using a Service**

**Goal:** Create a service to manage a shared list of tasks between two components.

🔧 **Tasks:**
1. Generate a `TaskService`.
2. Define methods to add, remove, and retrieve tasks.
3. Use the service in two components (`TaskListComponent` and `TaskManagerComponent`) to share the task list.

**Example:**
- `TaskService`:
  ```typescript
  @Injectable({ providedIn: 'root' })
  export class TaskService {
    private tasks: string[] = [];

    getTasks(): string[] {
      return this.tasks;
    }

    addTask(task: string): void {
      this.tasks.push(task);
    }

    removeTask(index: number): void {
      this.tasks.splice(index, 1);
    }
  }
  ```

- `TaskListComponent`:
  ```typescript
  constructor(private taskService: TaskService) {}

  tasks = this.taskService.getTasks();
  ```

### **Lab 2: Fetch Data from an API Using a Service**

**Goal:** Create a service to fetch data from a public API and display it in a component.

🔧 **Tasks:**
1. Generate a `PostService`.
2. Use Angular’s `HttpClient` to fetch data from `https://jsonplaceholder.typicode.com/posts`.
3. Display the posts in a `PostListComponent`.

**Example:**
- `PostService`:
  ```typescript
  @Injectable({ providedIn: 'root' })
  export class PostService {
    constructor(private http: HttpClient) {}

    fetchPosts(): Observable<any> {
      return this.http.get('https://jsonplaceholder.typicode.com/posts');
    }
  }
  ```

- `PostListComponent`:
  ```typescript
  posts: any[] = [];

  constructor(private postService: PostService) {}

  ngOnInit(): void {
    this.postService.fetchPosts().subscribe(data => this.posts = data);
  }
  ```

---

## **🧩 Reflection Questions**
1. How does dependency injection improve code reusability and testability?
2. What are the benefits of using services for state management?
3. How can you decide whether to provide a service at the root or component level?

---

🎉 **Congratulations on completing Day 19!** You’ve learned how to use Angular services and dependency injection to share data and manage dependencies. Tomorrow, you’ll dive into routing and navigation to build single-page applications.

