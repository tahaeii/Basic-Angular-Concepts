# Feature Modules in Angular

In a **large Angular application**, keeping all components and services inside `AppModule` can **increase code complexity and make management difficult**. **Feature Modules** help us break the application into **smaller, manageable** sections.  

---

## Example Scenario

Assume we have a **User Management Page** that contains two components:  

- `UserListComponent` → Displays a list of users.  
- `UserDetailComponent` → Displays details of a specific user.  

---

### Step 1: Creating the User Module

We can generate a new module using the following command:  

```bash
ng generate module user
```
Or a shorter version:  

```bash
ng g m user
```
This command creates a file named `user.module.ts`.  

---

### Step 2: Generating Components Inside the Module

```bash
ng g c user/user-list
ng g c user/user-detail
```

Now, the `user` folder contains:  

```
/src/app/user/
 ├── user.module.ts
 ├── user-list/
 │   ├── user-list.component.ts
 │   ├── user-list.component.html
 ├── user-detail/
 │   ├── user-detail.component.ts
 │   ├── user-detail.component.html
```

---

### Step 3: Defining `UserModule` and Configuring It

Now, we need to register the components inside `user.module.ts`:  

**`user.module.ts`**
```typescript
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { UserListComponent } from './user-list/user-list.component';
import { UserDetailComponent } from './user-detail/user-detail.component';

@NgModule({
  declarations: [UserListComponent, UserDetailComponent], // Registers the components inside this module.  
  imports: [CommonModule], // Includes `CommonModule` to enable **Angular directives** like `*ngIf` and `*ngFor`. 
  exports: [UserListComponent] // Allows `UserListComponent` to be used in other modules if needed.  
})
export class UserModule { }
```

---

### Step 4: Importing `UserModule` in `AppModule` (Simple Approach)  

To use this module throughout the application, we need to import it inside `AppModule`:  

**`app.module.ts`**
```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent } from './app.component';
import { UserModule } from './user/user.module'; // Import User Module

@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule, UserModule], // Add UserModule
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

Now, all components inside `UserModule` are available throughout the application.