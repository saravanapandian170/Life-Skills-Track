# Event Sourcing — Architecture, Concepts, and Implementation

## 1. Introduction
Event Sourcing stores every change in the system as an immutable **event** instead of persisting only the current state.  
It provides:
- Complete audit trail  
- Ability to rebuild past states  
- Support for time-based queries  
- Strong pairing with CQRS  

## 2. Why Use Event Sourcing
- **Auditability** – Every change is recorded in order.  
- **Reproducibility** – Replaying events reconstructs any historical state.  
- **Temporal Queries** – Easy to ask “What was the state at time X?”  
- **Event-Driven Architecture** – Events can integrate with other services.  
- **Scalability** – Reads and writes scale independently with CQRS.  

## 3. Core Concepts
- **Event** – Immutable fact that something happened.  
- **Command** – Intent to perform an action; may produce events.  
- **Aggregate** – Domain object handling commands and emitting events.  
- **Event Store** – Append-only storage of all events.  
- **Projections / Read Models** – Query-optimized views built from events.  
- **Snapshotting** – Saves compressed state to reduce replay cost.  
- **Versioning / Upcasting** – Handles schema evolution of events.  
- **Concurrency Control** – Optimistic locking to avoid conflicts.  

## 4. Architecture Flow
- Command received → Load past events → Rehydrate aggregate → Validate command  
- Aggregate emits events → Events appended to event store  
- Events published to subscribers → Projections updated  
- Snapshots optionally used to speed up replay  

## 5. Challenges
- Event store grows over time  
- Replaying large histories is costly  
- Event schema evolution is hard  
- Increased architectural complexity  
- Eventual consistency on read models  
- Handling side-effects during event replay  

## 6. Best Practices
- Use Transactional Outbox for reliable event publishing  
- Emit meaningful domain events only  
- Introduce versioning and upcasting early  
- Tune snapshot frequency  
- Design projections for real query use-cases  
- Test replay, snapshots, and concurrency deeply  

## 7. Real-World Use Cases
- Banking and finance  
- E-commerce and ordering systems  
- Gaming platforms  
- Collaboration and version-history tools  
- Analytics and audit systems  

## References
- https://eventuate.io/whyeventsourcing.html?utm_source=chatgpt.com  
- https://www.geeksforgeeks.org/system-design/event-sourcing-pattern/  
- https://docs.aws.amazon.com/prescriptive-guidance/latest/cloud-design-patterns/event-sourcing.html?utm_source=chatgpt.com
