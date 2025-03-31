# Configuring Routes

In Angular, routes are defined in the **`app-routing.module.ts`** file. These routes determine **which component** should be displayed when a user navigates to a specific URL.  

---

## Types of Routes in Angular:

### Static Routes  
The simplest type of route, mapping a **fixed URL** to a component:  
```typescript
{ path: 'home', component: HomeComponent }
```

---

### Dynamic Routes  
Used when we need to retrieve **dynamic values** from the URL.  

```typescript
{ path: 'user/:id', component: UserProfileComponent }
```
In this example, the `id` value is extracted from the URL inside `UserProfileComponent`:  

```typescript
import { ActivatedRoute } from '@angular/router';

constructor(private route: ActivatedRoute) {}

ngOnInit() {
  const userId = this.route.snapshot.paramMap.get('id');
  console.log('User ID:', userId);
}
```

---

### Default and Invalid Routes

- **`path: ''`** → Sets the default route.  
- **`path: '**'`** → Handles invalid URLs (404 page).  

```typescript
{ path: '', redirectTo: '/home', pathMatch: 'full' }, // Default Page
{ path: '**', component: PageNotFoundComponent } // 404 Page
```

---

## Full Example:
```typescript
const routes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'about', component: AboutComponent },
  { path: 'user/:id', component: UserProfileComponent },
  { path: '**', component: PageNotFoundComponent }
];
```  

Now, Angular will **dynamically render components** based on the URL!