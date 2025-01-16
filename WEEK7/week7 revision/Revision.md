# **.NET & Angular Guide: Week 7 - DevOps & Deployment**

## **🧩 Day 35: Week 7 Summary and Refining CI/CD with Monitoring**

Welcome to Day 35! Today, you’ll wrap up Week 7 by reviewing key concepts and achievements, refining your CI/CD pipeline, and adding monitoring capabilities to your application for enhanced reliability and performance insights.

---

## **🧩 Summary of Week 7**

### **Day 31: Docker Basics**
- Learned the fundamentals of Docker.
- Created Dockerfiles for both .NET backend and Angular frontend applications.
- Built and ran Docker containers locally.

💡 **Key Takeaway:** Docker simplifies application packaging and deployment by creating lightweight, portable containers.

### **Day 32: Introduction to Kubernetes**
- Explored Kubernetes concepts like pods, deployments, and services.
- Deployed a Dockerized application to a Kubernetes cluster.
- Used `kubectl` to manage and scale applications.

💡 **Key Takeaway:** Kubernetes orchestrates containerized applications, enabling scaling, resilience, and efficient resource usage.

### **Day 33: Introduction to CI/CD**
- Set up a CI/CD pipeline using GitHub Actions.
- Automated builds, tests, and deployments for your applications.
- Integrated Docker image builds into the pipeline.

💡 **Key Takeaway:** CI/CD automates the software delivery process, reducing errors and accelerating release cycles.

### **Day 34: Finalizing and Deploying the Capstone Project**
- Deployed the full-stack application to a live environment.
- Dockerized and pushed images to a container registry.
- Tested the live application for functionality and user acceptance.

💡 **Key Takeaway:** Deployment to a live environment requires thorough preparation, integration testing, and monitoring.

---

## **🧩 Refining Your CI/CD Pipeline**

### **1. Add Build Artifacts**
Ensure your pipeline generates build artifacts (e.g., `.dll` files, Angular production builds) for troubleshooting and deployment verification.

💡 **Example:**
```yaml
- name: Upload Build Artifacts
  uses: actions/upload-artifact@v3
  with:
    name: build-artifacts
    path: ./build
```

### **2. Include Code Quality Checks**
Integrate tools like SonarCloud or ESLint for static code analysis.

💡 **Example for Angular:**
```yaml
- name: Run ESLint
  run: npm run lint
```

### **3. Automate Rollbacks**
Configure your CI/CD pipeline to automatically roll back to the last stable version in case of deployment failures.

💡 **Tip:** Use version tagging for deployments.

---

## **🧩 Adding Application Monitoring**

### **1. Use Application Performance Monitoring (APM)**
Implement tools like Azure Application Insights, New Relic, or Datadog to monitor application performance.

💡 **Steps for Azure Application Insights:**
1. Install the Application Insights SDK in your .NET backend:
   ```bash
   dotnet add package Microsoft.ApplicationInsights.AspNetCore
   ```
2. Configure Application Insights in `Startup.cs`:
   ```csharp
   services.AddApplicationInsightsTelemetry(Configuration["ApplicationInsights:InstrumentationKey"]);
   ```
3. Add the instrumentation key to `appsettings.json`:
   ```json
   {
     "ApplicationInsights": {
       "InstrumentationKey": "your-key"
     }
   }
   ```

### **2. Set Up Frontend Monitoring**
Integrate monitoring for Angular using tools like Sentry or LogRocket.

💡 **Example for Sentry:**
1. Install the Sentry SDK:
   ```bash
   npm install @sentry/angular
   ```
2. Initialize Sentry in your `main.ts` file:
   ```typescript
   import * as Sentry from "@sentry/angular";
   Sentry.init({
     dsn: "your-dsn",
   });
   ```

### **3. Monitor Logs and Alerts**
Set up logging for both backend and frontend applications. Use tools like Azure Monitor or AWS CloudWatch for centralized log management.

💡 **Tip:** Define alerts for specific thresholds, such as high CPU usage or unhandled exceptions.

---

## **🧩 Practical Labs**

### **Lab 1: Refine Your CI/CD Pipeline**
**Goal:** Enhance your pipeline with build artifacts, code quality checks, and rollback mechanisms.

🔧 **Tasks:**
1. Update the GitHub Actions workflow to include artifact uploads.
2. Add static code analysis for backend and frontend.
3. Implement version tagging for automated rollbacks.

### **Lab 2: Add Monitoring to Your Application**
**Goal:** Integrate APM and monitoring tools into your application.

🔧 **Tasks:**
1. Configure Application Insights for the backend.
2. Set up frontend monitoring using Sentry.
3. Define custom alerts and thresholds for critical issues.

---

## **🧩 Reflection Questions**
1. How does monitoring improve application reliability and user experience?
2. What additional features can you add to your CI/CD pipeline for better automation?
3. How can you ensure your monitoring setup doesn’t negatively impact application performance?

---

🎉 **Congratulations on completing Day 35!** You’ve refined your CI/CD pipeline and added monitoring capabilities, ensuring your applications are robust and reliable. Next week, you’ll focus on advanced deployment strategies and scaling.

