# Dynamic Forms in Angular

Sometimes, we need a **dynamic form**, where the number of fields changes based on conditions. **Reactive Forms** in Angular allow us to **dynamically add and remove fields** in a form.

---

## Understanding Dynamic Forms

Standard forms have a fixed structure, but in some cases, we need to:  
- Change the number of inputs based on user needs.  
- Allow users to add new fields (e.g., multiple phone numbers).  
- Fetch form data from an API and dynamically build the form.

---

## Implementing Dynamic Forms in Angular

### Step 1: Configure FormArray in Reactive Forms

We use **FormArray** to manage dynamic fields.

**First, import `ReactiveFormsModule`:**

```typescript
import { ReactiveFormsModule } from '@angular/forms'

@NgModule({
  imports: [ReactiveFormsModule]
})
export class AppModule {}
```

### Step 2: Define the Dynamic Form in `component.ts`

```typescript
import { Component } from '@angular/core'
import { FormArray, FormControl, FormGroup, Validators } from '@angular/forms'

@Component({
  selector: 'app-dynamic-form',
  templateUrl: './dynamic-form.component.html'
})
export class DynamicFormComponent {
  userForm = new FormGroup({
    name: new FormControl('', Validators.required),
    emails: new FormArray([]) // Array to manage multiple emails
  })

  get emails() {
    return this.userForm.get('emails') as FormArray
  }

  addEmail() {
    this.emails.push(
      new FormControl('', [Validators.required, Validators.email])
    )
  }

  removeEmail(index: number) {
    this.emails.removeAt(index)
  }

  onSubmit() {
    console.log('Form Data:', this.userForm.value)
  }
}
```

### Step 3: Create the Dynamic Form in `component.html`

```html
<form [formGroup]="userForm" (ngSubmit)="onSubmit()">
  <label>Name:</label>
  <input formControlName="name" />
  <div *ngIf="userForm.controls.name.invalid && userForm.controls.name.touched">
    Name is required.
  </div>

  <h4>Emails:</h4>
  <div formArrayName="emails">
    <div *ngFor="let email of emails.controls; let i = index">
      <input [formControlName]="i" placeholder="Enter email" />
      <button type="button" (click)="removeEmail(i)">❌ Remove</button>
    </div>
  </div>

  <button type="button" (click)="addEmail()">➕ Add Email</button>

  <button type="submit" [disabled]="userForm.invalid">Submit</button>
</form>
```

---

## Key Points

- **FormArray** is a collection of form controls that can be dynamically added or removed.  
- **`addEmail()`** adds a new email field to the array.  
- **`removeEmail(index)`** removes an email field from the array.

This form allows users to enter multiple emails and remove them as needed.

---

## Conclusion

- **FormArray** in Reactive Forms enables **dynamic and scalable forms**.  
- Ideal for managing **lists of phone numbers, emails, or addresses**.  
- Instead of using a fixed number of `FormControl`, we use `FormArray` for better flexibility.
