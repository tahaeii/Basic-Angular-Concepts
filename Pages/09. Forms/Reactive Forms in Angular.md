# Reactive Forms in Angular
Reactive Forms are suitable for **complex and dynamic forms**, offering full control over input data.  

## Features:
- More structured and organized code  
- Suitable for large and complex forms  
- Supports **FormGroup** and **FormControl** for better management  

---

## Implementing a Reactive Form

### Step 1: Import `ReactiveFormsModule`  
First, add `ReactiveFormsModule` in `app.module.ts`:  

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { ReactiveFormsModule } from '@angular/forms';
import { AppComponent } from './app.component';

@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule, ReactiveFormsModule], // Add ReactiveFormsModule
  bootstrap: [AppComponent],
})
export class AppModule {}
```  
---

### Step 2: Creating the Form in TypeScript

```typescript
import { Component } from '@angular/core';
import { FormGroup, FormControl, Validators } from '@angular/forms';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
})
export class AppComponent {
  userForm = new FormGroup({
    name: new FormControl('', Validators.required),
    email: new FormControl('', [Validators.required, Validators.email]),
  });

  onSubmit() {
    console.log('Form Data:', this.userForm.value);
  }
}
```  

---

### Step 3: Creating the Form in HTML  

```html
<form [formGroup]="userForm" (ngSubmit)="onSubmit()">
  <label for="name">Name:</label>
  <input id="name" formControlName="name" />
  <div *ngIf="userForm.controls.name.invalid && userForm.controls.name.touched">
    Name is required.
  </div>

  <label for="email">Email:</label>
  <input id="email" formControlName="email" />
  <div *ngIf="userForm.controls.email.invalid && userForm.controls.email.touched">
    Please enter a valid email.
  </div>

  <button type="submit" [disabled]="userForm.invalid">Submit</button>
</form>
```  

**Reactive Forms** provide advanced validation and dynamic interaction with user inputs.