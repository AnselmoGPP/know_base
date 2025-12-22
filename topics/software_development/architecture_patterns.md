# Architecture patterns

## Table of Contents

+ [Introduction](#introduction)
+ [Choosing architecture](#choosing-architecture)
+ [Monolith](#monolith)
+ [Layered](#layered)
+ [Clean](#clean)
+ [Hexagonal](#hexagonal)
+ [Modular monolith](#modular-monolith)
+ [Microservices](#microservices)
+ [CQRS](#cqrs)
+ [Serverless](#serverless)
+ [](#)


## Introduction

Software **architecture patterns** are predefined, reusable solutions to common design challenges at the system level, providing a high-level structure for organizing components, defining interactions, and establishing the overall layout of a software system. They address concerns related to scalability, performance, maintainability, and reliability, guiding decisions about the macro-level aspects of software development.

Architecture patterns operate at a higher level of abstraction than **design patterns**, who focus on solving specific, smaller-scale problems within individual components.

**Back-end patterns**:

- **Monolithic**: Ideal for small to medium-sized applications but makes independent scaling of parts difficult.
- **Layered**: Organizes applications into distinct layers for quick development and enterprise applications but can lead to unorganized code and complex redeployments.
- **Clean**: 
- **Hexagonal**:
- **Modular monolith**: 
- **Microservices**: Supports rapid development and global teams but can introduce performance issues and challenges in task division.
- **CQRS (Command Query Responsibility Segregation)**: It separates read and write operations to improve scalability and performance, though it increases database complexity and cost.
- **Serverless**: Runs code in ephemeral containers managed by cloud providers. Developers focus on logic without managing servers.

**More**:

- **Event-driven**: Suitable for user interfaces and agile applications but introduces complexity in error handling and testing.
- **Event sourcing**: Instead of storing the current state, this pattern stores a sequence of state-changing events. The current state is reconstructed by replaying these events.
- **Model-View-Controller (MVC)**: It helps organize complex applications by separating data, presentation, and user input handling, though it may add unnecessary complexity for simpler applications.
- **Client-Server model**: It centralizes resources and management but creates a single point of failure and high server maintenance costs.
- **Microkernel** (plugin): It separates core functionality from extensions, promoting modularity.
- **Pipes and Filters**: It breaks down complex processing into reusable, sequential elements, though it risks data loss and performance limits.
- **Peer-to-Peer**: It enables decentralized systems like file sharing and cryptocurrency but faces security and performance challenges due to node dependency.

**Cloud environment patterns**:

- **Circuit Breaker**: It enhances fault tolerance by rerouting traffic when a service fails, though it requires sophisticated infrastructure like service meshes.
- **Saga**: It manages long-running transactions across microservices by using a sequence of compensating actions to maintain consistency, but it demands significant programming effort.
- **Backends for Frontends**: It creates dedicated backend services for different frontends, improving reliability and security.
- **Queue-Based Load Leveling**: It uses a queue as a buffer to smooth out variable workloads, enhancing reliability and cost efficiency.

**Other patterns**:

- **Strangler Fig**: It allows for incremental migration of legacy systems by wrapping the old system with a new one, reducing risk during transformation, though it requires careful routing and rollback planning.
- **Sharding**: It divides data across multiple database instances to improve query performance and storage distribution, but it demands skilled database administration.
- **Event Sourcing**: It records all state changes as events, enabling real-time data processing and audit trails, though it requires a robust and low-latency network.

The following list (76 elements) is exhaustive, though no list can be truly complete because patterns evolve and are sometimes renamed or combined.

- Layered/structural patterns

  - **Monolithic** architecture: All code is together in a single deployment unit.
  - **Layered** architecture: Horizontal layers. Each one has a specific responsibility and interacts only with adjacent layers.
  - **Clean** architecture
  - **Hexagonal** architecture (Ports and Adapters)
  - **Modular** architecture 
  X N-Tier architecture
  X Three-Tier architecture
  X Two-Tier architecture
  - Onion architecture
  - Component-Based architecture
  - Package-Oriented architecture

- Distributed Systems patterns

  - Client–Server
  - Peer-to-Peer
  - Broker
  - Service-Oriented architecture (SOA)
  - **Microservices** architecture
  - Distributed Monolith
  - Cloud-Native architecture
  - **Serverless** architecture
  - Space-Based architecture
  - Grid Computing architecture
  - Clustered architecture

- Event-Driven and Messaging patterns

  - Event-Driven architecture (EDA)
  - Event-Based architecture
  - Publish–Subscribe
  - Message-Oriented architecture
  - Message Bus
  - Event Sourcing
  - **CQRS** (Command Query Responsibility Segregation)
  - Stream Processing architecture

- Data-Centric patterns

  - Repository
  - Blackboard
  - Data-Centered architecture
  - Data Lake architecture
  - Data Warehouse architecture
  - Lambda architecture
  - Kappa architecture

- Presentation and UI Architecture patterns

  - Model–View–Controller (MVC)
  - Model–View–ViewModel (MVVM)
  - Model–View–Presenter (MVP)
  - Presentation–Abstraction–Control (PAC)
  - Document–View
  - Front Controller

- Integration patterns

  - Enterprise Integration patterns (EIP)
  - Pipes and Filters
  - Adapter architecture
  - API Gateway
  - Backend for Frontend (BFF)
  - Sidecar pattern
  - Ambassador pattern

- Scalability, Reliability, and Performance patterns

  - Master–Slave
  - Leader–Follower
  - Replicated Services
  - Sharded architecture
  - Load-Balanced architecture
  - Circuit Breaker
  - Bulkhead
  - Strangler Fig
  - Retry pattern
  - Failover pattern

- Security-Oriented Architecture patterns

  - Zero Trust architecture
  - Secure Gateway
  - Defense in Depth
  - Identity-Centric architecture

- Domain and Business-Oriented patterns

  - Domain-Driven Design (DDD) architecture
  - Microkernel architecture (Plug-in Architecture)
  - Rule-Based architecture

- Legacy and Specialized patterns

  - Mainframe architecture
  - Client–Host architecture
  - Interpreter architecture
  - Virtual Machine architecture

- Hybrid and Emerging patterns

  - Hybrid architecture
  - Polyglot architecture
  - Multi-Tenant architecture
  - Self-Healing architecture
  - Reactive architecture


## Choosing architecture

Choosing the right pattern depends on different things such as:

- Project requirements
- Budget
- Team expertise
- Team size
- Frequency of changes
- Scalability needs
- Long-term operational goals

Decision-making frameworks can help to analyze trade-offs and avoid common anti-patterns.

Choosing __back-end architecture__: 

- Highly coupled system? (strong and frequent transactions between domains) (too much communication between different parts of the system)
  - [Yes] __Layered monolith__
  - [No] Long lasting product and focus on mantainability/tests? (maintainability or test phase)
    - [Yes] Apply __clean__ / __hexagonal__ within the monolith
    - [No] 5-12 engineers working in parallel? (big team)
      - [No] __Layered monolith__
	  - [Yes] __Modular monolith__
	    - One domain has different rithm or scale? (one module of the system gets more requests)
	      - [No] __Modular monolith__
		  - [Yes] Extract only that domain (extract that module into an independent __microservice__)
		    - Do you have solid CI/CD + observability + tracing?
		      - [No] __Modular monolith__
			  - [Yes] >12-15 engineers or independent releases per domain?
			    - [No] __Modular monolith__
			    - [Yes] __Microservices per domain__
			      - Traffic is global or very irregular?
				    - [Yes] __Partial serverless__
				    - [No] Do you accept eventual consistency?
				      - [Yes] Add __EDA__ / __CQRS__
				      - [No] Keep __simple synchronization__

The following chapters explain each architecture pattern. Each chapter has the following sections:

- Description
- Characteristics
- Typical structure
- Advantages
- Disadvantages
- Use cases
- Comparisons


## Monolith

### Description

An application is built as a single, unified, and self-contained deployment unit. All code is together, so the whole deployment happens at once. Badly implemented it can create a "giant ball of mud" (a lot of code thightly coupled, difficult to update, and with intermingled responsabilities). Many successful systems begin as monoliths and evolve toward more distributed architectures only when scaling, organizational, or operational needs justify the added complexity.

### Characteristics

- __Single codebase__: All functionality—user interface, business logic, and data access—is implemented within one codebase.
- __Single deployment artifact__: The application is built, tested, and deployed as one executable or package (for example, a JAR, WAR, or binary).
- __Shared runtime and resources__: All components run in the same process and typically share memory, CPU, and other system resources.
- __Tight coupling__: Modules are often interdependent, with direct method calls rather than network-based communication.
- __Centralized data management__: Usually relies on a single database or tightly coupled data layer.

### Typical structure

- Presentation layer (UI, controllers)
- Business logic layer (services, domain logic)
- Data access layer (repositories, ORM, database access)
- Although these layers may be logically separated, they are physically deployed together.

### Advantages

- __Simplicity__: Easier to design, build, test, and deploy, especially for small teams or early-stage products.
- __Performance__: In-process communication is faster than network calls.
- __Operational ease__: Fewer moving parts; simpler monitoring, logging, and deployment pipelines.
- __Straightforward debugging__: End-to-end execution paths are easier to trace.

### Disadvantages

- __Limited scalability__: The entire application must be scaled as a whole, even if only one part needs additional capacity.
- __Reduced agility__: Small changes can require rebuilding and redeploying the entire system.
- __Growing complexity__: As the codebase expands, maintainability and understandability decline.
- __Technology lock-in__: Difficult to adopt different technologies for different components.
- __Lower fault isolation__: A failure in one module can impact the entire application.

### Use cases

- Small to medium-sized applications
- Early-stage startups or proof-of-concept systems
- Teams with limited DevOps or distributed systems expertise
- Applications with relatively stable and well-understood requirements

### Comparisons

- Versus __Microservices__: Monoliths favor simplicity and cohesion, while microservices favor scalability and independent deployment.
- Versus __Modular Monoliths__: Modular monoliths retain single deployment but enforce strong internal boundaries to mitigate coupling.


## Layered

### Description

The application is organized into horizontal layers, where each layer has a specific responsibility and interacts only with adjacent layers. This remains one of the most widely adopted and foundational patterns due to its conceptual simplicity and organizational clarity.

Example of layers: The Communication layer receives a request, the Domain layer gets the requested data, 

- Communication: External communication. Transportation with the API.
- Domain: Functions for computations and data processing.
- Data: Functions that call to databases or external APIs. Data acquisition from 3rd parties.

### Characteristics

The system is structured as a stack of layers. Each layer:

- Encapsulates a well-defined set of responsibilities
- Depends only on the layer directly beneath it
- Provides services to the layer above it

This creates a clear separation of concerns and enforces logical boundaries within the application.

### Typical structure

**Common structure** (the exact number and naming of layers can vary):

- __Presentation__ layer
  - User interface
  - Input handling
  - Request/response coordination
 - __Application__ (or Service) layer
  - Application workflows
  - Use-case orchestration
  - Transaction management
- __Domain__ (or Business) layer
  - Core business rules
  - Domain models and logic
- __Data Access__ (or Infrastructure) layer
  - Database access
  - External system integration
  - Persistence logic

**Layer interaction rules**:

- __Top-down dependency__: Higher layers depend on lower layers, never the reverse.
- __No layer skipping__ (in strict layering): Each request passes through every layer in sequence.
- __Controlled bypassing__ (in relaxed layering): Certain layers may be skipped for performance or simplicity.

**Common variations** balance structure versus flexibility, to adapt to different system sizes, performance requirements, and organizational constraints:

- __Two-tier__ architecture: Two layers; typically, Presentation and Data layers. Business logic often resides in the presentation layer or is tightly coupled with it. Common in simple desktop applications or early client–server systems.
- __Three-tier__ architecture: Three layers; typically, Presentation, Application (business logic) and Data layers. Improves separation of concerns and scalability compared to two-tier systems. Widely used in web and enterprise applications.
- __N-tier__ architecture: Extends three-tier architecture to multiple logical or physical layers. Layers may be deployed across different servers or services. Enables scalability, load distribution, and finer-grained responsibility separation. Common in large enterprise and distributed systems.
- __Strict layered__ architecture: Each layer can only communicate with the layer directly below it. All requests must pass through every layer in sequence. Enforces strong discipline and clear boundaries, improving maintainability. Can introduce performance overhead and rigidity.
- __Relaxed layered__ architecture: Higher layers may bypass intermediate layers and access lower layers directly. Used to reduce latency or simplify flows where full layering is unnecessary. Offers flexibility but requires careful governance to avoid architectural erosion.

### Advantages

- __Separation of concerns__: Each layer has a clear and focused responsibility.
- __Maintainability__: Changes in one layer have limited impact on others.
- __Testability__: Layers can be tested independently using mocks or stubs.
- __Team scalability__: Teams can work in parallel on different layers.
- __Technology isolation__: Infrastructure changes are often confined to lower layers.

### Disadvantages

- __Performance overhead__: Additional layers can introduce latency.
- __Rigidity__: Strict layering can make simple changes more complex.
- __Overengineering risk__: Too many layers for small systems add unnecessary complexity.
- __Leakage of concerns__: Poorly enforced boundaries can result in business logic creeping into upper layers.

### Use cases

- Enterprise and line-of-business applications
- Systems with well-understood domains
- Teams that value clarity, governance, and maintainability
- Applications with relatively stable requirements

### Comparisons

- __Monolithic__ architecture: Layered architecture is often implemented within a monolith.
- __Clean__ / __Onion__ / __Hexagonal__ architectures: These refine layering by inverting dependencies and strengthening domain isolation.


## Clean

### Description

It emphasizes independence of business logic from frameworks, user interfaces, databases, and external systems, with the primary goal of maximizing maintainability, testability, and long-term adaptability. It's particularly effective when the business domain is the most valuable and volatile part of the system, and technical details are expected to change over time.

It's similar to the Layered pattern, but also helps with the dependencies. Useful for complex layered architectures. However, it requires all business logic features to be fully defined and documented before implementation.

### Characteristics

- __Separation of concerns__: Business rules are isolated from technical details.
- __Dependency inversion__: Source code dependencies always point inward, toward higher-level policies.
- __Framework independence__: Frameworks are treated as implementation details, not foundations.
- __Testability__: Business logic can be tested without external dependencies.
- __UI and database independence__: The system does not depend on specific UI or database technologies.

### Typical structure

It's commonly visualized as concentric circles, where each inner circle represents more abstract and stable policies.

From inside to outside:

- __Entities__
  - Enterprise-wide business rules
  - Core domain models and logic
  - Highly stable and reusable
- __Use Cases__ (application business rules)
  - Application-specific business workflows
  - Orchestrate entities to fulfill user goals
  - Define input and output data structures
- __Interface Adapters__
  - Controllers, presenters, gateways
  - Convert data between use-case formats and external formats
  - Isolate use cases from UI, database, and frameworks
- __Frameworks and Drivers__
  - Web frameworks, databases, UI frameworks, messaging systems
  - Contain concrete implementations and integrations
  - Easily replaceable without impacting core logic

**Dependency rule**: Source code dependencies must point only inward.

- Outer layers depend on inner layers. 
- Inner layers are unaware of outer layers.
- Communication is achieved through interfaces defined in inner layers and implemented in outer layers.

### Advantages

- Strong business rule protection
- High testability without mocks of infrastructure
- Improved maintainability and evolvability
- Reduced coupling to frameworks and vendors
- Clear architectural boundaries

### Disadvantages

- Increased initial complexity
- More boilerplate and abstraction
- Steeper learning curve for teams unfamiliar with the pattern
- Can be excessive for small or short-lived applications

### Use cases

- Systems with complex or evolving business logic
- Long-lived enterprise applications
- Projects requiring high test coverage
- Teams that expect changes in frameworks, UI, or persistence technologies

### Comparisons

- __Onion__ and __Hexagonal__ architectures are closely related and share similar goals.

- __Layered__ architecture focuses on separation, while Clean architecture emphasizes dependency direction and domain protection.


## Hexagonal

### Description
### Characteristics
### Typical structure
### Advantages
### Disadvantages
### Use cases
### Comparisons

It's similar to the Layered pattern, but also helps with the dependencies. Useful for complex layered architectures.

It requires all business logic features to be fully defined and documented before implementation.


## Modular monolith

### Description
### Characteristics
### Typical structure
### Advantages
### Disadvantages
### Use cases
### Comparisons

Basically, it's a well-done monolith. Responsabilities are well defined, and the different code parts and services are well separated (you can work in Payments without breaking Purchases). Modules are well defined and separated. To modularize the monolith you need to analyse the functionalities, users, and dependencies of your system.


## Microservices

### Description
### Characteristics
### Typical structure
### Advantages
### Disadvantages
### Use cases
### Comparisons

Advantages: Better deployment speed, and safer development.

It's recommended to begin with a monolith, keep it modular, and split it into microservices once the monolith becomes a problem. So, if some module requires scalability, you can replace it with a microservice.

Microservices are too technically expensive for small teams.


## CQRS

### Description
### Characteristics
### Typical structure
### Advantages
### Disadvantages
### Use cases
### Comparisons

CQRS (Command Query Responsibility Segregation) is good for event-driven architectures. It segregates commands from actions. CQRS is often used with WebSockets.

Example: Given a server (or microservice), segregate requests to it (commands) from its responses (actions). This allows you to enqueue the requests while listening for responses asynchronously. Each request has a unique id. An operation is considered completed when the request receives the response.

It increases scalability, but increases complexity. Useful for managing big amounts of information.


## Serverless

### Description
### Characteristics
### Typical structure
### Advantages
### Disadvantages
### Use cases
### Comparisons

Servers management is delegated to a cloud (AWS, etc.). It's more expensive than keeping all in a dedicated server. Useful for high availability (process running non-stop) and peak traffic (your product is used mostly at certain times). For non-peak traffic (stable usage), dedicated server is preferred.

Architectures can be implemented in very different ways. Example: a monolith can be deployed in a dedicated server using Docker, Kubernetes, Lambdas (AWS), etc.