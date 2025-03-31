# Built-in Pipes in Angular

Angular provides a set of **built-in pipes** to format data efficiently. Below are some of the most commonly used ones:

## 1. uppercase & lowercase

Convert text to **uppercase** or **lowercase**

```html
<p>{{ 'hello world' | uppercase }}</p>  <!-- Output: HELLO WORLD -->
<p>{{ 'HELLO WORLD' | lowercase }}</p>  <!-- Output: hello world -->
```

## 2. titlecase

Capitalize the **first letter** of each word

```html
<p>{{ 'angular is awesome' | titlecase }}</p>   <!-- Output: Angular Is Awesome -->
```

## 3. date

Format dates in different styles

```html
<p>{{ today | date: 'short' }}</p>  <!-- Output: 3/2/25 -->
<p>{{ today | date: 'fullDate' }}</p>   <!-- Output: Sunday, March 2, 2025 -->
```

## 4. currency

Format numbers as **currency**

```html
<p>{{ 2500 | currency:'USD' }}</p>
<!-- Output: $2,500.00 -->
<p>{{ 2500 | currency:'EUR' }}</p>
<!-- Output: €2,500.00 -->
```

## 5. percent

Convert a number to **percentage**

```html
<p>{{ 0.75 | percent }}</p> <!-- Output: 75% -->
```

## 6. json

Display an object in **readable JSON format**

```html
<p>{{ user | json }}</p>
```

```typescript
user = { name: 'Ali', age: 25 }
```

**Output:**

```json
{
  "name": "Ali",
  "age": 25
}
```

## 7. slice

Extract a portion of an **array or string**

```html
<p>{{ [1,2,3,4,5] | slice:1:3 }}</p>    <!-- Output: [2,3] -->
```
