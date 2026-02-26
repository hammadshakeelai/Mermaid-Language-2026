# Mermaid

Practising...


# Flowcharts
```mermaid
flowchart TD
    A[ass] --> B[Bomb] --> T[Taliban]
    T --> TT[Twin Towers] --> A
    B --> A --> T
    B --> TT --> B
```
```mermaid
flowchart TD 
    X[Input] --> F(Function) --> Y[Output]
```
```mermaid
flowchart TD 
    X[data] --> F((preprocessing)) --> Y[information]
```
```mermaid
flowchart TD 
    X[Question] --> F{Yes/No} --> Y[Result]
```
```mermaid
flowchart LR 
    X[Play Angry Birds] --> F{Game Asks Are You A Bird} 
    F -->|NO| Y(You Filthy Pig)
    F -->|YES| Z{{Comes, Let Take Back Ye Eggs}}
```
```mermaid
flowchart TD
    P --> LOOP
    LOOP --> P
    X[START] -->|INPUT| P[PROCESS]
    P -->|OUTPUT| E[END]
```
# Sequence Diagrams
<!--  autonumber for numbering in steps -->
```mermaid
sequenceDiagram

    participant Client
    participant OAuth Provider
    participant Server
    activate Client
    Client->>OAuth Provider: Request access token
    activate OAuth Provider
    OAuth Provider->>Client: Sends access token
    deactivate OAuth Provider
    Client->>Server: Requests Resource
    Server->>OAuth Provider: Authentication Request
    OAuth Provider->>Server: Authenticates
    Server->>Client: Sends Resource
    deactivate Client
```
```mermaid
    sequenceDiagram
        participant omar
        participant me
        participant bus
        participant university
        bus ->> me: reaches my stop
        activate me
        me ->> bus: gets on
        deactivate me
        activate bus
        bus ->> omar: reaches omar stop
        deactivate bus
        activate omar
        omar ->> bus: gsts on bus
        deactivate omar
        activate bus
        bus ->> university: reached uni
    
```
# Class Diagrams

```mermaid
classDiagram
    class Order {
        +OrderStatus status
    }
    class OrderStatus {
        <<enumeration>>
        FAILED
        PENDING
        PAID
    }
    class PaymentProcessor {
        <<interface>>
        -String apikey
        #conect(String url,, JSON header)
        +processPayment(Order order) OrderStatus
    }
    class Customer {
        +String name
    }
    Customer <|-- PrivateCustomer
    Customer <|-- BusinessCustomer
    PaymentProcessor <|.. StripePaymentProcessor
    PaymentProcessor <|.. PaypalPaymentProcessor
    Order o-- Customer
    car *-- engine
```
"o"  for aggregation
"*"  for composition

# Entity Relationship Diagrams
#### ERD == erDiagram
for a simple e-commerce system
![1771880928354](image/MERMAID/1771880928354.png)
```mermaid
erDiagram
    Mehmood ||--o{ Me: Contacts
    Me ||--|| Whatsapp : uses
    Mehmood {
        String name
        String phoneNumber
    }
    Me {
        String name
        String sextype
        mobile phone 
    }
    Whatsapp {
        String color
        String pin
    }
```