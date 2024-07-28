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

### Level I: Context Diagram
- High-level overview of the system and its interactions with other entities (i.e. user, other systems)
```mermaid
C4Context
    title Autonomous Vehicle Fleet Management System (AVFMS)

    Person(fm, "Fleet Manager", "Interacts with the system via mobile app to monitor and control the fleet")
    System_Boundary(avfms, "Autonomous Vehicle Fleet Management System") {
        System(ma, "Mobile App", "Allows fleet managers to control and monitor the fleet")
        System(tms, "Traffic Management System", "Manages real-time traffic data and optimizes routes")
        System(av, "Autonomous Vehicles", "Fleet of self-driving vehicles")
        System(bff, "BFF", "Hosts the backend services and stores relational data")
        System(dt, "Digital Twins", "Stores and provides twin data and acts as a repository for AD software models")
    }

    System_Boundary(ext, "External System Boundary") {
        System_Ext(tpi, "Third-Party Integrations (Mapping Service, GNSS, Weather Service)", "Provides additional functionalities such as route optimization and weather-aware navigation")
    }

    Rel(fm, ma, "Interacts with")
    Rel(fm, tms, "Interacts with")
    Rel(fm, av, "Monitors and controls")
    Rel(tpi, dt, "Integrates with")
    BiRel(av, dt, "Integrates with")
    BiRel(bff, dt, "Integrates with")
    BiRel(ma, bff, "Integrates with")

    UpdateRelStyle(fm, ma, $textColor="brown", $lineColor="black", $offsetY="90")
    UpdateRelStyle(fm, tms, $textColor="brown", $lineColor="black", $offsetY="90")
    UpdateRelStyle(fm, av, $textColor="brown", $lineColor="black", $offsetY="90", $offsetX="255")
    UpdateRelStyle(bff, dt, $textColor="brown", $lineColor="black", $offsetY="30", $offsetX="-10")
    UpdateRelStyle(ma, bff, $textColor="brown", $lineColor="black")
    UpdateRelStyle(av, dt, $textColor="brown", $lineColor="black")
    UpdateRelStyle(tpi, dt, $textColor="black", $lineColor="brown")

    UpdateElementStyle(fm, $fontColor="orange", $bgColor="black", $borderColor="orange")
    UpdateElementStyle(bff, $fontColor="orange", $bgColor="black", $borderColor="orange")
    UpdateElementStyle(tpi, $fontColor="orange", $bgColor="black", $borderColor="orange")
    UpdateElementStyle(ma, $fontColor="orange", $bgColor="black", $borderColor="orange")
    UpdateElementStyle(tms, $fontColor="orange", $bgColor="black", $borderColor="orange")
    UpdateElementStyle(av, $fontColor="orange", $bgColor="black", $borderColor="orange")
    UpdateElementStyle(dt, $fontColor="orange", $bgColor="black", $borderColor="orange")


    UpdateLayoutConfig($c4ShapeInRow="3", $c4BoundaryInRow="1")

```

# Level II: Container Diagram

```mermaid
C4Container
    title Autonomous Vehicle Fleet Management System - Container Diagram

    Person(fm, "Fleet Manager", "Manages and monitors the fleet")

    System_Boundary(autonomous_vehicle_system, "Autonomous Vehicle Fleet Management System") {
        Container(ma, "Mobile App", "iOS, Android", "Allows fleet managers to control and monitor the fleet")
        Container(tms, "Traffic Management System", "Real-time traffic data management", "Optimizes routes based on traffic data")
        Container(av, "Autonomous Vehicles", "ROS2, Pyhon/C++", "Participates in the fleet and receives commands from the system")
        Container(api, "BFF", "NestJS, NodeJS", "Handles requests from the mobile app and other services as a BFF")
        Container(dt, "Digital Twins", "Eclipse Ditto", "Hosts digital twin data, avaialble software models to run on the edge")
    }

    System_Boundary(ext, "External System Boundary") {
        System_Ext(tpi, "Third-Party Integrations (Mapping Service, GNSS, Weather Service)", "Provides additional functionalities such as route optimization and weather-aware navigation")
    }

    Rel(fm, ma, "Uses")
    Rel(ma, api, "Sends requests to")
    Rel(api, tms, "Fetches traffic data from")
    Rel(api, av, "Sends commands to")
    Rel(api, dt, "Stores and retrieves data from")
    Rel(dt, tpi, "Integrates with")

    UpdateElementStyle(fm, $fontColor="orange", $bgColor="black", $borderColor="orange")
    UpdateElementStyle(api, $fontColor="orange", $bgColor="black", $borderColor="orange")
    UpdateElementStyle(tpi, $fontColor="orange", $bgColor="black", $borderColor="orange")
    UpdateElementStyle(ma, $fontColor="orange", $bgColor="black", $borderColor="orange")
    UpdateElementStyle(tms, $fontColor="orange", $bgColor="black", $borderColor="orange")
    UpdateElementStyle(av, $fontColor="orange", $bgColor="black", $borderColor="orange")
    UpdateElementStyle(dt, $fontColor="orange", $bgColor="black", $borderColor="orange")


    UpdateLayoutConfig($c4ShapeInRow="3", $c4BoundaryInRow="1")
```