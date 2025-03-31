# How to Create a Component in Angular?

In Angular, components can be created in **two ways**:  
- **Manually**  
- **Using Angular CLI**  

---

## Creating a Component with Angular CLI
You can generate a new component using the following command:  
```sh
ng generate component my-component
```
or a shorter version:  
```sh
ng g c my-component
```
This command creates **four files**:  
```perl
my-component/
  ├── my-component.component.ts
  ├── my-component.component.html
  ├── my-component.component.css
  ├── my-component.component.spec.ts // Unit test file for my-component
```
---

## Creating a Component Manually
1. Create a **new class** in the `src/app` directory.
2. Add the `@Component` decorator to the class.
3. Specify `selector`, `templateUrl`, and `styleUrls`.  

### Example:
```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-example',
  templateUrl: './example.component.html',
  styleUrls: ['./example.component.css']
})
export class ExampleComponent {
  title = 'Example Component';
}
```
---

## Adding a Component to a Page
After creating a component, you need to declare it inside a module:

```typescript
import { ExampleComponent } from './example/example.component';

@NgModule({
  declarations: [ExampleComponent]
})
export class AppModule { }
```
Now, you can use its **selector** in HTML:  
```html
<app-example></app-example>
```