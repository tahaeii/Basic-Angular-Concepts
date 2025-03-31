# Attribute Directives in Angular

**Attribute Directives** modify the **behavior or appearance** of an element **without changing** the DOM structure.

---

## Common Attribute Directives in Angular

| **Directive** | **Usage**                             |
| ------------- | ------------------------------------- |
| `ngClass`     | Dynamically add or remove CSS classes |
| `ngStyle`     | Dynamically change an element’s style |
| `ngModel`     | Two-way data binding for form inputs  |

---

### `ngClass` – Dynamic CSS Class Binding

**Example:**

```html
<p [ngClass]="{'text-success': isSuccess, 'text-danger': !isSuccess}">
  Message Status
</p>
```

```typescript
isSuccess = true
```

If `isSuccess = true`, the class **`text-success`** is added.  
If `isSuccess = false`, the class **`text-danger`** is added.

---

### `ngStyle` – Dynamic Inline Styling

**Example:**

```html
<p [ngStyle]="{'color': isWarning ? 'red' : 'black'}">
  This text changes color dynamically
</p>
```

```typescript
isWarning = false
```

If `isWarning = true`, the text **turns red**.

---

### `ngModel` – Two-Way Data Binding

**Example:**

```html
<input [(ngModel)]="username" placeholder="Enter your name" />
<p>Your name: {{ username }}</p>
```

```typescript
username = ''
```

The input value is **automatically synchronized** with the `username` variable.
