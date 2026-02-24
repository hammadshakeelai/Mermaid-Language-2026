```mermaid
classDiagram
    Sensor {
        SenseOutput
    }
    Arduino {
        SenseOutput
    }
    Sensor <|-- Arduino
```