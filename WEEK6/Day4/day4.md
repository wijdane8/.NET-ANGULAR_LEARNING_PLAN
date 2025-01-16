# **.NET & Angular Guide: Week 6 - Advanced Topics**

## **🧩 Day 29: Advanced RxJS Concepts**

Welcome to Day 29! Today, you will dive deeper into RxJS (Reactive Extensions for JavaScript), which is a key part of Angular for managing asynchronous data streams. RxJS powers Angular’s `HttpClient`, forms, and many other features, making it an essential tool for advanced Angular applications.

---

## **🧩 What is RxJS?**

RxJS is a library for reactive programming using Observables, which provide a powerful way to work with asynchronous data streams. With RxJS, you can:
- **Compose asynchronous operations:** Combine multiple data streams.
- **Handle events gracefully:** React to user interactions or API responses.
- **Apply operators:** Transform and manipulate data streams easily.

### **Key Concepts**
1. **Observable:** Represents a data stream that can emit values over time.
2. **Observer:** Reacts to values emitted by an Observable.
3. **Subscription:** Connects an Observer to an Observable.
4. **Operators:** Transform or filter data streams (e.g., `map`, `filter`, `mergeMap`).

---

## **🧩 Advanced RxJS Operators**

### **1. Higher-Order Mapping Operators**

#### **mergeMap**
Processes multiple inner Observables concurrently.

```typescript
import { of } from 'rxjs';
import { mergeMap } from 'rxjs/operators';

of('Task 1', 'Task 2').pipe(
    mergeMap(task => fakeApiCall(task))
).subscribe(response => console.log(response));

function fakeApiCall(task: string) {
    return of(`${task} completed`);
}
```

#### **switchMap**
Cancels previous Observables when a new value is emitted.

```typescript
import { fromEvent } from 'rxjs';
import { switchMap } from 'rxjs/operators';

fromEvent(document, 'click').pipe(
    switchMap(() => fakeApiCall('Clicked'))
).subscribe(response => console.log(response));
```

#### **concatMap**
Processes Observables sequentially, maintaining order.

```typescript
import { of } from 'rxjs';
import { concatMap } from 'rxjs/operators';

of('Step 1', 'Step 2').pipe(
    concatMap(step => fakeApiCall(step))
).subscribe(response => console.log(response));
```

### **2. Combination Operators**

#### **combineLatest**
Combines multiple Observables and emits their latest values.

```typescript
import { combineLatest, of } from 'rxjs';

combineLatest([
    of('Angular'),
    of('RxJS')
]).subscribe(([framework, library]) => console.log(`${framework} with ${library}`));
```

#### **forkJoin**
Emits values from multiple Observables when all complete.

```typescript
import { forkJoin, of } from 'rxjs';

forkJoin([
    of('API 1 Response'),
    of('API 2 Response')
]).subscribe(([api1, api2]) => console.log(api1, api2));
```

---

## **🧩 Practical Labs**

### **Lab 1: Enhance a Search Feature**
**Goal:** Use RxJS operators to optimize a search bar that debounces user input and cancels previous requests.

🔧 **Tasks:**
1. Create an input field for search terms.
2. Use `debounceTime` and `switchMap` to call an API after a delay.
3. Display the search results in real-time.

#### **Sample Code:**
```typescript
searchInput.valueChanges.pipe(
    debounceTime(300),
    switchMap(term => this.apiService.search(term))
).subscribe(results => this.searchResults = results);
```

---

### **Lab 2: Combine Data Streams**
**Goal:** Display a dashboard combining user information and activity logs.

🔧 **Tasks:**
1. Fetch user data and activity logs using separate API calls.
2. Use `combineLatest` to merge the data streams.
3. Display the combined data on the dashboard.

---

## **🧩 Reflection Questions**
1. What are the advantages of using higher-order mapping operators in RxJS?
2. How do combination operators like `combineLatest` simplify handling multiple data streams?
3. What scenarios benefit most from `switchMap` compared to `mergeMap`?

---

🎉 **Congratulations on completing Day 29!** You’ve explored advanced RxJS operators and learned how to manage complex data streams in Angular applications. Tomorrow, you’ll delve into lazy loading and custom directives for further enhancing application performance and functionality.

