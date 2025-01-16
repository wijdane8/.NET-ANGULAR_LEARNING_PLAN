# **.NET & Angular Guide: Week 4 - Angular Foundations**

## **🧹 Day 16: Getting Started with Angular**

Welcome to Day 16! This marks the beginning of your journey with Angular. Today, you will set up your development environment, explore the basics of Angular, and create your first Angular application.

---

## **🧹 Introduction to Angular**

### **What is Angular?**
- A framework for building single-page web applications (SPAs).
- Developed and maintained by Google.
- Uses TypeScript for development.

💡 **Key Features:**
1. Component-based architecture.
2. Two-way data binding.
3. Dependency injection for scalable applications.
4. Comprehensive tools for routing, forms, and HTTP communication.

---

## **🧹 Setting Up the Development Environment**

### **Step 1: Install Node.js**
1. Download and install Node.js from [Node.js Official Website](https://nodejs.org).
2. Verify the installation:
   ```bash
   node -v
   npm -v
   ```

### **Step 2: Install Angular CLI**
1. Install Angular CLI globally using npm:
   ```bash
   npm install -g @angular/cli
   ```
2. Verify the installation:
   ```bash
   ng version
   ```

### **Step 3: Create a New Angular Project**
1. Create a new Angular application:
   ```bash
   ng new my-first-angular-app
   ```
   - Select "CSS" when prompted for styles.
2. Navigate to your project directory:
   ```bash
   cd my-first-angular-app
   ```

### **Step 4: Run Your Angular App**
1. Start the development server:
   ```bash
   ng serve
   ```
2. Open your browser and go to `http://localhost:4200` to see your Angular app in action.

---

## **🧹 Exploring the Project Structure**

💡 **Key Files and Directories:**
1. `src/app`: Contains the core application logic, including components, modules, and services.
2. `src/index.html`: The main HTML file.
3. `angular.json`: Configuration file for the Angular CLI.

💡 **Best Practices:**
- Keep components modular and reusable.
- Organize services in a separate directory.

---

## **🧹 Practical Labs**

### **Lab 1: Create Your First Angular App**
**Goal:** Familiarize yourself with Angular's setup and structure.

🔧 **Tasks:**
1. Set up a new Angular project using Angular CLI.
2. Explore the project structure.
3. Run the app and view it in the browser.

---

### **Lab 2: Experiment with Angular CLI**
**Goal:** Understand the CLI commands and their utility.

🔧 **Tasks:**
1. Use the following Angular CLI commands:
   - `ng generate component hello-world`: Creates a new component.
   - `ng lint`: Runs the linter for the project.
   - `ng build`: Builds the project for production.
2. Modify the default `AppComponent` template to display:
   - A custom message: "Welcome to My First Angular App!"
   - A list of features you plan to implement using `*ngFor`.

---

## **🧹 Reflection Questions**
1. What benefits do you see in using Angular for web development?
2. How does Angular CLI simplify project setup and management?
3. What challenges did you face while setting up your first Angular app?

---

🎉 **Congratulations on completing Day 16!** You’ve set up your Angular environment, built your first app, and explored its structure. Tomorrow, you’ll dive into components and templates, the building blocks of Angular applications.

