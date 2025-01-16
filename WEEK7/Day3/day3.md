# **.NET & Angular Guide: Week 7 - DevOps & Deployment**

## **🧩 Day 33: Introduction to CI/CD**

Welcome to Day 33! Today, you’ll explore the fundamentals of Continuous Integration and Continuous Deployment (CI/CD), a critical process for automating builds, tests, and deployments. By the end of this guide, you’ll set up a basic CI/CD pipeline for your full-stack application using GitHub Actions.

---

## **🧩 What is CI/CD?**

CI/CD is a methodology that automates application development workflows, ensuring faster delivery and higher quality.

### **Key Components of CI/CD:**
1. **Continuous Integration (CI):** Automates the process of merging code changes and running tests.
2. **Continuous Deployment (CD):** Automates the deployment of code to production environments after successful tests.

---

## **🧩 Benefits of CI/CD**
- **Faster Releases:** Automates repetitive tasks to shorten release cycles.
- **Improved Quality:** Ensures every change is tested and verified.
- **Consistency:** Reduces human error in deployment processes.
- **Collaboration:** Encourages developers to integrate changes frequently.

---

## **🧩 Setting Up a CI/CD Pipeline with GitHub Actions**

### **Step 1: Create a Workflow File**
1. In your GitHub repository, navigate to `.github/workflows`.
2. Create a file named `ci-cd.yml`.

### **Step 2: Define the Workflow**
Add the following to your `ci-cd.yml` file:

```yaml
name: CI/CD Pipeline

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout Code
      uses: actions/checkout@v3

    - name: Setup .NET
      uses: actions/setup-dotnet@v3
      with:
        dotnet-version: '7.0'

    - name: Install Dependencies
      run: dotnet restore

    - name: Build the Application
      run: dotnet build --no-restore

    - name: Run Tests
      run: dotnet test --no-build

  deploy:
    runs-on: ubuntu-latest
    needs: build

    steps:
    - name: Checkout Code
      uses: actions/checkout@v3

    - name: Deploy to Azure
      env:
        AZURE_WEBAPP_NAME: ${{ secrets.AZURE_WEBAPP_NAME }}
        AZURE_WEBAPP_PACKAGE_PATH: ./publish
      run: |
        echo "Deploying to Azure..."
        # Add Azure CLI deployment steps here.
```

### **Explanation:**
- **on:** Specifies when the workflow runs (e.g., on push to `main`).
- **jobs:** Defines the build and deploy processes.
- **steps:** Lists individual tasks (e.g., checking out code, building, testing).

---

## **🧩 Enhancing Your CI/CD Pipeline**

### **Add Linting for Angular**
Include a step to lint your Angular code:

```yaml
- name: Install Node.js
  uses: actions/setup-node@v3
  with:
    node-version: '16'

- name: Install Angular CLI
  run: npm install -g @angular/cli

- name: Lint Angular Code
  run: ng lint
```

### **Automate Docker Image Build**
Build and push a Docker image as part of the pipeline:

```yaml
- name: Build Docker Image
  run: docker build -t myapp:latest .

- name: Push Docker Image
  run: |
    echo "Pushing Docker image..."
    docker tag myapp:latest myregistry/myapp:latest
    docker push myregistry/myapp:latest
```

---

## **🧩 Practical Labs**

### **Lab 1: Create a Basic CI/CD Pipeline**
**Goal:** Set up a pipeline to automate builds and tests for your .NET and Angular applications.

🔧 **Tasks:**
1. Create a GitHub Actions workflow for your backend.
2. Add build and test steps for the Angular frontend.
3. Verify that the pipeline triggers on code pushes.

---

### **Lab 2: Deploy to Azure Using CI/CD**
**Goal:** Automate deployment of your full-stack app to Azure.

🔧 **Tasks:**
1. Add Azure deployment steps to the workflow.
2. Use GitHub Secrets to securely store Azure credentials.
3. Verify the deployment after a successful pipeline run.

---

## **🧩 Reflection Questions**
1. What challenges did you face while setting up the pipeline?
2. How does CI/CD improve the development workflow?
3. What additional steps could you add to your pipeline for better quality assurance?

---

🎉 **Congratulations on completing Day 33!** You’ve set up a CI/CD pipeline to automate your application’s build, test, and deployment processes. Tomorrow, you’ll finalize and deploy your full-stack project as part of your capstone project.

