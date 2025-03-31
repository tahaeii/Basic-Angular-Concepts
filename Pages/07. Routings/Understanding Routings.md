# What is a Routing in Angular?

Routing in Angular allows users to **navigate between different pages** **without reloading** the entire application. This is handled by the **Angular Router**, which manages different routes efficiently.  

---

## Simple Example:  
A basic project with **two pages**: `Home` and `About`.  

**app-routing.module.ts**
Defines the **routes** for the application:  

```typescript
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { HomeComponent } from './home/home.component';
import { AboutComponent } from './about/about.component';

const routes: Routes = [
  { path: '', component: HomeComponent }, // Home Page
  { path: 'about', component: AboutComponent } // About Page
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

**app.component.html** *(Creating Navigation Links)*
```html
<nav>
  <a routerLink="/">Home</a>
  <a routerLink="/about">About</a>
</nav>
<router-outlet></router-outlet>
```

---

### **Result:**  
When the user clicks on **"About"**, the content of `AboutComponent` is displayed **without refreshing the page**!