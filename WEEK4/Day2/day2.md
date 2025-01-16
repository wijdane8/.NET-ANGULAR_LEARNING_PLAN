# **.NET & Angular Guide: Week 4 - Angular Foundations**

## **🧩 Day 17: Components and Templates**

Welcome to Day 17! Today, you will dive into **Angular components** and **templates**, which are fundamental building blocks of any Angular application. By the end of this session, you will understand how to create reusable components and define the structure of your application using templates.

---

## **🧩 Understanding Angular Components**

### **What are Components?**
- Components control a portion of the UI in Angular applications.
- Every Angular component consists of:
  - **HTML Template:** Defines the view (UI).
  - **CSS Styles:** Applies styles specific to the component.
  - **TypeScript Class:** Defines the logic and behavior of the component.

### **Anatomy of a Component**
1. **Decorator:** `@Component` metadata specifies the template, style, and selector.
2. **Class:** Contains logic and data binding.

Example:
```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-hello-world',
  template: `<h1>Hello, {{name}}!</h1>`,
  styles: [`h1 { color: blue; }`]
})
export class HelloWorldComponent {
  name: string = 'Angular';
}
```

---

## **🧩 Creating Components**

### **Using Angular CLI**
1. Generate a new component:
   ```bash
   ng generate component component-name
   # or shorthand
   ng g c component-name
   ```
2. The CLI creates the following files:
   - `component-name.component.ts`: Logic.
   - `component-name.component.html`: Template.
   - `component-name.component.css`: Styles.
   - `component-name.component.spec.ts`: Unit tests.

### **Using Components in Templates**
1. Add the component selector in another component's template:
   ```html
   <app-hello-world></app-hello-world>
   ```
2. Verify it displays correctly in the browser.

---

## **🧩 Templates in Angular**

### **Dynamic HTML with Templates**
- Use **interpolation** to display dynamic data:
  ```html
  <h1>{{title}}</h1>
  ```
- Use **property binding** to bind DOM properties:
  ```html
  <img [src]="imageUrl">
  ```

### **Directives**
- **Structural Directives:** Modify DOM structure.
  - `*ngIf`:
    ```html
    <p *ngIf="isVisible">This is visible</p>
    ```
  - `*ngFor`:
    ```html
    <ul>
      <li *ngFor="let item of items">{{item}}</li>
    </ul>
    ```

- **Attribute Directives:** Modify DOM element appearance.
  - Example:
    ```html
    <button [style.background-color]="isActive ? 'green' : 'red'">Click me</button>
    ```

---

## **🧩 Practical Labs**

### **Lab 1: Create a Profile Card Component**
**Goal:** Create and use a component to display user profile information.

🔧 **Tasks:**
1. Generate a `profile-card` component.
2. Add inputs for `name`, `role`, and `image`.
3. Use the following template for the component:
   ```html
   <div class="card">
     <img [src]="image" alt="Profile Picture">
     <h2>{{name}}</h2>
     <p>{{role}}</p>
   </div>
   ```
4. Style the component with CSS.
5. Add the component to the `AppComponent` template and pass data to it.

---

### **Lab 2: Use *ngFor to Display a List**
**Goal:** Display a list of users using the `profile-card` component.

🔧 **Tasks:**
1. Define an array of users in the `AppComponent`:
   ```typescript
   users = [
     { name: 'Alice', role: 'Developer', image: 'alice.jpg' },
     { name: 'Bob', role: 'Designer', image: 'bob.jpg' },
   ];
   ```
2. Use `*ngFor` to render a `profile-card` for each user:
   ```html
   <app-profile-card *ngFor="let user of users"
                     [name]="user.name"
                     [role]="user.role"
                     [image]="user.image">
   </app-profile-card>
   ```

---

## **🧩 Reflection Questions**
1. How does Angular's component-based architecture improve code maintainability?
2. What challenges did you encounter while working with templates and directives?
3. How can you make components more reusable and modular?

---

🎉 **Congratulations on completing Day 17!** You’ve mastered the essentials of components and templates. Tomorrow, you’ll explore data binding and event handling in Angular applications.

