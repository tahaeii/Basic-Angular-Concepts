# Two-Way Data Binding in Angular

**Two-Way Data Binding** is a more advanced technique in Angular that enables **bi-directional synchronization** between the component’s data and the UI. This approach is useful when users input values that need to be immediately updated in the component.

In **One-Way Data Binding**, data flows in a single direction, but in **Two-Way Data Binding**, changes in the UI and component **automatically synchronize** with each other.

---

## How to Use Two-Way Data Binding in Angular

In Angular, **ngModel** is used to implement Two-Way Data Binding. It is part of the **FormsModule**, so it must first be imported into `app.module.ts`:

```typescript
import { FormsModule } from '@angular/forms'

@NgModule({
  imports: [FormsModule]
})
export class AppModule {}
```

Then, in the component:

```typescript
export class AppComponent {
  username = ''
}
```

And in the template:

```html
<input [(ngModel)]="username" placeholder="Enter your name" />
<p>Hello, {{ username }}!</p>
```

---

### How Does This Work?

✔ When the user **enters a value** in the input field, the `username` variable in the component **updates automatically**.  
✔ Any **changes to `username`** are **immediately** reflected in the UI.
