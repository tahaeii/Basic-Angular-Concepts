# What is a Component in Angular?

**Components** are the **building blocks** of the user interface in Angular. Each component consists of **HTML, CSS, and TypeScript** to control a specific part of the UI.  

---

## **Structure of a Component**  
A typical Angular component includes three main parts:  

- **Template (HTML)** – Defines the **structure and appearance** of the page.  
- **Style (CSS/SCSS)** – Controls the **styling** of the component.  
- **Class (TypeScript)** – Handles the **logic and behavior** of the component.  

---

## **Example of a Simple Component**  
```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-hello',
  template: `<h1>Hello, {{ name }}!</h1>`,
  styles: [`h1 { color: blue; }`]
})
export class HelloComponent {
  name: string = 'Angular';
}
```

`selector: 'app-hello'` means you can use this component in HTML as:  
```html
<app-hello></app-hello>
```