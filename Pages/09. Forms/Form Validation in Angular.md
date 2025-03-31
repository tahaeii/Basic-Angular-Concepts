# Form Validation in Angular 
Validation ensures that users enter correct data. Angular supports two types of validation:  

- **Built-in Validators**: `required`, `email`, `minLength`, `maxLength`, etc.  
- **Custom Validators**: User-defined validation functions.  

---

## Validation in Template-driven Forms

```html
<input type="email" name="email" [(ngModel)]="email" required email />
<div *ngIf="myForm.controls.email?.invalid && myForm.controls.email?.touched">
  Please enter a valid email.
</div>
```

---

## Validation in Reactive Forms

```typescript
userForm = new FormGroup({
  email: new FormControl('', [Validators.required, Validators.email]),
});
```  

### Using Validation in HTML

```html
<input formControlName="email" />
<div *ngIf="userForm.controls.email.invalid && userForm.controls.email.touched">
  Please enter a valid email.
</div>
```

---

## Custom Validation
To enforce custom rules (e.g., prohibiting certain words), we can create a **custom validator function**:  

```typescript
import { AbstractControl, ValidationErrors } from '@angular/forms';

export function forbiddenNameValidator(control: AbstractControl): ValidationErrors | null {
  return control.value.includes('admin') ? { forbiddenName: true } : null;
}
```  

### Using the Custom Validator in a Form

```typescript
name: new FormControl('', [Validators.required, forbiddenNameValidator])
```  

**This prevents users from entering "admin" as their name.**  

---  
## Dynamic Error Messages

```html
<div *ngIf="userForm.controls.email.hasError('required')">
  Email is required.
</div>
<div *ngIf="userForm.controls.email.hasError('email')">
  Please enter a valid email.
</div>
```  

**This dynamically displays error messages based on the validation type.**