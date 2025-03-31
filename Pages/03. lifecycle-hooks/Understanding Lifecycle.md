# Lifecycle Hooks in Angular  

Every component in **Angular** has a **lifecycle**, which includes different stages such as **creation, updates, and destruction**. The **lifecycle hooks** allow us to execute specific code at the right time, such as when a component is initialized or when an input value changes.  

---

## Lifecycle Stages of a Component  

Angular provides **8 lifecycle hooks** that are executed at different stages of a component's lifecycle:  

| **Method**               | **Description**                                   | **Execution Time**                              |
|-------------------------|-------------------------------------------------|------------------------------------------------|
| `constructor`          | Initializes the class                            | When the component is created                 |
| `ngOnChanges`         | Detects changes in `@Input` properties            | Before and after every input property change  |
| `ngOnInit`            | Runs initialization logic                         | After setting initial values                  |
| `ngDoCheck`          | Manually checks for changes                        | After every change detection cycle            |
| `ngAfterContentInit`  | Executes after `ng-content` initialization        | After projected content is inserted           |
| `ngAfterContentChecked` | Runs after content changes are checked          | After every change detection cycle for content |
| `ngAfterViewInit`     | Executes after the component's view is initialized | After `ViewChild` elements are initialized    |
| `ngAfterViewChecked`  | Runs after view changes are checked               | After every change detection cycle for the view |
| `ngOnDestroy`         | Cleans up before the component is destroyed       | Right before the component is removed         |

---

## Execution Order of Lifecycle Hooks  

The execution order of these methods is:  

```
constructor → ngOnChanges → ngOnInit → ngDoCheck → ngAfterContentInit → 
ngAfterContentChecked → ngAfterViewInit → ngAfterViewChecked → ngOnDestroy
```

---

## Practical Example of Lifecycle Hooks  

The following example logs messages to the console at each lifecycle stage:  

```typescript
import { Component, Input, OnChanges, OnInit, DoCheck, AfterContentInit, 
         AfterContentChecked, AfterViewInit, AfterViewChecked, OnDestroy } from '@angular/core';

@Component({
  selector: 'app-lifecycle',
  template: `<p>Lifecycle works! Input: {{ data }}</p>`
})
export class LifecycleComponent implements OnInit, OnChanges, DoCheck, AfterContentInit, 
                                         AfterContentChecked, AfterViewInit, AfterViewChecked, OnDestroy {

  @Input() data: string = '';

  constructor() {
    console.log('constructor: Component created');
  }

  ngOnChanges() {
    console.log('ngOnChanges: @Input value changed');
  }

  ngOnInit() {
    console.log('ngOnInit: Initialization completed');
  }

  ngDoCheck() {
    console.log('ngDoCheck: Change detection running');
  }

  ngAfterContentInit() {
    console.log('ngAfterContentInit: ng-content initialized');
  }

  ngAfterContentChecked() {
    console.log('ngAfterContentChecked: ng-content changes checked');
  }

  ngAfterViewInit() {
    console.log('ngAfterViewInit: View initialized');
  }

  ngAfterViewChecked() {
    console.log('ngAfterViewChecked: View changes checked');
  }

  ngOnDestroy() {
    console.log('ngOnDestroy: Component is being destroyed');
  }
}
```

### Using the Component in a Parent Component  

```html
<app-lifecycle [data]="message"></app-lifecycle>
<button (click)="message = 'Hello Angular'">Change Value</button>
```

```typescript
export class AppComponent {
  message = 'Welcome!';
}
```

---

## Common Use Cases of Lifecycle Hooks  

**`ngOnInit`** → Initialize variables and fetch data from an API  
**`ngOnChanges`** → Detect and respond to changes in `@Input` values  
**`ngDoCheck`** → Manually track changes that Angular does not detect automatically  
**`ngOnDestroy`** → Clean up resources such as timers, subscriptions, and event listeners to prevent memory leaks