# What is Change Detection in Angular?

**Change Detection** in Angular is one of the most important mechanisms for updating the UI. It determines when and how component data changes should be detected and reflected in the user interface (**DOM**).

Simply put, when a component's data changes, Angular automatically checks for updates and, if necessary, updates the **DOM**. This process is managed by the **Change Detection Mechanism**.

**Read [this](../Web-Concepts/virtual-dom-vs-real-dom.md) to better understand how change detection works in Angular.**

---

## How is Change Detection Executed in Angular?

Whenever an **event** occurs in the application, **Angular triggers the Change Detection process**.  
This process consists of **three main steps**:

### Step 1: Detecting Events (Triggering Change Detection)

Change Detection is triggered when any of the following events occur:

1. A **UI event** happens (e.g., clicking a button or changing an input field).  
2. An **HTTP request** completes, receiving new data from the server.  
3. A **setTimeout** or **setInterval** executes.  
4. A **Promise** or **Observable** emits a new value.  
5. A **direct change** occurs in the application's data model.

| **Category**                                         | **Common Examples**                         | **Explanation**                                           |
| ---------------------------------------------------- | ------------------------------------------- | --------------------------------------------------------- |
| **User Events**                                   | `click`, `input`, `scroll`                  | When the user interacts with the UI.                      |
| **Direct Data Changes**                           | Changing a variable or array value          | A direct change in a variable triggers Change Detection.  |
| **Receiving Data from Promises/Observables/HTTP** | `HttpClient.get()`, `Promise.resolve()`     | When new data is received from a server or an Observable. |
| **Timers (`setTimeout`, `setInterval`)**          | Executing delayed code                      | Each time a timer executes, Change Detection runs.        |
| **Manually Triggering Change Detection**          | `detectChanges()`, `detach()`, `reattach()` | Manually controlling Change Detection in components.      |

**How does Angular detect these changes?**  
Angular **uses Zone.js** to track all of these events.

---

### Step 2: Executing Change Detection in the Component Tree

When Angular detects an event, it runs **Change Detection** across all components.

**How is the component tree checked?**

- Angular starts **from the root component** and traverses down the tree.
- Each component is checked to see if its data has changed.
- If a change is detected, the new value is rendered in the **DOM**.

**This process follows the "dirty checking" algorithm:**

- The new value is **compared** with the previous value.
- If they are different, **the change is applied**.

---

### Step 3: Updating the DOM if a Change is Found

If Change Detection detects a change:  
**The new value is applied to the DOM.**  
**Components that haven’t changed remain untouched.**

**However, there's a performance issue!**  
By default, **Angular checks all components**, even if no changes occurred! The next section will explain **[how to optimize this process](change-detection-strategies.md)**.

---

## Example: Change Detection in Action

Suppose we have a component that displays a counter and updates its value on button click.

### Code: Running Change Detection in a Simple Example

```typescript
@Component({
  selector: 'app-counter',
  template: `
    <button (click)="increase()">Increase</button>
    <p>Count: {{ count }}</p>
  `
})
export class CounterComponent {
  count = 0

  increase() {
    this.count++
  }
}
```

**What Happens When We Click the Button?**

1. The **increase()** method executes and increments `count`.  
2. Angular **detects the event**.  
3. The **Change Detection process runs**, and the updated value appears in the **DOM**.
