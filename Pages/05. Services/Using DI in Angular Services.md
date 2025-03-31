# What is Dependency Injection (DI)?  
**Dependency Injection (DI)** is a **design pattern** where dependencies of a class are **injected from the outside** instead of being created within the class itself. This improves **flexibility**, **testability**, and **reduces hard-coded dependencies**.  

## Example of Dependency Injection in Angular

Angular has a built-in **Injector** that manages services and injects them into different parts of the application. Instead of each component creating its own service, **Angular manages it and injects it when needed**!

### 1. Defining a Service  
```typescript
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root', // Makes the service globally available in the application
})
export class LoggerService {
  log(message: string) {
    console.log(`[LOG]: ${message}`);
  }
}
```  
The **`@Injectable({ providedIn: 'root' })`** tells Angular to keep this service as a **Singleton** throughout the entire application.  

### 2. Injecting the Service into a Component  
```typescript
import { Component } from '@angular/core';
import { LoggerService } from './logger.service';

@Component({
  selector: 'app-home',
  template: `<button (click)="logMessage()">Log Message</button>`,
})
export class HomeComponent {
  constructor(private loggerService: LoggerService) {}

  logMessage() {
    this.loggerService.log('Button clicked!');
  }
}
```  
Now, when the button is clicked, the message will be logged in the console!