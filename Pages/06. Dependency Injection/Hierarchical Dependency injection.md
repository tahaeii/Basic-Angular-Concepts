# Hierarchical Dependency Injection

In Angular, dependency injection follows a **hierarchical** structure.  
This means that each level (**Module, Component, Directive**) can have its own separate instance of a service.

---

## Hierarchical Injector Structure in Angular

```
Root Injector (Application-wide)
│── Feature Module Injector (Module-level)
│   │── Component Injector (Component-level)
│   │   │── Directive Injector (Directive-level)
```

---

## Example 1: Registering a Service at the Root Level

If a service is registered using `providedIn: 'root'`, only a **single** instance (Singleton) of it exists throughout the entire application.

```typescript
@Injectable({
  providedIn: 'root'
})
export class GlobalService {}
```

### Result:

All components will share the **same instance** of `GlobalService`.

---

## Example 2: Registering a Service in a Specific Module

If a service is registered inside a **feature module**, it will only be available within that module.

```typescript
@NgModule({
  providers: [FeatureService]
})
export class FeatureModule {}
```

### Result:

Components from other modules will **not** have access to this service.

---

## Example 3: Registering a Service at the Component Level

If a service is registered inside a **component**, it will only be available within that component and its child components in the **View Tree**.

```typescript
@Component({
  selector: 'app-child',
  providers: [ChildService]
})
export class ChildComponent {}
```

### Result:

Each time `ChildComponent` is created, **a new instance** of `ChildService` will be instantiated.
