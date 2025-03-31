# What Are Route Guards?  

Route Guards help us **restrict access** to certain pages. For example, only **logged-in users** should be able to access the **profile page**.  

---

## Types of Route Guards in Angular:  
**CanActivate** → Determines whether a user is allowed to access a route.  
**CanDeactivate** → Checks if a user can leave a page.  
**CanLoad** → Prevents lazy-loaded modules from being loaded if the user is not authorized.  

---

## Implementing CanActivate (Protecting the User Profile Page)

### Generate a New Guard:

```bash
ng generate guard auth
```

---

### Implement Authentication Logic in `auth.guard.ts`:
```typescript
import { Injectable } from '@angular/core';
import { CanActivate, Router } from '@angular/router';

@Injectable({
  providedIn: 'root'
})
export class AuthGuard implements CanActivate {

  constructor(private router: Router) {}

  canActivate(): boolean {
    const isAuthenticated = localStorage.getItem('token') !== null;
    if (!isAuthenticated) {
      this.router.navigate(['/login']);
      return false;
    }
    return true;
  }
}
```

---

### Apply the Guard to the Route:
```typescript
const routes: Routes = [
  { path: 'profile', component: ProfileComponent, canActivate: [AuthGuard] }
];
```

---
**Result:** Now, **only logged-in users** can access the profile page. If they are **not authenticated**, they will be **redirected to the login page**.