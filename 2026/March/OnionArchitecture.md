# Onion Architecture 

(also known as Clean Architecture), a software design pattern where dependencies flow inward toward a central Domain layer. 
This structure ensures that the core business logic remains independent of external concerns like databases or user interfaces.

<img width="396" height="392" alt="image" src="https://github.com/user-attachments/assets/0f7e418c-b5cd-4839-9f29-7b65cb1aea60" />

## Core Layers and Components
### Domain (The Core): 
The innermost circle containing business entities and state. It is fully independent of all other layers.

### Application: Surrounds the Domain and coordinates system behavior through use cases and application-specific logic. It depends only on the Domain.

### Outer Infrastructure Layers:
#### Presentation: Handles user interaction (e.g., Web API, MVC, or mobile app).
#### Persistence: A part of the infrastructure responsible for data storage and retrieval (e.g., database operations).
#### Infrastructure: Manages external system access and third-party integrations. 

## Key Design Principles
### Inward Dependencies: Every layer only knows about the layers inside it. For example, the Persistence layer can depend on the Domain, but the Domain cannot depend on Persistence.
### Dependency Inversion: Interfaces are defined in inner layers, while their concrete implementations (like specific database code) are placed in outer layers.
### High Testability: Because the core has no external dependencies, it can be easily unit-tested without needing a live database or UI.
### Technology Agnostic: You can swap external technologies (e.g., switching from SQL to MongoDB) without changing the core business logic.

## A persistence layer
A persistence layer is a software abstraction layer that manages the storage, retrieval, and modification of data, allowing it to exist beyond an application's lifecycle, usually via a database. It acts as a bridge between the business logic and data storage, typically implementing CRUD operations and translating between in-memory objects and database rows. 

### Key aspects of the persistence layer include:
Abstraction: 
It hides the complexity of SQL queries and specific database technologies from the business logic.

Data Access Layer (DAL): Often referred to as a DAL, it decouples the application from the underlying storage mechanism.

Components: It involves techniques like ORMs (Object-Relational Mapping), DAO (Data Access Objects), or Repository patterns.

Key Functions:
It handles data integration, transaction management, caching, and ensuring data consistency.
Benefits: 
It enhances maintainability, testability, and readability by separating data access logic from core application logic. 

Common implementations include using Java Persistence API (JPA)****Spring Data JPA, or Hibernate in Java applications.
Also EF

