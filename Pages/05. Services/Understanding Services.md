# What is a Service in Angular?  
Services in Angular are **classes** responsible for managing **data** and **business logic**. They help components **avoid repetitive code** by handling tasks like fetching data from an API, processing information, and managing application state.  

## Why Use Services?  
**Separation of Business Logic:** HTTP requests and data processing are handled in services, allowing components to focus only on displaying data.  
**Reusability:** Services can be used across multiple components.  
**Performance Optimization:** Through **Dependency Injection (DI)**, Angular efficiently manages and optimizes service instances.  

## Simple Example of a Service  
```typescript
export class LoggerService {
  log(message: string) {
    console.log(`[LOG]: ${message}`);
  }
}
```  
Here, we have a simple **LoggerService** that logs messages to the console. Now, we need to use this service in components.