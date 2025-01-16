# **.NET & Angular Guide: Week 4 - Angular Foundations**

## **🧩 Day 18: Data Binding and Event Handling**

Welcome to Day 18! Today, you will explore **data binding** and **event handling** in Angular, which are vital for creating interactive and dynamic user interfaces. By the end of this session, you will understand how to bind data between components and templates and handle user interactions effectively.

---

## **🧩 Understanding Data Binding**

### **Types of Data Binding**

1. **Interpolation**

   - Bind data from the component to the template.

   ```html
   <h1>{{ title }}</h1>
   ```

2. **Property Binding**

   - Bind properties of DOM elements to values in the component.

   ```html
   <img [src]="imageUrl">
   ```

3. **Event Binding**

   - Listen to user events and call methods in the component.

   ```html
   <button (click)="onClick()">Click Me</button>
   ```

4. **Two-Way Binding**

   - Combine property and event binding using `[(ngModel)]` for two-way data synchronization.

   ```html
   <input [(ngModel)]="username">
   <p>Hello, {{ username }}!</p>
   ```

---

## **🧩 Event Handling**

### **Binding to Events**

- Use Angular’s event binding syntax to respond to user actions.
- Syntax: `(event)="method()"`

Example:

```html
<button (click)="handleClick()">Click Me</button>
```

```typescript
handleClick() {
  alert('Button clicked!');
}
```

### **Passing Parameters to Event Handlers**

- Use `$event` to access event data.

Example:

```html
<input (input)="handleInput($event)">
```

```typescript
handleInput(event: Event) {
  console.log((<HTMLInputElement>event.target).value);
}
```

---

## **🧩 Practical Labs**

### **Lab 1: Build a Simple Form with Two-Way Binding**

**Goal:** Use `[(ngModel)]` to create a real-time interactive form.

🔧 **Tasks:**

1. Create a form with fields for `firstName` and `lastName`.
2. Bind these fields to variables in the component using `[(ngModel)]`.
3. Display a live preview of the entered name.

**Template Example:**

```html
<form>
  <label>First Name:</label>
  <input [(ngModel)]="firstName">
  <label>Last Name:</label>
  <input [(ngModel)]="lastName">
</form>
<p>Hello, {{ firstName }} {{ lastName }}!</p>
```

**Component Example:**

```typescript
firstName = '';
lastName = '';
```

---

### **Lab 2: Implement a Counter with Event Binding**

**Goal:** Create a counter app with increment and decrement functionality.

🔧 **Tasks:**

1. Display a counter value.
2. Add buttons to increase and decrease the counter.
3. Bind click events to methods in the component.

**Template Example:**

```html
<p>Counter: {{ counter }}</p>
<button (click)="increment()">Increment</button>
<button (click)="decrement()">Decrement</button>
```

**Component Example:**

```typescript
counter = 0;

increment() {
  this.counter++;
}

decrement() {
  this.counter--;
}
```

---

### **Lab 3: Create a Search Bar with Event Handling**

**Goal:** Implement a search bar that filters a list of items in real time.

🔧 **Tasks:**

1. Define a list of items in the component.
2. Add an input field to capture search terms.
3. Use an event handler to filter the displayed items based on the search term.

**Template Example:**

```html
<input (input)="filterItems($event)" placeholder="Search">
<ul>
  <li *ngFor="let item of filteredItems">{{ item }}</li>
</ul>
```

**Component Example:**

```typescript
items = ['Apple', 'Banana', 'Cherry', 'Date', 'Fig', 'Grape'];
filteredItems = [...this.items];

filterItems(event: Event) {
  const query = (<HTMLInputElement>event.target).value.toLowerCase();
  this.filteredItems = this.items.filter(item => item.toLowerCase().includes(query));
}
```

---

## **🧩 Reflection Questions**

1. How does Angular’s two-way binding simplify form handling?
2. What are some common use cases for event binding in real-world applications?
3. How can you optimize event handling for better performance?

---

🎉 **Congratulations on completing Day 18!** You have learned how to implement data binding and event handling in Angular. Tomorrow, you’ll explore services and dependency injection to enhance data sharing and management across components.

