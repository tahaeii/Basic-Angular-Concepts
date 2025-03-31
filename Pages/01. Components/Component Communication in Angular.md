# Communication Between Components in Angular

In real-world projects, components often need to communicate with each other. In Angular, this communication can be established in several ways, depending on whether the components have a parent-child relationship or are unrelated.

---

## Methods of Component Communication

| Method         | Description                                           | Communication Direction      |
|--------------|-------------------------------------------------|------------------|
| `@Input()`  | Sends data from the parent to the child component. | Parent → Child  |
| `@Output()` | Sends data from the child to the parent component. | Child → Parent  |
| `ViewChild()` | Allows the parent to access the child’s methods and properties. | Parent → Child (direct) |
| Service & RxJS | Enables communication between unrelated components. | Between independent components |

---

## 1. Parent-to-Child Communication with `@Input()`
**Using `@Input()` to pass data from parent to child**  
`@Input()` is used to send data from the parent component to the child component.

### **Example:**
### **Parent Component**
```html
<app-child [message]="parentMessage"></app-child>
```
```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-parent',
  templateUrl: './parent.component.html'
})
export class ParentComponent {
  parentMessage = 'Hello from Parent!';
}
```
### **Child Component**
```html
<p>Received from parent: {{ message }}</p>
```
```ts
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-child',
  templateUrl: './child.component.html'
})
export class ChildComponent {
  @Input() message: string = ''; // Receiving value from the parent
}
```
**Result:** `parentMessage` is passed from the parent to the child and displayed.

---

## 2. Child-to-Parent Communication with `@Output()` and `EventEmitter`
Sometimes, the child component needs to send data to the parent. This is done using `@Output()` and `EventEmitter`.

### **Example:**
### **Child Component**
```html
<button (click)="sendMessage()">Send message to parent</button>
```
```ts
import { Component, EventEmitter, Output } from '@angular/core';

@Component({
  selector: 'app-child',
  templateUrl: './child.component.html'
})
export class ChildComponent {
  @Output() messageEvent = new EventEmitter<string>();

  sendMessage() {
    this.messageEvent.emit('Hello from Child!');
  }
}
```
### **Parent Component**
```html
<app-child (messageEvent)="receiveMessage($event)"></app-child>
<p>Message from child: {{ childMessage }}</p>
```
```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-parent',
  templateUrl: './parent.component.html'
})
export class ParentComponent {
  childMessage: string = '';

  receiveMessage(message: string) {
    this.childMessage = message;
  }
}
```
**Result:** When the button is clicked in `ChildComponent`, the message `"Hello from Child!"` is sent to `ParentComponent`.

---

## 3. Direct Parent-to-Child Access with `@ViewChild()`
If the parent needs to access the child’s methods or properties, `@ViewChild()` can be used.

### **Example:**
### **Child Component**
```html
<p>Message from parent: {{ message }}</p>
```
```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-child',
  templateUrl: './child.component.html'
})
export class ChildComponent {
  message: string = '';

  changeMessage(newMessage: string) {
    this.message = newMessage;
  }
}
```
### **Parent Component**
```html
<app-child></app-child>
<button (click)="updateChild()">Change child message</button>
```
```ts
import { Component, ViewChild } from '@angular/core';
import { ChildComponent } from '../child/child.component';

@Component({
  selector: 'app-parent',
  templateUrl: './parent.component.html'
})
export class ParentComponent {
  @ViewChild(ChildComponent) child!: ChildComponent;

  updateChild() {
    this.child.changeMessage('New message from Parent!');
  }
}
```
**Result:** Clicking the button updates the `message` property in the child component.

---

### Note:
If a component contains another component in its **template**, it is a **parent**.
If a component is placed inside another component using its **selector**, it is a **child**.

---

## 4. Communication Between Independent Components Using Services and RxJS
When components are unrelated, a shared service can be used for communication.

### **Creating a Service for Component Communication**
```ts
import { Injectable } from '@angular/core';
import { BehaviorSubject } from 'rxjs';

@Injectable({
  providedIn: 'root'
})
export class DataService {
  private messageSource = new BehaviorSubject<string>('Default Message');
  currentMessage = this.messageSource.asObservable();

  changeMessage(message: string) {
    this.messageSource.next(message);
  }
}
```

### **Sender Component (First Component)**
```html
<input [(ngModel)]="message">
<button (click)="sendMessage()">Send Message</button>
```
```ts
import { Component } from '@angular/core';
import { DataService } from '../data.service';

@Component({
  selector: 'app-sender',
  templateUrl: './sender.component.html'
})
export class SenderComponent {
  message: string = '';

  constructor(private dataService: DataService) {}

  sendMessage() {
    this.dataService.changeMessage(this.message);
  }
}
```

### **Receiver Component (Second Component)**
```html
<p>Received message: {{ message }}</p>
```
```ts
import { Component, OnInit } from '@angular/core';
import { DataService } from '../data.service';

@Component({
  selector: 'app-receiver',
  templateUrl: './receiver.component.html'
})
export class ReceiverComponent implements OnInit {
  message: string = '';

  constructor(private dataService: DataService) {}

  ngOnInit() {
    this.dataService.currentMessage.subscribe(message => this.message = message);
  }
}
```
**Result:** Any change in `SenderComponent` will update `ReceiverComponent` automatically.
