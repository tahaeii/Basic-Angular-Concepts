# What Are Pipes in Angular?

Pipes are one of **Angular’s powerful features** used to **process and format data** before displaying it in the UI. They allow us to present data in **a more readable format** within an HTML template **without modifying the data directly in components**.

In simple terms, a **Pipe in Angular** is a **transformation function** that takes an **input value**, processes it, and returns a **new formatted value**.  
Pipes are commonly used in **Interpolation (`{{ }}`)** and **Property Binding**.

---

## Why Use Pipes in Angular?

**Improves Code Readability** – Instead of writing complex functions in HTML, we use a Pipe.  
**Makes Code Simpler and Cleaner** – Processing tasks like date formatting, currency display, etc., become easier.  
**Reusability** – A Pipe can be used across multiple components.  

---

## How to Use Pipes in Angular?
Pipes in Angular are used with the `|` (pipe) operator.  

For example, to convert a text to uppercase:  

```html
<p>{{ 'hello world' | uppercase }}</p>  <!-- Output: HELLO WORLD -->
```  

---

## Types of Pipes in Angular

Angular provides **two types** of Pipes:  

1. **[Built-in Pipes](built-in-pipes.md)** - Predefined Pipes provided by Angular.  
2. **[Custom Pipes](custom-pipes.md)** - Pipes that we define ourselves.  

---  

## Key Points About Pipes

**Pipes do not modify the original value**; they return a new transformed value.  
**Multiple Pipes can be chained together** for advanced processing.  
**Custom Pipes must be added to the module’s `declarations` section** before use.  