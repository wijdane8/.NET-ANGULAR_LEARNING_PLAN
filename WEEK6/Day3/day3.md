# **.NET & Angular Guide: Week 6 - Advanced Topics**

## **🧩 Day 28: Real-Time Communication with SignalR**

Welcome to Day 28! Today, you will explore SignalR—a library in ASP.NET Core that enables real-time communication between clients and servers. Real-time features are essential for applications like chat systems, live notifications, and collaborative tools.

---

## **🧩 What is SignalR?**

SignalR simplifies the process of adding real-time web functionality to your application. It allows the server to push updates to connected clients, eliminating the need for frequent polling.

### **Features of SignalR:**
1. **Real-Time Communication:** Enables bi-directional communication between client and server.
2. **Automatic Reconnection:** Handles reconnection if the connection is dropped.
3. **Protocol Support:** Supports WebSockets, Server-Sent Events, and Long Polling.
4. **Hub-Based Architecture:** Uses hubs for communication between server and clients.

---

## **🧩 Setting Up SignalR**

### **Step 1: Add SignalR to the Backend**
1. **Install the SignalR NuGet Package:**
   ```bash
   dotnet add package Microsoft.AspNetCore.SignalR
   ```

2. **Create a Hub Class:**
   Define a hub for communication.
   ```csharp
   public class ChatHub : Hub {
       public async Task SendMessage(string user, string message) {
           await Clients.All.SendAsync("ReceiveMessage", user, message);
       }
   }
   ```

3. **Register SignalR in the Pipeline:**
   Add SignalR to the middleware pipeline in `Program.cs`:
   ```csharp
   builder.Services.AddSignalR();

   app.UseEndpoints(endpoints => {
       endpoints.MapHub<ChatHub>("/chatHub");
   });
   ```

### **Step 2: Add SignalR to the Angular Frontend**
1. **Install the SignalR Client Library:**
   ```bash
   npm install @microsoft/signalr
   ```

2. **Create a SignalR Service:**
   Create a service to manage SignalR connections.
   ```typescript
   import { Injectable } from '@angular/core';
   import * as signalR from '@microsoft/signalr';

   @Injectable({ providedIn: 'root' })
   export class SignalRService {
       private hubConnection: signalR.HubConnection;

       startConnection(): void {
           this.hubConnection = new signalR.HubConnectionBuilder()
               .withUrl('http://localhost:5000/chatHub')
               .build();

           this.hubConnection.start()
               .then(() => console.log('Connection started'))
               .catch(err => console.log('Error while starting connection: ', err));
       }

       onReceiveMessage(callback: (user: string, message: string) => void): void {
           this.hubConnection.on('ReceiveMessage', callback);
       }
   }
   ```

3. **Use the Service in a Component:**
   Update the component to send and receive messages.
   ```typescript
   export class ChatComponent {
       user: string = '';
       message: string = '';
       messages: { user: string, message: string }[] = [];

       constructor(private signalRService: SignalRService) {}

       ngOnInit(): void {
           this.signalRService.startConnection();
           this.signalRService.onReceiveMessage((user, message) => {
               this.messages.push({ user, message });
           });
       }

       sendMessage(): void {
           this.signalRService.hubConnection
               .invoke('SendMessage', this.user, this.message)
               .catch(err => console.error(err));
           this.message = '';
       }
   }
   ```

---

## **🧩 Practical Labs**

### **Lab 1: Build a Chat Application**
**Goal:** Create a simple chat application using SignalR.

🔧 **Tasks:**
1. Create a `ChatHub` class in the backend.
2. Add SignalR support to your Angular frontend.
3. Test real-time communication by sending and receiving messages.

---

### **Lab 2: Implement Real-Time Notifications**
**Goal:** Add real-time notifications to an existing application.

🔧 **Tasks:**
1. Create a `NotificationHub` class in the backend.
2. Push notifications to connected clients when specific events occur (e.g., new data added).
3. Display notifications in the Angular app.

---

## **🧩 Reflection Questions**
1. How does SignalR differ from traditional polling methods?
2. What are the benefits of using hubs for real-time communication?
3. How can SignalR improve user engagement in your applications?

---

🎉 **Congratulations on completing Day 28!** You’ve learned how to implement real-time communication in your applications using SignalR. Tomorrow, you’ll begin exploring advanced RxJS concepts in Angular.

