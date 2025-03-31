# What Are Providers in Angular?

In Angular, **providers** determine how a **dependency** is created and managed.  
Every service that is injected into **Dependency Injection (DI)** must have a provider that specifies how Angular should instantiate it.

---

## Defining Providers in Angular

There are three main ways to define a provider in Angular:

### Using `providedIn: 'root'`

This method is specified inside the `@Injectable()` decorator, making the service **globally available** as a **singleton** throughout the application.

```typescript
@Injectable({
  providedIn: 'root' // This service is created only once for the entire application
})
export class MyService {}
```

#### Advantages:

- No need to register the service inside `providers: []` in modules.
- **Lazy Loading:** The service is only instantiated when needed.

---

### Registering the Provider in a Module or Component

This method allows **scoped** registration of the service.

#### Registering at the Module Level:

```typescript
@NgModule({
  providers: [MyService] // This service is available only within this module
})
export class AppModule {}
```

#### Registering at the Component Level:

```typescript
@Component({
  selector: 'app-home',
  providers: [MyService] // This service is available only in this component and its children
})
export class HomeComponent {}
```

#### Differences:

- If a service is registered at the **module level**, all components in that module can use it.
- If a service is registered at the **component level**, a **new instance** of the service is created for each instance of the component.

---

### Using Injection Tokens (For Special and More Complex Cases)

Sometimes, instead of injecting **service classes**, we need to inject a specific **value** into DI. This is where **Injection Tokens** come in.

#### Creating an Injection Token:

```typescript
import { InjectionToken } from '@angular/core'

export const API_URL = new InjectionToken<string>('apiUrl')
```

#### Providing the Value in a Module:

```typescript
@NgModule({
  providers: [{ provide: API_URL, useValue: 'https://api.example.com' }]
})
export class AppModule {}
```

#### Injecting the Value in a Service:

```typescript
import { Inject, Injectable } from '@angular/core'
import { API_URL } from './tokens'

@Injectable({
  providedIn: 'root'
})
export class ApiService {
  constructor(@Inject(API_URL) private apiUrl: string) {}

  getApiUrl(): string {
    return this.apiUrl
  }
}
```

#### Why Use Injection Tokens?

- Necessary for injecting **non-class values** like **strings, arrays, functions, or objects**.
- **Better than global variables** since it still benefits from **Dependency Injection**.
