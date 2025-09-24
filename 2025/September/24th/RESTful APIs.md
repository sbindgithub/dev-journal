# REST API Summary  

## Background  
- REST (**Representational State Transfer**) was introduced by **Roy Fielding** in his PhD dissertation (2000).  
- It is an **architectural style** for designing networked applications.  
- Core idea: A **server hosts resources** (data), and a **client requests representations** of those resources.  

## Why REST Matters  
- REST popularized trends like **cloud computing** and **microservices-based architecture**.  
- REST APIs are widely used due to **simplicity, flexibility, and scalability**.  

---

## What is REST?  
- REST is a **pattern for building APIs** using web standards.  

## What is a REST API?  
- A REST API allows **applications to communicate and exchange data** over HTTP.  
- Based on **open standards**, consumable by:  
  - Web browsers  
  - Mobile apps  
  - Desktop apps  
  - IoT devices  

---

## REST Constraints (must follow for true RESTfulness)  
1. **Client–Server**: Separation of concerns between UI (client) and data (server).  
2. **Stateless**: Each request contains all necessary information (no session storage on server).  
3. **Cacheable**: Responses must define whether they are cacheable to improve performance.  
4. **Uniform Interface**:  
   - Each resource is identified by a **unique URI**.  
   - Example:  
     ```  
     http://pragimtech.com/api/products
     ```  
     - Protocol → `http`  
     - Domain → `pragimtech.com`  
     - Optional → `/api`  
     - Endpoint → `/products`  

---

## REST vs SOAP  

| **Aspect**          | **SOAP** (Protocol)                           | **REST** (Architectural Style)                |
|----------------------|-----------------------------------------------|-----------------------------------------------|
| Full Form           | Simple Object Access Protocol                 | Representational State Transfer               |
| Nature              | Strict protocol                               | Flexible design pattern                       |
| Communication       | XML only                                      | Multiple formats (JSON, XML, plain text, etc.)|
| Coupling            | Tightly coupled (strict contracts)            | Loosely coupled (flexible like browsers)      |
| Performance         | Slower (heavy XML & overhead)                 | Faster (lightweight, often JSON-based)        |
| Caching             | Not cacheable                                 | Read requests can be cached                   |
| Security            | Built-in (WS-Security)                        | Inherits from underlying protocol (e.g. HTTPS)|
| Use Cases           | Financial apps, reliable messaging, ACID ops  | Web, mobile, microservices, IoT               |
| Popularity          | Less common today                             | Dominant for modern APIs                      |

---

## Conclusion  
- REST can be taught alone, but mentioning SOAP makes the contrast clear and shows **why REST is widely preferred today**.  
- If your audience is **completely new**, keep SOAP as a **side note**.  
- If they are **IT students or developers**, include a REST vs SOAP section.  

----

## MCQ 1

Which of the following is NOT a REST constraint?

A. Client-Server
B. Stateless
C. Cacheable
D. Persistent Connection

