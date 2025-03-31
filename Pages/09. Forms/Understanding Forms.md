# What Are Forms in Angular?
Forms are one of the **core components** of any web application, allowing users to interact with the system. Through forms, users can enter and submit information such as **name, email, messages, passwords**, and more.  

Angular provides **two main approaches** for working with forms:  

1. **[Template-driven Forms](template-driven-forms.md)**
2. **[Reactive Forms](reactive-forms.md)**

---  
## Difference Between Template-driven and Reactive Forms

| Feature               | Template-driven Forms      | Reactive Forms               |
|-----------------------|--------------------------|------------------------------|
| **Logic Definition**  | In HTML (`ngModel`)      | In TypeScript (`FormGroup`)  |
| **Complexity**        | Simple and lightweight   | Advanced and flexible        |
| **Data Control**      | Low (direct UI binding)  | High (centralized in TS)     |
| **Best for**          | Simple forms             | Large and complex forms      |
| **Validation**        | Basic, defined in HTML   | Flexible, defined in TS      |  

**Choose the right approach** based on the complexity and scalability of your form requirements!