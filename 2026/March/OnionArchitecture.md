# Onion Architecture 

(also known as Clean Architecture), a software design pattern where dependencies flow inward toward a central Domain layer. 
This structure ensures that the core business logic remains independent of external concerns like databases or user interfaces.

## Core Layers and Components
### Domain (The Core): 
The innermost circle containing business entities and state. It is fully independent of all other layers.

### Application: Surrounds the Domain and coordinates system behavior through use cases and application-specific logic. It depends only on the Domain.

### Outer Infrastructure Layers:
#### Presentation: Handles user interaction (e.g., Web API, MVC, or mobile app).
#### Persistence: A part of the infrastructure responsible for data storage and retrieval (e.g., database operations).
#### Infrastructure: Manages external system access and third-party integrations. 




