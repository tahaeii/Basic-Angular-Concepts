# Nested Routes (Child Routes)

Child Routes help create a hierarchical structure for application routes. This is useful when defining internal pages for a specific section, such as a **User Management** section that includes "User List" and "User Details" pages.

## Implementing Child Routes in Angular

### 1. Defining Nested Routes

First, define the child routes inside `app-routing.module.ts`:

```typescript
const routes: Routes = [
  {
    path: 'users',
    component: UsersComponent,
    children: [
      { path: 'list', component: UserListComponent },
      { path: 'profile/:id', component: UserProfileComponent }
    ]
  }
]
```

**This means:**

- Navigating to `/users/list` will display **UserListComponent**.
- Navigating to `/users/profile/5` will display **UserProfileComponent**.

### 2. Using `<router-outlet>` in the Parent Component

In `users.component.html`, which serves as the parent component, we use `<router-outlet>` to display the child components:

```html
<h2>User Management</h2>
<nav>
  <a routerLink="list">User List</a>
  <a routerLink="profile/1">User Details</a>
</nav>
<!-- 
  <router-outlet> is a special directive in Angular that defines 
  where the content of components related to child routes should be displayed.  
  In this example, whenever the route "users/list" or "users/profile/:id" is activated,  
  the corresponding component (UserListComponent or UserProfileComponent) will be displayed here.
-->
<router-outlet></router-outlet>
```

This ensures that **UserListComponent** or **UserProfileComponent** is displayed **inside** `UsersComponent`, not across the entire application.

**Practical Outcome**

| **Route**          | **Displayed Component** |
| ------------------ | ----------------------- |
| `/users/list`      | `UserListComponent`     |
| `/users/profile/1` | `UserProfileComponent`  |

This method is particularly useful when displaying multiple related pages within a section **without affecting other parts of the application**.