# Custom Directives in Angular

Sometimes, we need to add **custom behaviors** to elements that are **not available** in built-in directives. This is where **custom directives** come in handy.

---

## Example: A Directive to Change Text Color on Hover

### Creating the Directive (`highlight.directive.ts`)

```typescript
import { Directive, ElementRef, Renderer2, HostListener } from '@angular/core'

@Directive({
  selector: '[appHighlight]'
})
export class HighlightDirective {
  constructor(private el: ElementRef, private renderer: Renderer2) {}

  @HostListener('mouseenter') onMouseEnter() {
    this.renderer.setStyle(this.el.nativeElement, 'color', 'blue')
  }

  @HostListener('mouseleave') onMouseLeave() {
    this.renderer.setStyle(this.el.nativeElement, 'color', 'black')
  }
}
```

---

### Using the Directive in HTML

```html
<p appHighlight>Hover over this text to change its color</p>
```

On **hover (`mouseenter`)**, the text **turns blue**.  
On **leaving (`mouseleave`)**, the text **returns to its original color**.
