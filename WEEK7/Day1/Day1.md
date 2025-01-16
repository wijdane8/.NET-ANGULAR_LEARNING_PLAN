# **.NET & Angular Guide: Week 7 - DevOps & Deployment**

## **🧩 Day 31: Docker Basics**

Welcome to Day 31! This week, you’ll begin your journey into DevOps and deployment strategies. Today’s focus is on understanding **Docker**, a powerful tool for creating, managing, and running containers that encapsulate your application and its dependencies.

---

## **🧩 What is Docker?**

Docker is a platform that allows developers to build, package, and run applications in containers. Containers ensure that the application behaves consistently across different environments.

### **Key Concepts**
1. **Docker Image:** A lightweight, standalone package containing all the dependencies required to run an application.
2. **Docker Container:** A runtime instance of a Docker image.
3. **Dockerfile:** A text file with instructions to build a Docker image.

### **Advantages of Docker**
- **Portability:** Run your application anywhere.
- **Consistency:** Same environment from development to production.
- **Isolation:** Avoid conflicts between different applications.
- **Efficiency:** Lightweight compared to virtual machines.

---

## **🧩 Setting Up Docker**

### **Step 1: Install Docker**
1. Download and install Docker Desktop from [Docker’s official site](https://www.docker.com/).
2. Verify installation by running:
   ```bash
   docker --version
   ```

---

## **🧩 Dockerizing a .NET API**

1. **Navigate to Your .NET Project Directory:**
   ```bash
   cd path/to/TaskManagerAPI
   ```

2. **Create a Dockerfile:**
   ```plaintext
   # Use the official ASP.NET Core runtime image
   FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
   WORKDIR /app

   # Use the .NET SDK for building the app
   FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
   WORKDIR /src
   COPY . .
   RUN dotnet restore
   RUN dotnet publish -c Release -o /app

   # Final runtime image
   FROM base AS final
   WORKDIR /app
   COPY --from=build /app .
   ENTRYPOINT ["dotnet", "TaskManagerAPI.dll"]
   ```

3. **Build the Docker Image:**
   ```bash
   docker build -t taskmanagerapi .
   ```

4. **Run the Docker Container:**
   ```bash
   docker run -p 5000:80 taskmanagerapi
   ```

   Access the API at `http://localhost:5000`.

---

## **🧩 Dockerizing an Angular Application**

1. **Navigate to Your Angular Project Directory:**
   ```bash
   cd path/to/task-manager
   ```

2. **Create a Dockerfile:**
   ```plaintext
   # Use Node.js for building the Angular app
   FROM node:16 AS build
   WORKDIR /app
   COPY package*.json ./
   RUN npm install
   COPY . .
   RUN npm run build --prod

   # Use NGINX for serving the Angular app
   FROM nginx:alpine
   COPY --from=build /app/dist/task-manager /usr/share/nginx/html
   EXPOSE 80
   CMD ["nginx", "-g", "daemon off;"]
   ```

3. **Build the Docker Image:**
   ```bash
   docker build -t taskmanagerfrontend .
   ```

4. **Run the Docker Container:**
   ```bash
   docker run -p 4200:80 taskmanagerfrontend
   ```

   Access the Angular app at `http://localhost:4200`.

---

## **🧩 Practical Labs**

### **Lab 1: Dockerize the .NET API**
**Goal:** Create and run a Docker container for your .NET API.

🔧 **Tasks:**
1. Write a `Dockerfile` for the API.
2. Build and run the Docker image.
3. Verify the API is accessible through the browser or Postman.

---

### **Lab 2: Dockerize the Angular App**
**Goal:** Create and run a Docker container for your Angular application.

🔧 **Tasks:**
1. Write a `Dockerfile` for the Angular app.
2. Build and run the Docker image.
3. Verify the app is accessible through the browser.

---

## **🧩 Reflection Questions**
1. What are the benefits of containerizing applications with Docker?
2. How does a `Dockerfile` ensure consistency across environments?
3. What steps would you take to integrate both the frontend and backend into a single Dockerized solution?

---

🎉 **Congratulations on completing Day 31!** You’ve taken your first step into DevOps by learning how to containerize .NET and Angular applications. Tomorrow, you’ll explore Kubernetes for orchestrating containers at scale.

