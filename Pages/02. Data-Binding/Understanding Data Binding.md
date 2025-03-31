# Data Binding in Angular

**Data Binding** in Angular is a technique that allows you to synchronize data between a component and its template (HTML). This concept ensures that your data is automatically displayed in the UI and dynamically updated when changes occur.  

Angular provides **four types** of data binding:

| **Type**             | **Syntax**            | **Description**                                                  |
| -------------------- | --------------------- | ---------------------------------------------------------------- |
| **Interpolation**    | `{{ value }}`         | Displays a variable's value in HTML.                             |
| **Property Binding** | `[property]="value"`  | Binds a variable to an HTML element property.                    |
| **Event Binding**    | `(event)="method()"`  | Calls a method when an event occurs.                             |
| **Two-way Binding**  | `[(ngModel)]="value"` | Creates a two-way binding between a variable and an input field. |

