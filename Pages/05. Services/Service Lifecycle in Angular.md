# Lifecycle of Services in Angular  

Services in Angular have a **defined lifecycle**, influenced by **Scope** and **Injector**. Understanding this lifecycle helps in **optimizing service management** and **preventing memory leaks**.

---

## How to Register (Scope) a Service in Angular?
In Angular, a service can be registered at different levels, determining **how long it stays in memory** and **where it can be accessed**.

### Registering a Service at the Root Level (Singleton)
The most common way to register a service is using **`providedIn: 'root'`**, making it a **Singleton** available throughout the application with only **one instance**.

```typescript
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root', // Creates a single instance throughout the application
})
export class AuthService {
  isAuthenticated = false;
  
  login() {
    this.isAuthenticated = true;
    console.log('User logged in');
  }
}
```
**Result**: The service remains in memory **until the application is closed** and is shared across all components and modules.  

---

### Registering a Service at the Module Level
If a service should only be available within a specific **module**, register it in the `providers` array of that module.

```typescript
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { UserService } from './user.service';

@NgModule({
  imports: [CommonModule],
  providers: [UserService], // Service is only available in this module
})
export class UserModule {}
```
**Result**: The service is only accessible **within the `UserModule` and its dependent components**.  

---

### Registering a Service at the Component Level
If a service is needed **only for a specific component and its children**, register it in the `providers` array of that component.

```typescript
import { Component } from '@angular/core';
import { LoggerService } from './logger.service';

@Component({
  selector: 'app-profile',
  templateUrl: './profile.component.html',
  providers: [LoggerService], // Service is only available in this component and its children
})
export class ProfileComponent {
  constructor(private loggerService: LoggerService) {
    this.loggerService.log('Profile component initialized');
  }
}
```
**Result**: A **new instance** of `LoggerService` is created **every time the component is rendered**.  

---

## Comparing Service Scope & Destruction Timing

| **Registration Method** | **Scope** | **Destruction Timing** |
|-------------------------|-----------|------------------------|
| `providedIn: 'root'` | **Global (Singleton)** | When the application is closed |
| **Registered in a Module** | **Only in that Module** | When the module is unloaded |
| **Registered in a Component** | **Only in that Component and its Children** | When the component is destroyed |

---

## Destroying Services & Memory Management

Services registered at the **root** or **module** level are automatically managed by Angular, so **manual destruction is not needed**. However, services registered **at the component level** are destroyed **when the component is removed**.

### Using `ngOnDestroy` for Memory Management
If a service **subscribes to an Observable**, you should **unsubscribe** when the component is destroyed to **prevent memory leaks**.

```typescript
import { Component, OnDestroy } from '@angular/core';
import { Subscription } from 'rxjs';
import { LoggerService } from './logger.service';

@Component({
  selector: 'app-profile',
  templateUrl: './profile.component.html',
  providers: [LoggerService],
})
export class ProfileComponent implements OnDestroy {
  private subscription: Subscription;

  constructor(private loggerService: LoggerService) {
    this.subscription = this.loggerService.getData().subscribe(data => {
      console.log('Received data:', data);
    });
  }

  ngOnDestroy() {
    this.subscription.unsubscribe(); // Prevents Memory Leak
    console.log('ProfileComponent destroyed');
  }
}
```
**Result**: By using `ngOnDestroy` and `unsubscribe()`, we ensure **memory is freed properly**, preventing **memory leaks**.