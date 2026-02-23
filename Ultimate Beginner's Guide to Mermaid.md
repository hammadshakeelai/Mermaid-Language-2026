
# 🧜‍♂️ The Ultimate Beginner's Guide to Mermaid.js

Mermaid is a JavaScript-based diagramming and charting tool that renders Markdown-inspired text definitions to create and modify diagrams dynamically. 

## 🛠️ 1. Environment Setup
To write and view Mermaid diagrams, you need an environment that supports it:
* **VS Code:** Install the **Markdown Preview Mermaid Support** extension. Create a `.md` file, write your code, and open the Markdown preview to see your diagrams live.
* **Browser:** Use the [Mermaid Live Editor](https://mermaid.live). It's great for quick testing, sharing links, and downloading your diagrams as PNG, SVG, or PDF files.

---

## 🌊 2. Flowcharts (Graphs)
Flowcharts are used to represent workflows, processes, or systems step-by-step.

### Defining the Direction
* `flowchart TD`: **T**op to **D**own (Vertical)
* `flowchart LR`: **L**eft to **R**ight (Horizontal)

### Example: Custom OS Boot Sequence
```mermaid
flowchart TD
    A[Power On] --> B(BIOS / UEFI)
    B --> C{Custom Bootloader Found?}
    C -->|Yes| D[Load Bootloader into Memory]
    C -->|No| E[Halt System]
    D --> F((Execute Custom OS Kernel))
    F --> G[Initialize System Processes]

```

---

## ⏱️ 3. Sequence Diagrams

Sequence diagrams show how processes operate with one another and in what order. They are perfect for mapping out system interactions, API calls, or inter-process communication (IPC).

### Core Syntax

* `participant [Name]`: Defines the actors/systems.
* `->>`: Solid line with arrowhead (Message/Request).
* `-->>`: Dotted line with arrowhead (Response/Return).
* `activate` / `deactivate`: Creates a vertical box on the participant's lifeline to show active processing.

### Example: Inter-Process Communication (fork & wait)

```mermaid
sequenceDiagram
    autonumber
    participant Parent Process
    participant OS Scheduler
    participant Child Process
    
    Parent Process->>OS Scheduler: System Call: fork()
    activate OS Scheduler
    OS Scheduler->>Child Process: Allocate Memory & Clone
    activate Child Process
    OS Scheduler-->>Parent Process: Return Child PID
    deactivate OS Scheduler
    
    Child Process->>Child Process: Execute Task
    Child Process-->>OS Scheduler: exit(status)
    deactivate Child Process
    
    Parent Process->>OS Scheduler: System Call: wait()
    OS Scheduler-->>Parent Process: Return Termination Status

```

---

## 🏗️ 4. Class Diagrams

Class diagrams are essential in Software Engineering and Object-Oriented Programming (OOP) to show system structure by detailing classes, attributes, methods, and relationships.

### Class Anatomy

* `+` : Public
* `-` : Private
* `#` : Protected

### Relationships

* `<|--` : **Inheritance** * `o--` : **Aggregation** (Weak relationship)
* `*--` : **Composition** (Strong relationship)

### Example: PID Line-Following Robot Architecture

```mermaid
classDiagram
    class LineFollowerRobot {
        +String status
        +startNavigation()
        +stop()
    }
    
    class PIDController {
        -float kp
        -float ki
        -float kd
        +calculateError(float sensorInput) float
    }
    
    class MotorDriver {
        -int leftPin
        -int rightPin
        +setSpeed(int leftSpeed, int rightSpeed)
        +reverseTurningLogic()
    }
    
    class IRSensorArray {
        +readValues() int[]
    }

    LineFollowerRobot *-- PIDController : Uses
    LineFollowerRobot *-- MotorDriver : Controls
    LineFollowerRobot o-- IRSensorArray : Reads

```

---

## 🗄️ 5. Entity Relationship Diagrams (ERD)

ERDs are used in Database Management Systems (DBMS) to show how tables (entities) relate to one another.

### Cardinality (Crow's Foot Notation)

* `||--o{` : **One to Zero-or-Many** * `||--||` : **Exactly One to Exactly One** * `}o--o{` : **Many to Many** ### Example: University Registration System

```mermaid
erDiagram
    STUDENT ||--o{ ENROLLMENT : registers_for
    COURSE ||--o{ ENROLLMENT : contains
    
    STUDENT {
        int student_id PK
        string full_name
        string email
        int current_semester
    }
    
    COURSE {
        string course_code PK
        string course_title
        int credit_hours
    }
    
    ENROLLMENT {
        int enrollment_id PK
        int student_id FK
        string course_code FK
        date enrollment_date
    }

```

---

## 🎁 Bonus: Pie Charts

Pie charts are incredibly easy to format. Just provide the title and the key-value pairs.

### Example: Algorithm Performance Distribution

```mermaid
pie title CPU Time Spent on Sorting Algorithms
    "Merge Sort (O(n log n))" : 45
    "Quick Sort (O(n log n))" : 35
    "Bubble Sort (O(n^2))" : 15
    "Insertion Sort" : 5

```


---

# 🎨 The Mermaid.js Masterclass: Styling, Advanced Diagrams, and System Architecture

Mermaid is not just for black-and-white boxes. It contains a powerful rendering engine that supports CSS styling, complex logic flows, and project management tools.

## 🖌️ Part 1: The Art of Styling Nodes & Links

You can color-coordinate your flowcharts to make them readable at a glance. There are two main ways to do this: Inline Styling and Class-Based Styling.

### Method A: Inline Styling (`style`)

You apply CSS directly to a specific node using its ID.

```mermaid
flowchart TD
    A[Start Minecraft Server] --> B{Is Aternos Online?}
    B -->|Yes| C[Connect to IP]
    B -->|No| D[Wait in Queue]

    style A fill:#4CAF50,stroke:#388E3C,stroke-width:2px,color:#fff
    style D fill:#F44336,stroke:#D32F2F,stroke-width:4px,color:#fff,stroke-dasharray: 5 5

```

* `fill`: The background color (hex codes work best).
* `stroke`: The border color.
* `stroke-width`: Border thickness.
* `color`: Text color.
* `stroke-dasharray`: Creates dotted/dashed borders.

### Method B: Class-Based Styling (`classDef` & `class`)

If you have multiple nodes that need the same style (e.g., all database nodes are blue, all error nodes are red), inline styling is too slow. Instead, define a class and apply it.

```mermaid
flowchart LR
    classDef success fill:#28d000,stroke:#28a745,stroke-width:2px;
    classDef error fill:#dc354a,stroke:#dc3545,stroke-width:2px;
    classDef process fill:#4fabef,stroke:#007bff,stroke-width:2px;

    User --> API(API Gateway):::process
    API --> Auth{Valid Token?}
    Auth -->|Yes| DB[(Database)]:::success
    Auth -->|No| Reject[403 Forbidden]:::error

```

* Define the class: `classDef [className] [cssProperties]`
* Apply the class directly: Add `:::[className]` to the end of the node definition.

---

## 📦 Part 2: Subgraphs (Grouping Components)

Subgraphs allow you to group related nodes together inside a larger bounding box. This is crucial for visualizing software architecture or separating different systems.

```mermaid
flowchart TD
    subgraph Frontend [Client Side Architecture]
        UI[React UI] --> State[Redux Store]
    end

    subgraph Backend [Server Side Architecture]
        API[Express API] --> Auth[JWT Middleware]
    end

    subgraph Infrastructure [Data Layer]
        DB[(PostgreSQL)]
        Cache[(Redis Cache)]
    end

    State -.-> API
    Auth --> DB
    Auth --> Cache

```

* Use `subgraph [ID] [Optional Title]` to open the group.
* Use `end` to close it.
* Notice the `-.->` arrow? That creates a **dotted link** instead of a solid one.

---

## 🔄 Part 3: Advanced Sequence Diagrams

Sequence diagrams can handle complex logic like `if/else` statements, loops, and parallel processes using specialized blocks.

### Loops, Alt (If/Else), and Opt (Optional)

```mermaid
sequenceDiagram
    autonumber
    participant Client as GapHunter Frontend
    participant Server as Backend API
    participant DB as DBMS
    
    Client->>Server: Request Competitor Data (Target URL)
    
    alt Data Exists in Cache
        Server-->>Client: Return Cached JSON
    else Data Needs Scraping
        Server->>Server: Initialize Scraper Worker
        
        loop Every Pagination Page
            Server->>TargetSite: HTTP GET
            TargetSite-->>Server: Raw HTML
            Server->>Server: Parse DOM
        end
        
        Server->>DB: INSERT Extracted Data
        DB-->>Server: Confirm Write
        Server-->>Client: Return Fresh JSON
    end
    
    opt User Requested Email Alert
        Server->>EmailService: Dispatch Alert
    end

```

* `alt ... else ... end`: Represents conditional logic (If this, do X, else do Y).
* `loop ... end`: Represents an iterative process.
* `opt ... end`: Represents an optional step that only occurs under certain conditions.

---

## 🚦 Part 4: State Diagrams

State diagrams are used to describe the behavior of a system in terms of its states and the transitions between them. They are heavily used in hardware, robotics, and game development.

```mermaid
stateDiagram-v2
    [*] --> FindingLine : Initialize Variables
    
    FindingLine --> CorrectingLeft : Right Sensor detects line
    FindingLine --> CorrectingRight : Left Sensor detects line
    
    state CorrectingLeft {
        [*] --> ReverseTurningLogic
        ReverseTurningLogic --> TurnLeft
    }
    
    state CorrectingRight {
        [*] --> ReverseTurningLogic2
        ReverseTurningLogic2 --> TurnRight
    }
    
    CorrectingLeft --> FindingLine : Centered
    CorrectingRight --> FindingLine : Centered
    FindingLine --> Stop : Both Sensors High
    Stop --> [*] : Power Off

```

* `[*]`: Represents the start or end point.
* `-->`: The transition between states.
* You can nest states within other states for complex state machines (like the correcting logic above).

---

## 📅 Part 5: Gantt Charts (Project Planning)

Mermaid can render standard Gantt charts, which are excellent for tracking semester projects, sprints, or personal goals.

```mermaid
gantt
    title 4th Semester Workload & Project Timeline
    dateFormat  YYYY-MM-DD
    section Core Subjects
    Analysis of Algorithms Exam Prep  :a1, 2026-03-01, 14d
    DBMS Midterms                     :a2, after a1, 7d
    Intro to AI Assignments           :a3, 2026-03-05, 10d
    
    section Software Engineering
    Virtual Smart Backup (VSB) UI     :b1, 2026-03-01, 10d
    VSB API Integration               :b2, after b1, 15d
    Testing & QA                      :b3, after b2, 5d
    
    section Leisure
    Watch Jujutsu Kaisen S3           :c1, 2026-03-10, 3d
    Minecraft Server Maintenance      :c2, 2026-03-15, 2d

```

* `dateFormat`: Tells Mermaid how to read your dates.
* `section`: Groups tasks together.
* `[Task Name] : [ID], [Start Date], [Duration]`
* You can use `after [ID]` to make tasks sequential automatically.

---

## 🔀 Part 6: Git Graphs

If you are working on software, understanding branching is key. Mermaid has a dedicated graph type for visualizing Git version control history.

```mermaid
gitGraph
    commit id: "Initial Project Setup"
    branch feature/custom-bootloader
    checkout feature/custom-bootloader
    commit id: "Write ASM boot sector"
    commit id: "Switch to 32-bit protected mode"
    checkout main
    commit id: "Update README"
    merge feature/custom-bootloader
    branch bugfix/memory-leak
    checkout bugfix/memory-leak
    commit id: "Fix dangling pointers in kernel"
    checkout main
    merge bugfix/memory-leak tag: "v1.0"

```

* `commit id: "..."`: Creates a node on the current branch.
* `branch [name]`: Creates a new line.
* `checkout [name]`: Switches the active context to that branch.
* `merge [name]`: Brings the branch back into the current active branch.

---

