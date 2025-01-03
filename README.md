# Clean Architecture

---

## **Core Principles**

1. **Separation of Concerns**  
   Different parts of the system (business logic, UI, database) are isolated in separate layers.

2. **Dependency Inversion Principle (DIP)**  
   - High-level modules (business logic) should not depend on low-level modules (infrastructure); both should depend on abstractions.
   - Abstractions should not depend on details; details should depend on abstractions.

3. **Layered Architecture**  
   The architecture is divided into concentric layers with dependencies pointing inwards:
   - **Entities (Core Domain Layer)** – Contains business rules and domain models.
   - **Use Cases (Application Layer)** – Contains application-specific business logic.
   - **Interface Adapters** – Translates data between the core application and external systems (UI, DB, etc.).
   - **Infrastructure** – Implements persistence, third-party integrations, etc.

---

---
## **Clean Architecture - Layered Structure**

---

## **Domain Layer**

- Core business logic  
- No dependencies on other projects  
- Contains entities, interfaces, and domain events

---

## **Application Layer**

- Application logic and use cases  
- Depends only on Domain layer  
- Implements the **CQRS** pattern

---

## **Infrastructure Layer**

- Technical implementations  
- Database context and migrations  
- External service implementations

---

## **API Layer**

- HTTP endpoints  
- Middleware configurations  
- API-specific concerns

---

## **Tests Project**

- Mirrors the main project structure  
- Separate test projects for each layer  
- Integration tests in `API.Tests`

## **Layer Responsibilities**

- **Entities**  
  Represent the core business logic and rules.  
  These are independent and reusable across different applications.

- **Use Cases**  
  Orchestrate the flow of data to and from entities.  
  Implement application-specific business rules (e.g., creating or retrieving an order).

- **Interfaces (Driven Adapters)**  
  Define abstractions for interacting with external components (e.g., repositories, external services).
  
- **Infrastructure (Drivers)**  
  Implements interfaces for interacting with external systems (databases, APIs, etc.).  
  This layer can be replaced without affecting the core logic.

---

## **Flow of Control**

1. The **Use Case** initiates an action, such as creating a new order.
2. The use case calls a method on the **Repository Interface** (e.g., `IOrderRepository.AddOrder`).
3. The **Repository Interface** is implemented by a concrete class in the **Infrastructure Layer** (e.g., `OrderRepository`).
4. The concrete repository interacts with the database (via ORM, SQL commands, etc.) and returns data.
5. The returned data flows back through the use case to the controller or presenter.

## **Benefits**

1. **Testability**  
   Business rules and use cases can be tested independently by mocking interfaces.
   
2. **Flexibility**  
   Infrastructure can be changed (e.g., switching databases) with minimal impact on the application.

3. **Maintainability**  
   Clear separation of concerns makes the codebase easier to maintain and evolve.

4. **Scalability**  
   Facilitates horizontal scaling by allowing independent deployment of components.

---

## **Common Patterns Used**

1. **Repository Pattern**  
   Used to abstract persistence logic from the core business logic.
   
2. **Dependency Injection (DI)**  
   Used to inject concrete implementations of interfaces at runtime.

3. **Command Query Responsibility Segregation (CQRS)**  
   Separates read (query) and write (command) operations into different models.
   
4. **Event-Driven Architecture**  
   Use of events for decoupling different parts of the system.

---

## **Interview Questions (Sample)**

1. **What is Clean Architecture, and why is it important?**  
   Clean Architecture provides a way to organize code with a clear separation of concerns, ensuring that the core business logic is independent of external systems like databases, UI, and frameworks.

2. **How do you ensure Dependency Inversion in Clean Architecture?**  
   By depending on abstractions (interfaces) and providing concrete implementations in the infrastructure layer.

3. **What are the key differences between Entities and Use Cases in Clean Architecture?**  
   - **Entities** represent core business models and rules that are independent of the application.  
   - **Use Cases** represent application-specific logic and orchestrate tasks involving entities.

4. **How would you implement persistence in Clean Architecture?**  
   Define repository interfaces in the application layer and implement them in the infrastructure layer.

5. **What is the role of Interface Adapters in Clean Architecture?**  
   They act as a bridge between the application layer and external systems (UI, database, APIs) by converting data formats.

---

## **Common Mistakes**

1. **Tight Coupling of Layers**  
   Directly depending on infrastructure details (e.g., database) in the application layer.

2. **Placing Business Logic in the Infrastructure Layer**  
   Business logic should reside in the core and use case layers, not in controllers or repositories.

3. **Ignoring Dependency Inversion**  
   Failing to use abstractions (interfaces) can lead to a rigid and hard-to-maintain architecture.

---

## **Comparison with Other Architectures**

| Aspect                  | Clean Architecture                | Layered Architecture               | Hexagonal Architecture             |
|-------------------------|-----------------------------------|-----------------------------------|------------------------------------|
| **Dependency Direction** | Always inward towards core        | Layer to layer (downward)          | Inward towards core                |
| **Core Isolation**       | Core is fully isolated            | Core may depend on other layers    | Core is fully isolated             |
| **Testability**          | High (core is independent)        | Moderate (some coupling)           | High (core is independent)         |
| **Flexibility**          | High (easily swap infrastructure) | Moderate                           | High                               |

---

## **Summary**

- Clean Architecture is about creating systems that are **independent of frameworks, databases, and UI**, ensuring that the core logic is reusable and testable.
- It enforces **Dependency Inversion** by making high-level modules depend on abstractions rather than concrete implementations.
- Each layer has a well-defined responsibility, and the infrastructure layer can be swapped out with minimal changes to the core logic.
- Focus on defining **interfaces in the core layers** and implementing them in the infrastructure layer.
- Emphasize the benefits of **testability, maintainability, and scalability**.


