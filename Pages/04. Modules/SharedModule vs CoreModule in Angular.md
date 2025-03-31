# Usage & Difference of SharedModule vs CoreModule in Angular  

In **large Angular applications**, to improve **code organization** and **reusability**, two key modules are commonly used:  

**SharedModule** – For **common components, directives, and pipes**.  
**CoreModule** – For **global (singleton) services**.  

---

## 1. SharedModule – Reusable Components & Pipes 

Contains **components, directives, and pipes** used across multiple modules.  
**Does not** contain services (or if it does, it may create multiple instances).  
Prevents **duplicate code** in multiple modules.  

---

### Example of a SharedModule  
Suppose multiple modules in your application need a **button component** and a **pipe to convert text to uppercase**. Instead of defining them separately in each module, place them in a **SharedModule**.  

---

### Create `button.component.ts`  
```typescript
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-button',
  template: `<button class="btn">{{ label }}</button>`,
  styles: [`.btn { padding: 10px; border-radius: 5px; }`]
})
export class ButtonComponent {
  @Input() label: string = 'Click Me';
}
```

---

### Create `uppercase.pipe.ts`  
```typescript
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({ name: 'uppercaseText' })
export class UppercasePipe implements PipeTransform {
  transform(value: string): string {
    return value.toUpperCase();
  }
}
```

---

### Create `SharedModule`  
```typescript
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { ButtonComponent } from './button/button.component';
import { UppercasePipe } from './pipes/uppercase.pipe';

@NgModule({
  declarations: [ButtonComponent, UppercasePipe],  // Define components & pipes
  imports: [CommonModule],  // Required modules
  exports: [ButtonComponent, UppercasePipe]  // Share with other modules
})
export class SharedModule { }
```
Now, whenever **ButtonComponent** or **UppercasePipe** is needed, just **import `SharedModule`**.  

---

### Use `SharedModule` in `UserModule`  
```typescript
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { SharedModule } from '../shared/shared.module';  // Import SharedModule
import { UserListComponent } from './user-list/user-list.component';

@NgModule({
  declarations: [UserListComponent],
  imports: [CommonModule, SharedModule]  // Import SharedModule
})
export class UserModule { }
```

---

## 2. CoreModule – Global Singleton Services

Contains **services that should be created only once in the entire application**.  
**Imported only once** in `AppModule`.  
Prevents **multiple instances of the same service**.  

---

### Example of a CoreModule

Suppose your application has an **authentication service (`AuthService`)** that needs to be **shared globally**.  

---

### Create `auth.service.ts`
```typescript
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'  // Makes this service a Singleton across the app
})
export class AuthService {
  private isAuthenticated = false;

  login() { this.isAuthenticated = true; }
  logout() { this.isAuthenticated = false; }
  checkAuth() { return this.isAuthenticated; }
}
```
**Using `providedIn: 'root'` ensures it is a singleton** across the entire app.  
If we don’t use `providedIn: 'root'`, we must include this service in **CoreModule**.  

---

### Create `CoreModule`  
```typescript
import { NgModule } from '@angular/core';
import { AuthService } from './services/auth.service';

@NgModule({
  providers: [AuthService]  // Add service to module
})
export class CoreModule { }
```

---

### Import `CoreModule` in `AppModule`  
```typescript
import { CoreModule } from './core/core.module';

@NgModule({
  imports: [CoreModule]  // Import CoreModule only once in AppModule
})
export class AppModule { }
```

---

## 3. Key Differences Between `SharedModule` and `CoreModule`  

| **Feature** | **SharedModule** | **CoreModule** |
|-------------|-----------------|---------------|
| **Contains** | Components, Directives, Pipes | Global Singleton Services |
| **Import Frequency** | Imported in **every module that needs it** | Imported **only once in AppModule** |
| **Includes Services?** | No (If it does, may create multiple instances) | Yes (Singleton services) |
| **Main Purpose** | **Reusing UI components** | **Managing global services** |

---

## 4. Summary  

**Use `SharedModule`** for reusable **components, directives, and pipes**.  
**Use `CoreModule`** for **global services** (like authentication, API management, logging, etc.).  
**Import `CoreModule` only once** in `AppModule`.  
**`SharedModule` can be imported in any module** that needs it.