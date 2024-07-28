# Assignment One

## Task

- Research [c4 model](c4model.com) and exemplify each diagram type.

## Research

### C4 Model

```
1. A set of hierarchical abstractions (software systems, containers, components, and code)***
2. A set of hierarchical diagrams (system context, containers, components, and code).
3. Notation independent.
4. Tooling independent.
```

### Attributes
- Easy to learn
- Dev friendly ('they say')
- Enables communication
- Facilitates following processes (and more):
  - onboarding
  - review/eval
  - risk identification
  - threat modeling
- Standardization (unifying)
- Abstraction-first approach

### Abstractions
A `softare system` is "mapped" using following abstract terms and concepts:
- `containers`: a top-level encapsulating entity, that hosts other relatively small parts ('components')
- `component` : "...a group of related functionality, encapsulated behind a well-defined interface."
- `code`: concrecte implementation of components in a programming language (vai its constructs: classes, interfaces, functions etc...)
- there is also `people` involved btw.


## Sample Diagrams

### Level I: Context
- High-level overview of the system and its interactions with other entities (i.e. user, other systems)
```mermaid
C4Context
    title Autonomous Vehicle Fleet Management System

    Person(fm, "Fleet Manager", "Interacts with the system via mobile app to monitor and control the fleet")
    System_Boundary(autonomous_vehicle_system, "Autonomous Vehicle Fleet Management System") {
        System(ma, "Mobile App", "Allows fleet managers to control and monitor the fleet")
        System(tms, "Traffic Management System", "Manages real-time traffic data and optimizes routes")
        System(av, "Autonomous Vehicles", "Fleet of self-driving vehicles")
        System(cs, "Cloud Service", "Hosts the backend services and stores data")
    }

    System_Ext(tpi, "Third-Party Integrations (Mapping Service, Weather Service)", "Provides additional functionalities such as route optimization and weather-aware navigation")

    Rel(fm, ma, "Interacts with")
    Rel(fm, tms, "Interacts with")
    Rel(fm, av, "Monitors and controls")
    Rel(tpi, cs, "Integrates with")


```