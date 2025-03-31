# One-Way Data Binding in Angular

In **One-Way Data Binding**, data flows in only one direction—either **from the component to the view** or **from the view to the component**. This ensures that changes in the component directly affect the UI, but changes in the UI **do not** directly modify the component’s data unless **Event Binding** is used.

## Types of One-Way Data Binding in Angular

One-Way Data Binding is categorized into two main types:

1. **From Component to View:**

   - **Interpolation** (Displaying variable values inside text)
   - **Property Binding** (Binding values to HTML attributes)

2. **From View to Component:**
   - **Event Binding** (Binding events in HTML to component methods)

---

### 1. Interpolation (Displaying Variable Values in Text)

This method displays a **TypeScript variable’s value** inside HTML using `{{ }}` syntax.

#### Example:

```html
<h1>Welcome, {{ username }}!</h1>
```

```typescript
export class AppComponent {
  username = 'Ali'
}
```

- The `username` value is read from the component and displayed inside the `<h1>` tag.
- Any changes in `username` in TypeScript will be **instantly** reflected in the UI.

---

### 2. Property Binding (Binding Values to HTML Attributes)

In this method, a variable is bound to an **HTML attribute**. It is commonly used for attributes like `src`, `href`, `disabled`, `value`, etc.

#### Example:

```html
<img [src]="profileImage" alt="User Profile" />
```

```typescript
export class AppComponent {
  profileImage = 'assets/profile.jpg'
}
```

- The `src` attribute is bound to the `profileImage` variable.
- If `profileImage` changes, the `src` attribute is **automatically updated**.

---

### 3. Event Binding (Handling User Events)

Event Binding allows executing a **component method** when an event such as `click`, `keyup`, `mouseover`, or `input` occurs in an HTML element.

#### Example:

```html
<button (click)="sayHello()">Click me</button>
```

```typescript
export class AppComponent {
  sayHello() {
    alert('Hello, World!')
  }
}
```

- When the button is clicked, the `sayHello()` method is executed, displaying an alert message.
