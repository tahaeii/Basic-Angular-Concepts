# Custom Pipes in Angular

Sometimes, we need to create a **custom Pipe** for specific data transformations, such as converting text into a **custom format**.

---

## 1. Creating a Custom Pipe

Pipes in Angular are simple **TypeScript classes** that implement `PipeTransform`.

### 1.1 Creating a Pipe to Reverse a Text

```typescript
import { Pipe, PipeTransform } from '@angular/core'

@Pipe({
  name: 'reverse'
})
export class ReversePipe implements PipeTransform {
  transform(value: string): string {
    return value.split('').reverse().join('')
  }
}
```

### 1.2 Adding the Pipe to a Module

```typescript
import { NgModule } from '@angular/core'
import { ReversePipe } from './reverse.pipe'

@NgModule({
  declarations: [ReversePipe],
  exports: [ReversePipe]
})
export class SharedModule {}
```

### 1.3 Using the Pipe in an HTML Template

```html
<p>{{ 'Hello Angular' | reverse }}</p>  <!-- Output: ralugnA olleH -->
```

---

## 2. Pipe with Input Arguments

We can create Pipes that accept **parameters**:

```typescript
@Pipe({ name: 'repeat' })
export class RepeatPipe implements PipeTransform {
  transform(value: string, times: number): string {
    return value.repeat(times)
  }
}
```

```html
<p>{{ 'Hello' | repeat:3 }}</p> <!-- Output: HelloHelloHello -->
```

---

## 3. Impure Pipe for Arrays and Objects

Sometimes, we need a Pipe that updates when **arrays change dynamically**:

```typescript
@Pipe({
  name: 'filterItems',
  pure: false
  // If pure: true → The Pipe runs only when the input value changes. (Default)
  // If pure: false → The Pipe runs every time Angular detects changes, even if the value remains the same.
})
export class FilterPipe implements PipeTransform {
  transform(items: any[], searchText: string): any[] {
    return items.filter(item => item.includes(searchText))
  }
}
```

```html
<p *ngFor="let item of items | filterItems:'Angular'">{{ item }}</p>
```
