
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

```


```