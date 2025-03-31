# What is a Module in Angular?


In **Angular**, modules are the core structure for organizing and managing different parts of an application. Every Angular app has at least one main module, known as `AppModule`. However, in large applications, splitting the code into multiple modules is recommended to improve **scalability, maintainability, and performance**.  

---

## Understanding Modules in Angular  

A **module** in Angular is a **TypeScript class** decorated with `@NgModule`, which provides information about components, directives, pipes, services, and other modules within the application.  

---

## Key Components of an Angular Module

An Angular module consists of the following sections:  

| **Section**   | **Description**  |
|--------------|----------------|
| **declarations** | Contains the components, directives, and pipes of this module. |
| **imports** | Includes other modules that this module depends on. |
| **providers** | Contains services for **Dependency Injection (DI)**. |
| **bootstrap** | Only used in `AppModule`, defining which component should be displayed at startup. |

---

## Example of a Module with Multiple Components and a Service

```typescript
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { HomeComponent } from './home/home.component';
import { AboutComponent } from './about/about.component';
import { DataService } from './services/data.service';

@NgModule({
  declarations: [HomeComponent, AboutComponent], // Registers `HomeComponent` and `AboutComponent`.  
  imports: [CommonModule], // Includes `CommonModule`, which provides common Angular directives.  
  providers: [DataService], // Registers `DataService` for dependency injection.
  exports: [HomeComponent] // Makes `HomeComponent` available for use in other modules.
})
export class SharedModule { }
```