# Change Detection Strategies

Angular uses a mechanism called **Change Detection** to update the UI. This mechanism ensures that any changes in the component’s data are reflected in the UI.  
However, unnecessary UI updates can lead to **performance degradation**. To manage this process efficiently, Angular provides two different strategies:

**Change Detection Strategies in Angular**:

1. **Default**
2. **OnPush** (Optimized)

Each of these strategies has a specific way of managing changes, which we will explain below.

---

## Default Change Detection Strategy

In **Default Mode**, Angular checks the **entire component tree** after every change. This means:

- When a value changes, **all child components** are also checked.
- This check happens even if the input value of the child component has not changed.
- Any **event, setTimeout, or HTTP request** triggers a complete **Change Detection cycle**.

```typescript
@Component({
  selector: 'app-child',
  template: `<p>Child Component: {{ value }}</p>`
})
export class ChildComponent {
  @Input() value!: number
}
```

```typescript
@Component({
  selector: 'app-parent',
  template: `
    <button (click)="changeValue()">Change Value</button>
    <app-child [value]="counter"></app-child>
  `
})
export class ParentComponent {
  counter = 0
  changeValue() {
    this.counter++
  }
}
```

In this case:

- Every time the button is clicked, `counter` is updated.
- Angular **runs Change Detection across the entire app**.
- Even if the new value is the same as the previous one, Change Detection still executes.

**Problem with this approach:**
In large applications, these **unnecessary checks** reduce performance.

---

## OnPush Change Detection Strategy

**OnPush** is an **optimization technique** that reduces the number of Change Detection cycles.

When using `ChangeDetectionStrategy.OnPush`, Angular **only runs Change Detection** in specific cases.

**When Change Detection Runs in OnPush**:

1. A new value is received via `@Input()` **(and the new value !== previous value)**.
2. An **event handler** runs inside the component.
3. A change occurs in an **Observable** or **Signal**, producing a new value.

### How to Enable OnPush

```typescript
import { ChangeDetectionStrategy, Component, Input } from '@angular/core'

@Component({
  selector: 'app-child',
  template: `<p>Child Component: {{ value }}</p>`,
  changeDetection: ChangeDetectionStrategy.OnPush // Enabling OnPush
})
export class ChildComponent {
  @Input() value!: number
}
```

With this setup, `ChildComponent` will only update if it receives a **new object** via `@Input()`.

---

## Default vs. OnPush: When to Use Each?

| Feature                                                       | **Default**                          | **OnPush**                                          |
| ------------------------------------------------------------- | ------------------------------------ | --------------------------------------------------- |
| **How changes are checked?**                                  | The entire component tree is checked | Only if `@Input` changes or an event occurs         |
| **Does changing a local variable trigger Change Detection?**  | Yes                                  | No                                                  |
| **Does updating a normal variable execute Change Detection?** | Yes                                  | No, unless a new object is passed to `@Input`       |
| **Best suited for?**                                          | Small to medium applications         | Large-scale apps that need performance optimization |
| **Requires manual management?**                               | No                                   | Yes, developers must ensure new values are passed   |

### When to Use **OnPush**?

✔ When data comes from **Immutable Objects** or **RxJS Observables**.  
✔ When there are **many child components** and we don't want to check the entire tree.  
✔ In **high-data applications** where small changes **should not trigger full UI checks**.

### When to Use **Default**?

✔ When there are **frequent updates** and we don’t want to complicate Change Detection management.  
✔ When **performance optimization is not a primary concern**.
