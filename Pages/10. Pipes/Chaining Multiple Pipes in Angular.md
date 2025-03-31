# Chaining Multiple Pipes in Angular

In some cases, we may want to **chain multiple Pipes** to process data sequentially.  
Angular allows **combining multiple Pipes** within **Interpolation (`{{ }}`) or Property Binding**.  

To chain Pipes, **separate them using** `|` (pipe operator).  

**For Example:**
Combining `uppercase` and `slice` Pipes

```html
<p>{{ 'hello world' | uppercase | slice:0:5 }}</p> <!-- Output: HELLO -->
```
