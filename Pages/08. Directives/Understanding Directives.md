# What is a Directive in Angular?

**Directives** in Angular are elements that can modify the behavior of an element, component, or other directives. They allow us to create **dynamic and controllable HTML**.

---

## Types of Directives in Angular

Directives are categorized into **three types**:

1. **[Structural Directives](structural-directives.md)** - Modify the **DOM structure**.
2. **[Attribute Directives](attribute-directives.md)** - Modify the **appearance or behavior** of an element.
3. **[Custom Directives](custom-directives.md)** - User-defined directives created by developers.

---

## Example: Using `ngClass` (an Attribute Directive)

**HTML:**

```html
<p [ngClass]="{'active': isActive, 'inactive': !isActive}">
  This is a paragraph
</p>
```

**TypeScript:**

```typescript
isActive = true
```

This directive **adds or removes** the `active` class based on the value of `isActive`.
