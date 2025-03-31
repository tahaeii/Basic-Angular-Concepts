# Lazy Loading in Angular

In **Angular applications**, as the **codebase grows**, loading all modules at once can **slow down the initial load time** and impact performance. **Lazy Loading** allows us to **load modules only when needed**.

| **Loading Type**            | **Description**                                |
| --------------------------- | ---------------------------------------------- |
| **Eager Loading** (Default) | Loads all modules **at the start of the app**. |
| **Lazy Loading**            | Loads modules **only when required**.          |

- Unnecessary modules **are not loaded initially**.
- Modules **load only when the user navigates to that section**.

---

## Benefits of Lazy Loading

**Faster Initial Load Time** – Users see the page **more quickly**.  
**Reduced Bandwidth Usage** – Loads **only the necessary parts**.  
**Improved Performance** – **Unused code is not loaded initially**.  
**Modular & Readable Structure** – **Better project organization**.

---

## How to Implement Lazy Loading in Angular?

### Step 1: Create a Feature Module

First, create a new module called `UserModule` for user management:

```bash
ng generate module user --route users --module app.module
```

This command **automatically** creates a **Lazy Loaded Module** and adds its route to `app-routing.module.ts`.

---

### Define the `UserModule` (`user.module.ts`)

In this file, we **only include components and modules related to users**:

```typescript
import { NgModule } from '@angular/core'
import { CommonModule } from '@angular/common'
import { RouterModule, Routes } from '@angular/router'
import { UserListComponent } from './user-list/user-list.component'
import { UserDetailComponent } from './user-detail/user-detail.component'

const routes: Routes = [
  { path: '', component: UserListComponent }, // /users
  { path: ':id', component: UserDetailComponent } // /users/:id
]

@NgModule({
  declarations: [UserListComponent, UserDetailComponent],
  imports: [CommonModule, RouterModule.forChild(routes)]
})
export class UserModule {}
```

Notice that this module uses **`RouterModule.forChild(routes)`** because it is **Lazy Loaded** inside the main app routes.

---

### Add Lazy Loading in `app-routing.module.ts`

Instead of directly importing `UserModule`, we use `loadChildren`:

```typescript
import { NgModule } from '@angular/core'
import { RouterModule, Routes } from '@angular/router'

const routes: Routes = [
  {
    path: 'users',
    loadChildren: () => import('./user/user.module').then(m => m.UserModule)
  }
]

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule {}
```

Now, when the user navigates to **`/users`**, the **`UserModule`** will be downloaded **only at that moment**, improving performance.
