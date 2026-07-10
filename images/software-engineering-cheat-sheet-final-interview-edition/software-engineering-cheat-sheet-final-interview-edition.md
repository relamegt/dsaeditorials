# Software Engineering Cheat Sheet — Final Interview Edition

A complete, publish-ready reference covering Software Engineering fundamentals with full forms and clear working explanations, matching the structure of your OS, CN, DBMS, and ML sheets.

## 1. Basic Terminology

| Term | Full Form / Meaning |
| --- | --- |
| SE | Software Engineering — systematic application of engineering principles to design, develop, and maintain software |
| SDLC | Software Development Life Cycle |
| SRS | Software Requirements Specification |
| UML | Unified Modeling Language |
| CASE | Computer-Aided Software Engineering |
| QA | Quality Assurance |
| CI/CD | Continuous Integration / Continuous Deployment |
| MVP | Minimum Viable Product |
| API | Application Programming Interface |

## 2. SDLC — Software Development Life Cycle

**How it works**: SDLC is a structured sequence of phases a software project moves through, each producing specific deliverables that feed into the next phase.

1. **Requirement Analysis** — gathering and documenting what the system must do, usually captured in an SRS.
2. **Design** — translating requirements into architecture, data models, and interface designs.
3. **Implementation (Coding)** — writing actual source code based on the design.
4. **Testing** — verifying the software works correctly and meets requirements.
5. **Deployment** — releasing the software to production/users.
6. **Maintenance** — fixing bugs, adding features, and adapting to changes after release.

## 3. SDLC Models — How Each Works

**Waterfall Model**
How it works: Each phase must be fully completed before the next begins, in a strict linear sequence (Requirements → Design → Implementation → Testing → Deployment → Maintenance) — no going back once a phase is signed off.
Trait: Simple to manage and document, but inflexible to changing requirements; risky for long projects since problems surface only near the end.

**Iterative Model**
How it works: The system is built in repeated cycles; each iteration produces a working (partial) version, which is refined based on feedback in the next iteration.
Trait: Allows early detection of issues, but requires more planning overhead to manage iterations.

**Spiral Model**
How it works: Combines iterative development with explicit risk analysis — each "loop" of the spiral goes through planning, risk analysis, engineering, and evaluation before deciding to proceed to the next loop.
Trait: Ideal for large, high-risk projects, but complex to manage and can be costly.

**Agile Model**
How it works: Software is developed in small increments called **sprints** (typically 1–4 weeks); at the end of each sprint, a working piece of functionality is delivered, and feedback is incorporated into the next sprint's planning.
Trait: Highly flexible and responsive to change, but requires close, continuous customer collaboration.

**V-Model (Verification and Validation)**
How it works: Extends Waterfall by pairing each development phase with a corresponding testing phase planned in parallel (e.g., Requirements ↔ Acceptance Testing, Design ↔ System Testing).
Trait: Strong emphasis on testing from the start, but still rigid like Waterfall.

## 4. Agile Framework — Scrum

**How it works**: Scrum organizes work into fixed-length **sprints**. A **Product Backlog** lists all desired features; before each sprint, the team picks items into a **Sprint Backlog**. Daily **stand-up meetings** track progress, and a **Sprint Review** plus **Sprint Retrospective** close out each cycle to inspect the product and improve the process.

| Role | Responsibility |
| --- | --- |
| Product Owner | Defines and prioritizes the backlog based on business value |
| Scrum Master | Facilitates the process, removes blockers, ensures Scrum practices are followed |
| Development Team | Builds the actual product increment each sprint |

## 5. Requirements Engineering

- **Functional Requirements**: define what the system should *do* (e.g., "user can reset password").
- **Non-Functional Requirements**: define system qualities like performance, security, scalability, usability.
- **SRS (Software Requirements Specification)**: a formal document capturing all functional and non-functional requirements, acting as a contract between stakeholders and developers.

## 6. Software Design Principles

**How they work together**: These principles guide developers toward code that is easier to maintain, extend, and test.

- **Modularity**: breaking a system into independent, self-contained modules that can be developed and tested separately.
- **Coupling**: degree of interdependency between modules — **low coupling** (modules interact minimally) is desirable.
- **Cohesion**: degree to which elements within a single module belong together — **high cohesion** (a module does one focused thing well) is desirable.
- **Abstraction**: hiding complex implementation details behind a simple interface.
- **Encapsulation**: bundling data and the methods that operate on it together, restricting direct access from outside.

## 7. SOLID Principles — How Each Works

| Principle | Full Form | How It Works |
| --- | --- | --- |
| S | Single Responsibility Principle | A class should have only one reason to change — it should do exactly one job |
| O | Open/Closed Principle | Classes should be open for extension but closed for modification — add new behavior via extension, not by editing existing code |
| L | Liskov Substitution Principle | Objects of a subclass should be replaceable for objects of the superclass without breaking the program |
| I | Interface Segregation Principle | Prefer many small, specific interfaces over one large general-purpose interface, so classes aren't forced to implement unused methods |
| D | Dependency Inversion Principle | High-level modules should depend on abstractions (interfaces), not on concrete low-level implementations |

## 8. Design Patterns — How Key Ones Work

**Singleton Pattern**
How it works: Ensures a class has only one instance throughout the application by making the constructor private and providing a static method that returns the same cached instance every time it's called.

**Factory Pattern**
How it works: Delegates object creation to a separate "factory" method/class instead of using the constructor directly, so the calling code doesn't need to know the exact class being instantiated.

**Observer Pattern**
How it works: One object (the "subject") maintains a list of dependent "observers"; whenever the subject's state changes, it automatically notifies all observers so they can update themselves accordingly (basis for event-driven systems).

**Strategy Pattern**
How it works: Defines a family of interchangeable algorithms, encapsulates each one in its own class, and lets the client choose which algorithm to use at runtime without changing the code that uses it.

**MVC (Model-View-Controller)**
How it works: Separates an application into three parts — **Model** (data and business logic), **View** (UI presentation), and **Controller** (handles user input and coordinates between Model and View) — keeping concerns cleanly separated.

## 9. Software Testing — How Each Type Works

**Unit Testing**
How it works: Tests the smallest testable pieces of code (individual functions/methods) in isolation, usually automated, to confirm each unit behaves correctly on its own.

**Integration Testing**
How it works: Tests how multiple units/modules work together once combined, catching issues that arise from their interactions (e.g., a function passing wrong data format to another module).

**System Testing**
How it works: Tests the complete, fully integrated system against the overall requirements to verify end-to-end behavior.

**Acceptance Testing**
How it works: Performed by or on behalf of the end user/client to confirm the system meets business needs and is ready for release (often called UAT — User Acceptance Testing).

**Black-Box Testing**
How it works: Tester checks inputs and outputs without knowing the internal code structure — focuses purely on whether the system behaves as expected from a user's perspective.

**White-Box Testing**
How it works: Tester has full knowledge of the internal code and designs test cases to cover specific paths, branches, and logic within the code itself.

**Regression Testing**
How it works: Re-runs existing test cases after code changes to make sure new changes haven't broken previously working functionality.

## 10. Testing Levels — Quick Comparison

| Level | Tested By | Focus |
| --- | --- | --- |
| Unit | Developers | Individual functions/methods |
| Integration | Developers/Testers | Interaction between modules |
| System | QA Team | Entire system as a whole |
| Acceptance | End Users/Clients | Business requirements fulfillment |

## 11. Software Metrics & Estimation

- **LOC (Lines of Code)**: a simple but crude size metric, used historically to estimate effort.
- **Function Point Analysis**: measures software size based on the number and complexity of functions it delivers to the user, independent of the programming language.
- **COCOMO (Constructive Cost Model)**: How it works — estimates project effort, time, and cost using formulas based on estimated lines of code and project complexity factors (organic, semi-detached, embedded).

## 12. Version Control

**How it works**: A version control system (like Git) tracks every change made to source code over time, allowing multiple developers to work in parallel without overwriting each other's work, and enabling rollback to any previous state.

- **Branching**: creating a separate line of development to work on a feature without affecting the main codebase.
- **Merging**: combining changes from one branch back into another.
- **Pull Request**: a request to merge changes from one branch into another, typically reviewed by teammates before approval.
- **Merge Conflict**: occurs when two branches make competing changes to the same part of a file, requiring manual resolution.

## 13. CI/CD Pipeline

**Continuous Integration (CI)**
How it works: Developers frequently merge their code changes into a shared repository; each merge automatically triggers a build and a suite of automated tests, catching integration bugs early rather than at the end of development.

**Continuous Deployment/Delivery (CD)**
How it works: Once code passes CI's automated tests, it's automatically (Deployment) or semi-automatically after approval (Delivery) pushed through staging environments and released to production, reducing manual release overhead.

## 14. Software Maintenance Types

- **Corrective Maintenance**: fixing bugs/defects discovered after release.
- **Adaptive Maintenance**: modifying software to work in a new environment (e.g., new OS, new hardware).
- **Perfective Maintenance**: enhancing existing features or improving performance based on user feedback.
- **Preventive Maintenance**: proactively updating code to prevent future problems (e.g., refactoring for maintainability).

## 15. Software Architecture Styles

**Monolithic Architecture**
How it works: The entire application (UI, business logic, data access) is built and deployed as one single, tightly coupled unit.
Trait: Simple to develop and deploy initially, but hard to scale specific parts independently as the app grows.

**Microservices Architecture**
How it works: The application is split into small, independent services, each responsible for a specific business function, communicating with each other over lightweight protocols (usually REST APIs or message queues); each service can be developed, deployed, and scaled independently.
Trait: Highly scalable and flexible, but adds complexity in service coordination, deployment, and monitoring.

**Client-Server Architecture**
How it works: Clients send requests to a central server, which processes them and returns responses; the server manages shared resources like data and centralized logic.

## 16. Software Quality Attributes

- **Scalability**: system's ability to handle increasing load by adding resources.
- **Reliability**: system consistently performs its intended function without failure.
- **Maintainability**: ease with which the system can be modified to fix bugs or add features.
- **Portability**: ease of transferring software to different environments/platforms.
- **Usability**: how easily end users can learn and operate the system.

## 17. Risk Management in SE

**How it works**: Projects identify potential risks (technical, schedule, resource-related) early, assess their probability and impact, and create mitigation plans — monitored continuously throughout the project lifecycle to reduce the chance of failure.

## 18. Quick Interview Traps

- Waterfall is rigid and sequential; Agile is flexible and iterative — Agile handles changing requirements far better.
- Low coupling + high cohesion together produce the most maintainable code.
- SOLID's "O" (Open/Closed) means extend behavior via new code, not by modifying existing tested code.
- Unit testing checks isolated code; integration testing checks how modules interact; system testing checks the whole product.
- Black-box testing ignores code internals; white-box testing requires full code knowledge.
- Monolithic architecture is simpler to build early on; microservices scale better but add operational complexity.
- CI catches bugs early through frequent automated testing; CD automates the release process after CI passes.

