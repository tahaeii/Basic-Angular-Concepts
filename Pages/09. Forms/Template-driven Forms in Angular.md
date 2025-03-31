
# Template-driven Forms in Angular
This method is **suitable for simple and small forms**, where form logic is directly defined in the HTML template.  

## Features:
- Simple and easy to read  
- Requires less TypeScript code  
- Best for small forms  

---

##  Implementing a Template-driven Form

### Step 1: Import `FormsModule`
First, add `FormsModule` in `app.module.ts`:  

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { FormsModule } from '@angular/forms';
import { AppComponent } from './app.component';

@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule, FormsModule], // Add FormsModule
  bootstrap: [AppComponent],
})
export class AppModule {}
```  

---

## Step 2: Creating the Form in HTML

```html
<form #myForm="ngForm" (ngSubmit)="onSubmit()">
  <label for="name">Name:</label>
  <input type="text" id="name" name="name" [(ngModel)]="user.name" required />

  <label for="email">Email:</label>
  <input type="email" id="email" name="email" [(ngModel)]="user.email" required />

  <button type="submit" [disabled]="!myForm.valid">Submit</button>
</form>
```  

---

## Step 3: Managing Data in TypeScript

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
})
export class AppComponent {
  user = { name: '', email: '' };

  onSubmit() {
    console.log('Form submitted!', this.user);
  }
}
```
The form correctly binds values and logs the data in the console upon submission.