# Software Architecture Reference Sheet

## Architectural Principles

### SOLID Principles
1. **Single Responsibility Principle (SRP)**
   - A class should have only one reason to change
   - Each class should handle one specific functionality
   ```python
   # Good
   class UserAuthentication:
       def authenticate(self, credentials):
           pass

   class UserRepository:
       def save(self, user):
           pass
   ```

2. **Open/Closed Principle (OCP)**
   - Software entities should be open for extension but closed for modification
   ```python
   class Shape(ABC):
       @abstractmethod
       def area(self):
           pass

   class Rectangle(Shape):
       def area(self):
           return self.width * self.height
   ```

3. **Liskov Substitution Principle (LSP)**
   - Derived classes must be substitutable for their base classes
   ```python
   def process_shape(shape: Shape):
       # Should work with any Shape subclass
       return shape.area()
   ```

4. **Interface Segregation Principle (ISP)**
   - Clients shouldn't depend on interfaces they don't use
   ```python
   class Printer(ABC):
       @abstractmethod
       def print(self):
           pass

   class Scanner(ABC):
       @abstractmethod
       def scan(self):
           pass
   ```

5. **Dependency Inversion Principle (DIP)**
   - High-level modules shouldn't depend on low-level modules
   ```python
   class DataStore(ABC):
       @abstractmethod
       def store(self, data):
           pass

   class BusinessLogic:
       def __init__(self, data_store: DataStore):
           self.data_store = data_store
   ```

### Other Key Principles
1. **DRY (Don't Repeat Yourself)**
   - Avoid code duplication
   - Extract common functionality

2. **KISS (Keep It Simple, Stupid)**
   - Favor simple solutions
   - Avoid unnecessary complexity

3. **YAGNI (You Aren't Gonna Need It)**
   - Only implement features when needed
   - Avoid speculative functionality

4. **Separation of Concerns**
   - Divide system into distinct features
   - Minimize overlap between components

## Architectural Patterns

### Layered Architecture
```plaintext
┌─────────────────┐
│ Presentation    │
├─────────────────┤
│ Business Logic  │
├─────────────────┤
│ Data Access     │
└─────────────────┘
```
- **Components:**
  - Presentation Layer (UI)
  - Business Layer (Logic)
  - Data Access Layer (Storage)
- **Benefits:**
  - Clear separation
  - Easy maintenance
  - Independent development
- **Use Cases:**
  - Enterprise applications
  - Web applications
  - Desktop applications

### Microservices Architecture
```plaintext
┌──────────┐ ┌──────────┐ ┌──────────┐
│ Service A│ │ Service B│ │ Service C│
└──────────┘ └──────────┘ └──────────┘
      │            │            │
      └────────────┼────────────┘
                   │
            API Gateway/Bus
```
- **Characteristics:**
  - Independent services
  - Decentralized data
  - Service discovery
- **Benefits:**
  - Scalability
  - Technology diversity
  - Independent deployment
- **Challenges:**
  - Distributed system complexity
  - Data consistency
  - Service coordination

### Event-Driven Architecture
```plaintext
┌─────────┐    ┌───────────┐    ┌─────────┐
│Publisher│ -> │Event Bus  │ -> │Subscriber│
└─────────┘    └───────────┘    └─────────┘
```
- **Components:**
  - Event producers
  - Event consumers
  - Event bus/broker
- **Benefits:**
  - Loose coupling
  - Scalability
  - Flexibility
- **Use Cases:**
  - Real-time systems
  - IoT applications
  - Reactive systems

### Domain-Driven Design (DDD)
```plaintext
┌─────────────┐
│   Domain    │
│   Model     │
├─────────────┤
│ Application │
│  Services   │
├─────────────┤
│Infrastructure│
└─────────────┘
```
- **Key Concepts:**
  - Bounded Contexts
  - Aggregates
  - Value Objects
  - Entities
- **Patterns:**
  - Repository Pattern
  - Factory Pattern
  - Service Pattern

### Clean Architecture
```plaintext
┌────────────────┐
│    Entities    │
├────────────────┤
│  Use Cases     │
├────────────────┤
│  Interface     │
│  Adapters      │
├────────────────┤
│  Frameworks    │
└────────────────┘
```
- **Layers:**
  - Entities (Business objects)
  - Use Cases (Business rules)
  - Interface Adapters
  - Frameworks & Drivers
- **Benefits:**
  - Independence of frameworks
  - Testability
  - Independence of UI
  - Independence of Database

## Infrastructure Patterns

### Cloud Patterns
1. **High Availability**
   ```plaintext
   ┌─────────┐    ┌─────────┐
   │Region A │    │Region B │
   │ ┌───┐   │    │ ┌───┐   │
   │ │LB │   │    │ │LB │   │
   │ └───┘   │    │ └───┘   │
   └─────────┘    └─────────┘
   ```
   - Load balancing
   - Failover
   - Redundancy

2. **Scalability**
   - Horizontal scaling
   - Vertical scaling
   - Auto-scaling

3. **Resilience**
   - Circuit breaker
   - Retry pattern
   - Bulkhead pattern

### Storage Patterns
1. **CQRS (Command Query Responsibility Segregation)**
   ```plaintext
   ┌──────────┐    ┌──────────┐
   │ Commands │    │ Queries  │
   └────┬─────┘    └────┬─────┘
        │               │
   ┌────┴─────┐   ┌────┴─────┐
   │  Write   │   │  Read    │
   │   DB     │   │   DB     │
   └──────────┘   └──────────┘
   ```

2. **Event Sourcing**
   - Store state changes
   - Event log as source of truth
   - Event replay capability

## Security Patterns

### Authentication & Authorization
1. **OAuth 2.0/OpenID Connect**
   ```plaintext
   ┌─────────┐    ┌─────────┐
   │  Client │    │  Auth   │
   │         │<-->│ Server  │
   └─────────┘    └─────────┘
        │              │
        └──────────────┘
   ```

2. **JWT (JSON Web Tokens)**
   - Stateless authentication
   - Token-based security
   - Claims-based identity

### Security Principles
1. **Defense in Depth**
   - Multiple security layers
   - Redundant security controls

2. **Principle of Least Privilege**
   - Minimal access rights
   - Role-based access control

## Integration Patterns

### API Patterns
1. **REST**
   - Resource-based
   - Stateless
   - CRUD operations

2. **GraphQL**
   ```graphql
   type Query {
     user(id: ID!): User
   }
   
   type User {
     id: ID!
     name: String!
     posts: [Post!]!
   }
   ```

3. **gRPC**
   ```protobuf
   service UserService {
     rpc GetUser (UserRequest) returns (User);
   }
   ```

### Message Patterns
1. **Publisher/Subscriber**
   ```plaintext
   ┌────────┐   ┌─────────┐   ┌────────┐
   │Publisher│-->│  Topic  │-->│Subscriber│
   └────────┘   └─────────┘   └────────┘
   ```

2. **Request/Reply**
   - Synchronous communication
   - Response correlation

## Development & Operations

### DevOps Practices
1. **Continuous Integration**
   ```yaml
   pipeline:
     build:
       - compile
       - test
       - package
   ```

2. **Continuous Deployment**
   - Automated deployment
   - Environment promotion
   - Rollback capability

### Monitoring & Observability
1. **Logging**
   ```python
   logger.info("Operation completed", extra={
       "operation_id": id,
       "duration": time
   })
   ```

2. **Metrics**
   - System metrics
   - Business metrics
   - SLIs/SLOs

3. **Tracing**
   - Distributed tracing
   - Request flow tracking
   - Performance analysis

## Architecture Decision Records (ADR)

### Template
```markdown
# Title

## Status
[Proposed, Accepted, Deprecated, Superseded]

## Context
[What is the issue that we're seeing that is motivating this decision?]

## Decision
[What is the change that we're proposing and/or doing?]

## Consequences
[What becomes easier or more difficult to do because of this change?]
```

## Quality Attributes

### Performance
- Response time
- Throughput
- Resource utilization

### Scalability
- Load handling
- Resource scaling
- Cost efficiency

### Maintainability
- Code quality
- Documentation
- Technical debt

### Security
- Data protection
- Access control
- Compliance

### Reliability
- Fault tolerance
- Recovery
- Availability

## Implementation Guidelines

### Best Practices
1. **Documentation**
   - Architecture diagrams
   - API documentation
   - Decision records

2. **Testing**
   - Unit testing
   - Integration testing
   - Performance testing

3. **Code Quality**
   - Code reviews
   - Static analysis
   - Automated checks

### Anti-Patterns to Avoid
1. Big Ball of Mud
2. Golden Hammer
3. Accidental Complexity
4. Premature Optimization
