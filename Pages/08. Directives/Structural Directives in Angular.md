# Structural Directives in Angular

**Structural Directives** directly affect the **DOM structure** by adding, removing, or replacing elements.  
All structural directives are prefixed with `*`.

---

## Common Structural Directives in Angular

| **Directive** | **Usage**                                        |
| ------------- | ------------------------------------------------ |
| `*ngIf`       | Show or hide an element based on a condition     |
| `*ngFor`      | Repeat an element for each value in a list       |
| `*ngSwitch`   | Display one of multiple options based on a value |

---

### `*ngIf` – Show or Remove an Element

This directive **displays an element** in the DOM **only if a condition is true**.

**Example:**

```html
<p *ngIf="isVisible">This text is shown only if isVisible is true.</p>
```

```typescript
isVisible = true
```

If `isVisible = false`, the `<p>` element is **removed from the DOM**.

**More efficient than `hidden`** → The element is **completely removed** instead of just being hidden.

---

### `*ngFor` – Repeat an Element for Each Array Item

This directive **iterates over an array** and creates an element for each value.

\*\*Example: Displaying a List of Users

```html
<ul>
  <li *ngFor="let user of users">{{ user.name }}</li>
</ul>
```

```typescript
users = [{ name: 'Ali' }, { name: 'Zahra' }, { name: 'Mohammad' }]
```

**Getting the index of each item:**

```html
<li *ngFor="let user of users; let i = index">{{ i + 1 }} - {{ user.name }}</li>
```

---

### `*ngSwitch` – Display One of Multiple Options

Used when you want to **show only one element** based on a variable’s value.

**Example:**

```html
<div [ngSwitch]="status">
  <p *ngSwitchCase="'success'">Operation was successful!</p>
  <p *ngSwitchCase="'error'">An error occurred.</p>
  <p *ngSwitchDefault>Processing...</p>
</div>
```

```typescript
status = 'success' // Can be "error" or another value.
```
