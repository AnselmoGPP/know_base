# Architecture patterns

## Table of Contents

+ [Introduction](#introduction)
+ [Best architecture](#best-architecture)
+ [Layered/structural patterns](#layered/structural-patterns)
  + [Monolith](#monolith)
  + [Layered](#layered)
  + [Clean](#clean)
  + [Hexagonal](#hexagonal)
  + [Modular](#modular)
  + [Onion](#onion)
  + [Component-based](#component-based)
  + [Package oriented](#package-oriented)
+ [Distributed systems patterns](#distributed-systems-patterns)
  + [Microservices](#microservices)
  + [Serverless](#serverless)
  + [Client–server](#client-server)
  + [Peer-to-peer (P2P)](#peer-to-peer-(p2p))
  + [Broker](#broker)
  + [Service-oriented (SOA)](#service-oriented-(soa))
  + [Distributed monolith](#distributed-monolith)
  + [Cloud-native](#cloud-native)
  + [Space-based](#space-based)
  + [Grid computing](#grid-computing)
  + [Clustered](#clustered)
+ [Event-driven and Messaging patterns](#event-driven-and-messaging-patterns)
  + [CQRS](#cqrs)
+ [Data-centric patterns](#data-centric-patterns)
+ [Presentation and UI architecture patterns](#presentation-and-ui-architecture-patterns)
+ [Integration patterns](#integration-patterns)
+ [Scalability, Reliability, and Performance patterns](#scalability,-reliability,-and-performance-patterns)
+ [Security-oriented architecture patterns](#security-oriented-architecture-patterns)
+ [Domain and Business-oriented patterns](#domain-and-business-oriented-patterns)
+ [Legacy and Specialized patterns](#legacy-and-specialized-patterns)
+ [Hybrid and Emerging patterns](#hybrid-and-emerging-patterns)
+ [](#)
+ [](#)
+ [](#)
+ [](#)


## Introduction

Software **architecture patterns** are predefined, reusable solutions to common design challenges at the system level, providing a high-level structure for organizing components, defining interactions, and establishing the overall layout of a software system. They address concerns related to scalability, performance, maintainability, and reliability, guiding decisions about the macro-level aspects of software development.

Architecture patterns operate at a higher level of abstraction than **design patterns**, who focus on solving specific, smaller-scale problems within individual components.

**Back-end patterns**:

- **Monolithic**
- **Layered**
- **Clean**
- **Hexagonal**:
- **Modular monolith**
- **Microservices**
- **CQRS (Command Query Responsibility Segregation)**
- **Serverless**

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

- **Layered/structural patterns**

  - **Monolithic** architecture: All code is together in a single deployment unit.
  - **Layered** architecture: Horizontal layers. Each one has a specific responsibility and interacts only with adjacent layers.
  - **Clean** architecture: Independence of business logic from frameworks, UIs, databases, and external systems.
  - **Hexagonal** architecture (Ports and Adapters): Isolates the core application logic from external systems (UIs, databases, messaging systems, and 3rd-party services).
  - **Modular** architecture: System decomposed into self-contained, cohesive modules, with their own responsibilities.
  - **Onion** architecture: System organized into concentric layers around the domain model, to protect business logic and enforce dependency inversion.
  - **Component-based** architecture: System built from independent, reusable components that encapsulate both behavior and data.
  - **Package-oriented** architecture: System organized around packages (or namespaces) as the main units of decomposition.

- **Distributed systems patterns**

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

- **Event-driven and Messaging patterns**

  - Event-Driven architecture (EDA)
  - Event-Based architecture
  - Publish–Subscribe
  - Message-Oriented architecture
  - Message Bus
  - Event Sourcing
  - **CQRS** (Command Query Responsibility Segregation)
  - Stream Processing architecture

- **Data-centric patterns**

  - Repository
  - Blackboard
  - Data-Centered architecture
  - Data Lake architecture
  - Data Warehouse architecture
  - Lambda architecture
  - Kappa architecture

- **Presentation and UI architecture patterns**

  - Model–View–Controller (MVC)
  - Model–View–ViewModel (MVVM)
  - Model–View–Presenter (MVP)
  - Presentation–Abstraction–Control (PAC)
  - Document–View
  - Front Controller

- **Integration patterns**

  - Enterprise Integration patterns (EIP)
  - Pipes and Filters
  - Adapter architecture
  - API Gateway
  - Backend for Frontend (BFF)
  - Sidecar pattern
  - Ambassador pattern

- **Scalability, Reliability, and Performance patterns**

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

- **Security-oriented architecture patterns**

  - Zero Trust architecture
  - Secure Gateway
  - Defense in Depth
  - Identity-Centric architecture

- **Domain and Business-oriented patterns**

  - Domain-Driven Design (DDD) architecture
  - Microkernel architecture (Plug-in Architecture)
  - Rule-Based architecture

- **Legacy and Specialized patterns**

  - Mainframe architecture
  - Client–Host architecture
  - Interpreter architecture
  - Virtual Machine architecture

- **Hybrid and Emerging patterns**

  - Hybrid architecture
  - Polyglot architecture
  - Multi-Tenant architecture
  - Self-Healing architecture
  - Reactive architecture
  
Each architecture pattern is described in following chapters with this structure:

- Description
- Characteristics
- Typical structure
- Advantages
- Disadvantages
- Use cases
- Comparisons


## Best architecture

Choosing the right pattern depends on different things such as:

- Project requirements
- Budget
- Team expertise
- Team size
- Frequency of changes
- Scalability needs
- Long-term operational goals

Decision-making frameworks can help to analyze trade-offs and avoid common anti-patterns.

### Back-end architecture

Some options:

- Layered monolith
- Modular monolith
- Clean / Hexagonal
- Microservices
- EDA / CQRS
- Serverless

Decision tree: 

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


## Layered/structural patterns

<<<


## Monolith

### Description

An application is built as a single, unified, and self-contained deployment unit. All code is together, so the whole deployment happens at once. Many successful systems begin as monoliths and evolve toward more distributed architectures only when scaling, organizational, or operational needs justify the added complexity.

Badly implemented, it can create a "giant ball of mud", which is a lot of code thightly coupled, difficult to update, and with intermingled responsabilities.

Well implemented, a monolith is a **modular monolith**. Responsabilities are well defined, and the different code parts and services are well separated (you can work in Payments without breaking Purchases). Modules are well defined and separated. To modularize the monolith you need to analyse the functionalities, users, and dependencies of your system.

Ideal for small to medium-sized applications but makes independent scaling of parts difficult.

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

Organizes applications into distinct layers for quick development and enterprise applications but can lead to unorganized code and complex redeployments.

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

Hexagonal Architecture, also known as **Ports and Adapters** architecture, is designed to isolate the core application logic from external systems such as user interfaces, databases, messaging systems, and third-party services.

It's similar to the Layered pattern, but also helps with the dependencies. Useful for complex layered architectures. It requires all business logic features to be fully defined and documented before implementation.

### Characteristics

The application is placed at the center, and all interactions with the outside world occur through well-defined ports. Concrete adapters implement those ports to connect the application to specific technologies. The “hexagon” is a conceptual visualization, not a constraint on the number of connections.

### Typical structure

- Application Core
  - Contains domain logic and application services
  - Independent of frameworks, databases, and delivery mechanisms
  - Defines interfaces (ports) for all external interactions
- Ports
  - Abstract interfaces declared by the application core
  - Define how external actors interact with the core
  - Two common types:
    - Inbound ports: Use cases invoked by external actors
    - Outbound ports: Interfaces for persistence, messaging, or external services
- Adapters
  - Implement ports and translate between external formats and internal models
  - Examples:
    - REST controllers
	- CLI handlers
    - Database repositories
    - Message consumers or producers

**Dependency Direction** enforces the dependency inversion principle.

- Dependencies always point toward the application core
- Adapters depend on ports, not the other way around
- The core is unaware of who calls it or how results are delivered

**Interaction Flow** 

External actor → inbound adapter → inbound port → application core → outbound port → outbound adapter → external system

### Advantages

- Strong isolation of business logic
- High testability (core logic can be tested with mocked ports)
- Easy replacement of UI, database, or external services
- Supports multiple delivery mechanisms simultaneously
- Clear separation between domain and infrastructure

### Disadvantages

- Increased abstraction and boilerplate
- Requires disciplined design to avoid anemic cores
- May be excessive for small or simple applications

### Use cases

- Applications with complex domain logic
- Systems requiring multiple interfaces (web, API, batch, messaging)
- Long-lived systems expected to evolve technologically
- Teams prioritizing testability and architectural clarity

### Comparisons

- __Clean__ architecture: Conceptually similar; Clean Architecture formalizes layers and dependency rules more explicitly.
- __Onion__ architecture: Shares the same inward dependency direction but emphasizes layering.
- __Layered__ architecture: Hexagonal replaces layer-based coupling with interaction-based boundaries.
- __Hexagonal__ architecture is particularly effective when the goal is to treat infrastructure as a replaceable detail rather than a foundational concern.


## Modular

### Description

A system is decomposed into self-contained, cohesive modules, each responsible for a distinct functional area and interacting with other modules through well-defined interfaces.

It's frequently a strategic intermediate step between a simple monolith and a distributed system, providing structural clarity while preserving operational simplicity.

### Characteristics

The application is structured as a collection of modules that:

- Encapsulate their internal implementation
- Expose only explicit public interfaces
- Can be developed, tested, and reasoned about independently
- Collaborate to form a complete system

Key characteristics:

- __High cohesion__: Each module focuses on a single business capability or technical responsibility.
- __Low coupling__: Inter-module dependencies are minimized and controlled.
- __Explicit boundaries__: Clear contracts govern communication between modules.
- __Replaceability__: Modules can be modified or replaced with limited impact on others.
- __Shared runtime__: Often implemented within a single process.

### Typical structure

Modules are typically deployed together, though they may also be independently deployable in some implementations.

Modules may be organized by:

- Business domains (e.g., Billing, Orders, Inventory)
- Features or use cases
- Technical concerns (e.g., Authentication, Logging)

Each module commonly contains:

- Public interfaces (APIs)
- Internal implementation details
- Optional internal data models or services

### Advantages

- Improved maintainability and readability
- Enhanced team autonomy and parallel development
- Easier testing and refactoring
- Reduced cognitive load compared to large monoliths
- Supports evolutionary design

### Disadvantages

- Requires disciplined boundary enforcement
- Poorly designed modules can degenerate into tight coupling
- Initial design effort is higher than ad hoc structures
- Tooling and governance may be needed to prevent dependency sprawl

### Use cases

- Medium to large codebases
- Systems with multiple business capabilities
- Teams seeking structure without distributed-system complexity
- Applications expected to grow incrementally

### Comparisons

- __Monolithic__ architecture: Modular architecture is often implemented as a modular monolith.
- __Microservices__ architecture: Modular architecture applies similar principles without network boundaries.
- __Layered__ architecture: Modules can exist within or across layers.
- __Clean__ / __Hexagonal__ architectures: Modules may internally adopt these patterns.


## Onion

### Description

It organizes a system into concentric layers around the domain model, with the explicit goal of protecting business logic and enforcing dependency inversion. It's conceptually similar to Clean and Hexagonal architecture, but emphasizes layering with inward-pointing dependencies. It's most effective when the domain model must remain isolated, stable, and independent of technical concerns.

### Characteristics

- __Domain-centric design__: The domain model is the core of the system.
- __Dependency inversion__: All dependencies point inward, toward the domain.
- __Separation of concerns__: Infrastructure and frameworks are kept at the outer layers.
- __Testability__: Core logic is independent of technical details.

### Typical structure

Architectural layers (Inside → Outside):

- Domain Layer
  - Entities, value objects, domain services
  - Contains pure business rules
  - No dependencies on other layers
- Application Layer
  - Use cases and application services
  - Coordinates domain objects
  - Defines interfaces (contracts) for infrastructure services
- Infrastructure Layer
  - Implementations of persistence, messaging, logging, external integrations
  - Depends on interfaces defined in inner layers
- Presentation / UI Layer
  - Controllers, APIs, UI frameworks
  - Translates external input into application use cases

**Dependency Rule**:

- Inner layers must not depend on outer layers.
- Outer layers may depend on inner layers.
- Communication across layers is achieved via interfaces defined inward.

### Advantages

- Strong protection of domain logic
- Clear separation between business rules and infrastructure
- High testability without frameworks or databases
- Easier technology replacement over time
- Enforces architectural discipline

### Disadvantages

- Additional abstraction and boilerplate
- Requires experience to design effective boundaries
- May feel heavy for simple CRUD applications
- Initial development can be slower

### Use cases

- Domain-driven systems
- Long-lived applications with evolving requirements
- Teams prioritizing maintainability and correctness
- Systems where business logic is the primary asset

### Comparisons

- __Clean architecture__: A generalized and more formalized evolution of Onion Architecture.
- __Hexagonal architecture__: Similar dependency direction, but focuses on ports and adapters rather than layers.
- __Layered architecture__: Onion Architecture inverts dependency direction compared to traditional layering.
- __Onion architecture__ is most effective when the domain model must remain isolated, stable, and independent of technical concerns.


## Component-based

### Description

Component-Based Architecture (CBA) builds a system from independent, reusable components that encapsulate both behavior and data, and interact through well-defined interfaces.

The primary goal is to improve reusability, maintainability, and composability.

### Characteristics

- __Components as primary units__: Each component represents a discrete functional unit.
- __Encapsulation__: Internal implementation details are hidden.
- __Explicit interfaces__: Components communicate only through published contracts.
- __Loose coupling__: Dependencies between components are minimized.
- __Replaceability__: Components can be substituted without affecting the rest of the system.

### Typical structure

A component usually includes:

- Public interfaces (provided and required)
- Internal implementation
- Optional internal state
- Configuration metadata

Components may be:

- Fine-grained (UI widgets, libraries)
- Coarse-grained (business modules, services)

**Interaction model**:

- Components interact via method calls, events, or message passing.
- Dependencies are resolved at compile time, deployment time, or runtime.
- Communication may be synchronous or asynchronous.

### Advantages

- High modularity and reusability
- Improved maintainability and evolution
- Parallel development by multiple teams
- Easier testing through interface contracts
- Supports plug-and-play system composition

### Disadvantages

- Interface design requires upfront effort
- Overcomponentization can increase complexity
- Performance overhead if interactions are excessive
- Versioning and compatibility management can be challenging

### Use cases

- Large systems with reusable functional units
- UI-heavy applications (e.g., frontend frameworks)
- Systems requiring extensibility or plugin mechanisms
- Teams developing shared libraries or platforms

### Comparisons

- __Modular__ architecture: Component-based architecture is a concrete realization of modularity.
- __Microservices__ architecture: Components are local; microservices are distributed components.
- __Layered__ architecture: Components can exist within or across layers.
- __Microkernel__ architecture: A specialized component-based pattern.
- __Component-Based__ Architecture is best suited when reuse, composability, and clear interface contracts are central design goals.


## Package oriented

### Description

This organizes a system primarily around packages (or namespaces) as the main units of decomposition, with explicit rules governing dependencies between those packages.

The goal is to manage complexity in large codebases by enforcing cohesion, dependency direction, and architectural boundaries at the package level.

It's especially effective when architecture must be visible, enforceable, and understandable directly from the code structure.

### Characteristics

Rather than focusing on layers, services, or components, this architecture treats packages as architectural elements. Each package:

- Groups closely related classes or files
- Represents a coherent responsibility (often a feature or domain area)
- Exposes a limited public API
- Restricts which other packages may depend on it

Key principles:

- High cohesion within packages
- Low coupling between packages
- Explicit dependency rules (often enforced by tooling)
- Stable dependency direction (less stable packages depend on more stable ones)
- Clear ownership and responsibility

### Typical structure

Common package structuring strategies:

- __Feature-based__ packaging: Packages represent business capabilities (e.g., orders, billing).
- __Domain-based__ packaging: Packages align with domain concepts or bounded contexts.
- __Technical packaging__ (less preferred): Packages represent technical concerns (e.g., controllers, services, repositories).

Dependency management rules: Typical constraints include:

- No cyclic dependencies between packages
- Dependencies must follow a defined hierarchy or graph
- Only public interfaces of a package may be accessed
- Internal implementation details are hidden

These rules are often enforced using static analysis tools.

### Advantages

- Improved maintainability in large codebases
- Clear architectural visibility at the code level
- Easier refactoring and impact analysis
- Supports team ownership and parallel development
- Technology-agnostic and lightweight

### Disadvantages

- Relies on discipline and tooling for enforcement
- Does not address deployment or runtime concerns
- Can be undermined by weak language-level encapsulation
- Less guidance on runtime interaction patterns

### Use cases

- Large monolithic or modular monolithic systems
- Systems suffering from package sprawl or cyclic dependencies
- Teams needing lightweight architectural governance
- Codebases where deployment boundaries are not required

### Comparisons

- __Layered__ architecture: Packages can represent layers.
- __Modular__ architecture: Package-oriented architecture is often the implementation mechanism.
- __Clean__ / __Onion__ architectures: Package boundaries are used to enforce dependency direction.
- __Microservices__: Each service internally often follows package-oriented design.


## Distributed systems patterns

<<<


## Microservices

### Description

An application is composed of small, autonomous services, each responsible for a specific business capability and independently deployable. This is most effective when organizational structure, operational maturity, and domain complexity justify the cost of distribution.

Microservices supports rapid deployment, safer development, and global teams, but are too technically expensive for small teams, and can introduce performance issues and challenges in task division.

It's recommended to begin with a monolith, keep it modular, and split it into microservices once the monolith becomes a problem. So, if some module requires scalability, you can replace it with a microservice.

### Characteristics

- __Service autonomy__: Each service is developed, deployed, and scaled independently.
- __Business capability alignment__: Services are organized around business domains rather than technical layers.
- __Decentralized data management__: Each service owns its data and persistence model.
- __Lightweight communication__: Services interact via APIs, messaging, or events, typically over the network.
- __Technology heterogeneity__: Different services may use different languages, frameworks, or databases.

### Typical structure

- A microservices system usually includes:
- Multiple independently deployable services
- API gateways or edge services
- Service discovery mechanisms
- Inter-service communication (HTTP, gRPC, messaging)
- Centralized observability (logging, metrics, tracing)

Key supporting patterns:

- API Gateway
- Service Discovery <<<
- Circuit Breaker
- Saga <<<
- Event-Driven Architecture
- CQRS
- Strangler Fig

### Advantages

- __Scalability__: Services can scale independently based on demand.
- __Agility__: Faster, safer deployments with smaller change scopes.
- __Resilience__: Failures are isolated to individual services.
- __Team autonomy__: Small, cross-functional teams can own services end-to-end.
- __Technology flexibility__: Enables gradual adoption of new technologies.

### Disadvantages

- __Operational complexity__: Requires mature DevOps, CI/CD, and monitoring.
- __Distributed system challenges__: Network latency, partial failures, and eventual consistency.
- __Data consistency issues__: Transactions across services are complex.
- __Increased overhead__: More infrastructure, tooling, and coordination.
- __Higher cognitive load__: System behavior is harder to reason about.

### Use cases

- Large or rapidly growing systems
- Organizations with multiple autonomous teams
- Applications with clear domain boundaries
- Systems requiring independent scalability and deployment
- Teams experienced with distributed systems

### Comparisons

- __Monolithic__ architecture: Microservices decompose a monolith into distributed services.
- __Modular monolith__: Often a precursor to microservices.
- __SOA__: Microservices are a more fine-grained, independently deployable evolution of SOA.
- __Clean__ / __Hexagonal__ architectures: Commonly applied within individual services.


## Serverless

### Description

Servers management is delegated to a cloud (AWS, etc.). It's more expensive than keeping all in a dedicated server. Useful for high availability (process running non-stop) and peak traffic (your product is used mostly at certain times). For non-peak traffic (stable usage), dedicated server is preferred.

Runs code in ephemeral containers managed by cloud providers. Developers focus on logic without managing servers.

Architectures can be implemented in very different ways. Example: a monolith can be deployed in a dedicated server using Docker, Kubernetes, Lambdas (AWS), etc.

Serverless architecture is a cloud-native architectural pattern in which application logic is executed in managed, event-driven compute environments, and infrastructure provisioning, scaling, and server management are handled entirely by the cloud provider.

Despite the name, servers still exist; they are abstracted away from the development and operations teams.

Serverless architecture is most effective when operational simplicity and elastic scalability outweigh the need for fine-grained infrastructure control.

### Characteristics

- __No server management__: Developers do not provision, configure, or maintain servers.
- __Event-driven execution__: Functions run in response to events (HTTP requests, messages, file uploads, timers).
- __Automatic scaling__: The platform scales execution units up or down automatically.
- __Pay-per-use pricing__: Costs are based on actual execution time and resources consumed.
- __Stateless compute__: Functions are ephemeral and do not retain state between executions.

### Typical structure

Key components:

- __Functions as a Service (FaaS)__: Small, single-purpose functions that encapsulate business logic.
- __Managed cloud services__: Databases, queues, object storage, authentication, and APIs provided as services.
- __Event sources__: Triggers such as API gateways, message brokers, streams, or schedulers.

Typical architecture flow:

- Event occurs (e.g., HTTP request)
- Cloud provider invokes a function
- Function executes logic and interacts with managed services
- Function terminates, releasing compute resources

### Advantages

- Minimal operational overhead
- Built-in scalability and high availability
- Faster development and deployment
- Cost efficiency for variable or low-traffic workloads
- Strong alignment with event-driven systems

### Disadvantages

- Cold start latency
- Vendor lock-in risks
- Limited execution time and resource constraints
- Harder debugging and local testing
- Complex orchestration for long-running workflows

### Use cases

- Event-driven or asynchronous workloads
- APIs with unpredictable traffic patterns
- Data processing and integration pipelines
- Rapid prototyping and time-to-market–driven projects

### Comparisons

- __Microservices__ architecture: Serverless functions often act as microservices.
- __Event-driven__ architecture: Serverless systems are commonly event-based.
- __Monolithic__ architecture: Serverless decomposes monolithic logic into functions.
- __CQRS__: Frequently used for read or write sides independently.


## Client–Server

### Description

This splits responsibilities between clients, which request services, and servers, which provide those services over a network. The pattern establishes a clear separation between request initiators and service providers.

### Characteristics

- Separation of roles: Clients request services; servers provide them
- Centralized services and data: Shared resources managed by the server
- Request–response communication: Typically synchronous over a network
- Multiple clients, shared server: One server serves many clients
- Network dependency: Interaction occurs via standardized protocols

### Typical structure

- Clients
  - Initiate requests
  - Handle user interaction or request composition
  - Do not share state with other clients
- Servers
  - Provide services, resources, or data
  - Process client requests
  - Manage shared resources and business logic
- Network-based communication
  - Typically request–response
  - Uses standardized protocols (e.g., HTTP, TCP)

Typical interaction flow:

1. Client sends a request to the server
2. Server processes the request
3. Server returns a response
4. Client consumes and presents the result

Common variations:

- Two-tier client–server: Client communicates directly with the database server
- Three-tier client–server: Client → application server → database server
- Thin client: Minimal logic on the client
- Thick (fat) client: Significant logic on the client

### Advantages

- Clear separation of responsibilities
- Centralized data and security management
- Easier maintenance of shared resources
- Scales better than peer-to-peer for many use cases
- Widely understood and supported

### Disadvantages

- Server can become a bottleneck
- Single point of failure without redundancy
- Network latency impacts performance
- Limited offline capability
- Scaling requires additional infrastructure

### Use cases

- Networked applications
- Centralized data access requirements
- Systems requiring controlled access and security
- Web, enterprise, and database-driven applications

### Comparisons

- Layered architecture: Client–server systems often implement layered designs on the server side.
- Three-tier architecture: A structured form of client–server architecture.
- Microservices: Extend client–server principles across many servers.
- Peer-to-peer: Contrasts with client–server by decentralizing roles.
- Client–server architecture remains a foundational pattern underlying most modern web, mobile, and enterprise systems.


## Peer-to-peer (P2P)

### Description

In Peer-to-Peer (P2P) architecture all nodes (peers) have equal roles, act as both clients and servers, and share resources directly with one another without centralized control.

### Characteristics

- Decentralization: No central server controlling the system
- Symmetric roles: Each peer can request and provide services
- Direct peer communication: Peers interact directly over the network
- Resource sharing: Computing power, storage, or data is distributed
- Dynamic topology: Peers can join and leave at any time

### Typical structure

It consists of the following elements:

- Peers (nodes): Independent processes or machines with equal responsibilities
- Overlay network: Logical network that defines how peers discover and communicate with each other
- Discovery mechanism: Methods for peers to find other peers (e.g., flooding, distributed hash tables, bootstrap nodes)
- Direct communication channels: Peer-to-peer messaging or data transfer links
- Distributed resource management: Data, computation, or services partitioned or replicated across peers

This structure eliminates centralized servers while enabling coordinated, decentralized interaction.

### Advantages

- High scalability as peers increase
- Improved fault tolerance due to decentralization
- Efficient use of distributed resources
- Reduced infrastructure costs

### Disadvantages

- Complex coordination and discovery
- Harder security and trust management
- Inconsistent performance and availability
- Difficult debugging and governance

### Use cases

- File-sharing systems
- Distributed storage and blockchain systems
- Collaborative and decentralized applications
- Systems requiring resilience without central control

### Comparisons

- Client–server: P2P removes centralized servers
- Distributed systems: P2P is a fully decentralized form
- Hybrid architectures: Often combined with central coordination services
- Peer-to-peer architecture is best suited when decentralization, scalability, and resilience outweigh the need for centralized control.


## Broker

### Description

A central intermediary (the broker) manages communication, coordination, and interaction between decoupled clients and service providers. Clients do not communicate with servers directly; instead, all interaction is mediated by the broker.

### Characteristics

The broker acts as a message router and coordinator, enabling location transparency and loose coupling between distributed components.

### Typical structure

- Clients
  - Initiate requests for services
  - Are unaware of service provider locations or implementations
- Broker
  - Receives client requests
  - Locates appropriate service providers
  - Routes requests and responses
  - Manages registration and discovery
- Service Providers (Servers)
  - Register their services with the broker
  - Execute requested operations
  - Return results via the broker

Interaction flow:

1. Service provider registers with the broker
2. Client sends a request to the broker
3. Broker identifies a suitable provider
4. Request is forwarded to the provider
5. Response is routed back to the client

### Advantages

- Loose coupling between clients and providers
- Location transparency
- Improved scalability and extensibility
- Simplified client logic
- Centralized coordination and routing

### Disadvantages

- Broker can become a bottleneck or single point of failure
- Added latency due to indirection
- Increased broker complexity
- Requires robust fault tolerance mechanisms

### Use cases

- Distributed systems with dynamic service discovery
- Systems requiring transparent service location
- Middleware-based enterprise systems
- Message-oriented or service-based platforms

### Comparisons

- Client–server: Broker introduces an intermediary layer
- Message-oriented architecture: Broker often implements messaging semantics
- Microservices: Brokers may appear as service meshes or messaging brokers
- SOA: Broker is a foundational pattern in service-oriented systems
- Broker architecture is most effective when decoupling, flexibility, and dynamic service coordination are primary concerns.


## Service-oriented (SOA)

### Description

In SOA, a system is composed of loosely coupled, reusable services that expose well-defined business capabilities through standardized interfaces. The focus is on enterprise-level integration, interoperability, and reuse.

SOA is best suited for enterprise environments where interoperability, reuse, and governance outweigh the need for rapid, decentralized evolution.

### Characteristics

- Services as business capabilities: Each service represents a meaningful business function.
- Loose coupling: Services interact through contracts, not implementations.
- Standardized interfaces: Communication uses agreed-upon protocols and data formats.
- Service autonomy: Services control their own logic and resources.
- Reusability: Services are designed to be reused across multiple applications.

### Typical structure

- Service Providers: Implement and expose services.
- Service Consumers: Discover and invoke services.
- Service contracts: Define service interfaces, policies, and data schemas.
- Enterprise Service Bus (ESB) (common in traditional SOA): Handles routing, transformation, orchestration, and mediation.

Communication:

- Typically uses messaging or request–response
- Common protocols include SOAP, HTTP, messaging systems
- Often supports synchronous and asynchronous interaction

### Advantages

- Strong integration capabilities across heterogeneous systems
- Encourages reuse at an enterprise scale
- Technology and platform independence
- Aligns IT systems with business processes

### Disadvantages

- High complexity and governance overhead
- Performance impact due to mediation layers
- ESB can become a bottleneck or single point of failure
- Slower evolution compared to finer-grained architectures

### Use cases

- Large enterprises with multiple legacy systems
- Cross-organizational integration requirements
- Systems requiring strong governance and standardization
- Long-lived enterprise platforms

### Comparisons

- Microservices architecture: A finer-grained, decentralized evolution of SOA
- Broker architecture: ESB acts as a specialized broker
- Client–server: SOA generalizes client–server interactions
- Event-driven architecture: Often combined with SOA


## Distributed monolith

### Description
### Characteristics
### Typical structure
### Advantages
### Disadvantages
### Use cases
### Comparisons







## Cloud-native
## Space-based
## Grid computing
## Clustered



### Description
### Characteristics
### Typical structure
### Advantages
### Disadvantages
### Use cases
### Comparisons


## Event-driven and Messaging patterns

<<<


## CQRS

### Description

CQRS (Command Query Responsibility Segregation) is good for event-driven architectures. It segregates commands from actions. CQRS is often used with WebSockets. It separates read and write operations to improve scalability and performance, though it increases database complexity and cost.

Example: Given a server (or microservice), segregate requests to it (commands) from its responses (actions). This allows you to enqueue the requests while listening for responses asynchronously. Each request has a unique id. An operation is considered completed when the request receives the response.

It increases scalability, but increases complexity. Useful for managing big amounts of information.

CQRS (Command Query Responsibility Segregation) is a pattern in which a system separates the models and responsibilities for handling commands (writes) and queries (reads). CQRS is most valuable when read and write concerns differ significantly in complexity, scale, or performance requirements.

### Characteristics

Instead of using a single model to both read and write data, CQRS defines __commands__ to change system state and __queries__ to retrieve system state. Each side is designed, optimized, and evolved independently.

### Typical structure

Key components:

- Command Model
  - Handles create, update, and delete operations
  - Enforces business rules and invariants
  - Typically uses rich domain models
  - Does not return data beyond execution status
- Query Model
  - Handles read-only operations
  - Optimized for data retrieval and performance
  - Often uses denormalized or specialized data structures
  - Returns DTOs or view models
- Handlers
  - Command handlers execute business logic
  - Query handlers retrieve data

**Data Storage**: Command and query sides may share the same database, use separate databases, or use different storage technologies entirely. When combined with Event Sourcing, the write model persists events, and the read model is built from event projections.

### Advantages

- Independent scaling of read and write workloads
- Improved performance for complex queries
- Clear separation of responsibilities
- Simplified models for each concern
- Better alignment with complex domain logic

### Disadvantages

- Increased architectural complexity
- Eventual consistency between read and write models
- Higher implementation and operational cost
- Overkill for simple CRUD systems

### Use cases

- Systems with complex business logic
- Applications with high read-to-write ratios
- Domains requiring strict command validation
- Systems benefiting from event-driven processing

### Comparisons

- __Event Sourcing__: Frequently paired with CQRS
- __Microservices__: CQRS is often applied within services
- __Layered__ / __Clean__ architecture: CQRS fits naturally within these structures
- __CRUD__ architectures: CQRS replaces the single shared model


## Data-centric patterns

## Presentation and UI architecture patterns

## Integration patterns

## Scalability, Reliability, and Performance patterns

## Security-oriented architecture patterns

## Domain and Business-oriented patterns

## Legacy and Specialized patterns

## Hybrid and Emerging patterns






## 

### Description
### Characteristics
### Typical structure
### Advantages
### Disadvantages
### Use cases
### Comparisons





