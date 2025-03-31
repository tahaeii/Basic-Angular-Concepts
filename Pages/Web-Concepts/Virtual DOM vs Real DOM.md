# Virtual DOM vs Real DOM

## What is Real DOM?

The **Real DOM (Document Object Model)** is the standard tree structure used by browsers to render and manage HTML elements. Any change made to it is immediately reflected in the UI. However, updating the Real DOM can be expensive because each modification triggers **Reflow** and **Repaint**, which can impact performance.

## What is Virtual DOM?

The **Virtual DOM** is a lightweight, optimized copy of the Real DOM that is stored in memory. In frameworks like **React**, changes are first applied to the Virtual DOM and then compared (Diffing) with its previous version. Finally, only the modified parts of the Real DOM are updated, improving performance in certain scenarios.

---

### Why is Virtual DOM Essential in React?

React is a **declarative framework**, meaning that instead of directly instructing how to modify the DOM, developers define what the UI should look like.

- When data changes, **React rebuilds the entire Virtual DOM** and then compares it with the previous version using the **Diffing Algorithm**.
- Only the modified parts of the Real DOM are updated, preventing unnecessary re-renders.

**Trade-offs of Virtual DOM:**

- While this method improves efficiency by reducing direct DOM manipulations, it has an overhead: creating a new Virtual DOM and executing the Diffing Algorithm require additional processing power.

---

### Why is Real DOM Essential in Angular?

Angular is a **template-driven framework**, meaning that developers define an **HTML template** bound to **TypeScript variables (Data Binding)**.

- Unlike React, where the entire Virtual DOM is checked for differences, Angular directly **monitors the values of variables bound to the UI**.
- During each **Change Detection Cycle**, Angular checks only the variables used in the template and updates **only the affected parts of the Real DOM**.
- This approach eliminates the need for full-tree diffing since **Angular knows exactly which variables are bound to the UI**.

Thus, while React optimizes UI updates using Virtual DOM, **Angular efficiently updates Real DOM based on precise data bindings**.
