# Microservices Engineering Roadmap

A practical roadmap for learning **microservices, distributed systems, event-driven architecture, resilience, observability, and cloud-native deployment** using Node.js + TypeScript.

The goal is not to learn a collection of tools. The goal is to understand **why distributed systems require different architectural patterns and what failure modes those patterns introduce**.

---

## Tech Stack

Primary stack:

- Node.js
- TypeScript
- MongoDB
- Redis
- RabbitMQ
- Docker
- Kubernetes
- Prometheus
- Grafana
- OpenTelemetry
- GitHub Actions
- AWS
- Terraform

Later:

- Apache Kafka
- Service Mesh
- Istio / Linkerd

---

# Learning Path

```text
Distributed Systems Fundamentals
            ↓
     Modular Monolith
            ↓
     Service Boundaries
            ↓
    HTTP Communication
            ↓
 Database-per-Service
            ↓
  Redis & Concurrency
            ↓
 Async Messaging / RabbitMQ
            ↓
 Event-Driven Architecture
            ↓
 Idempotency & Consistency
            ↓
 Distributed Transactions
            ↓
       Saga Pattern
            ↓
    Resilience Patterns
            ↓
       API Gateway
            ↓
 Authentication & Authorization
            ↓
       Observability
            ↓
    Production Docker
            ↓
       Kubernetes
            ↓
          Kafka
            ↓
       CI/CD
            ↓
       Terraform
            ↓
 Advanced Distributed Systems
            ↓
       Service Mesh
```

---

# Phase 0 — Prerequisites

**Estimated time: 1 week**

Before starting microservices, understand the fundamentals required to operate distributed applications.

## Networking

- [ ] HTTP
- [ ] HTTPS
- [ ] TCP/IP basics
- [ ] DNS
- [ ] Ports
- [ ] Connection lifecycle
- [ ] Reverse proxy
- [ ] Load balancing
- [ ] WebSockets
- [ ] HTTP status codes

Understand:

```text
Client
  ↓
DNS
  ↓
Load Balancer
  ↓
Reverse Proxy
  ↓
Application
```

## Docker

- [ ] Images
- [ ] Containers
- [ ] Dockerfile
- [ ] Docker Compose
- [ ] Networks
- [ ] Volumes
- [ ] Environment variables
- [ ] Health checks
- [ ] Container restart policies

You should be able to run:

```text
service-a
service-b
mongodb
redis
rabbitmq
```

using Docker Compose.

---

# Phase 1 — Distributed Systems Fundamentals

**Estimated time: 1–2 weeks**

This is the most important theoretical phase.

## Learn

- [ ] What is a distributed system?
- [ ] Process vs service
- [ ] Container vs process
- [ ] Partial failure
- [ ] Network failure
- [ ] Latency
- [ ] Timeouts
- [ ] Retries
- [ ] Duplicate requests
- [ ] Duplicate messages
- [ ] Message loss
- [ ] Service unavailability
- [ ] Cascading failures
- [ ] Eventual consistency
- [ ] Strong consistency

Understand why:

```text
function call
```

is fundamentally different from:

```text
Service A
   ↓
network
   ↓
Service B
```

### Exercise

Build:

```text
client
  ↓
service-a
  ↓ HTTP
service-b
```

Then intentionally stop `service-b`.

Observe what happens.

---

# Phase 2 — Modular Monolith

**Estimated time: 1–2 weeks**

Before splitting into microservices, build a properly structured monolith.

## Example

```text
src/
├── modules/
│   ├── users/
│   ├── events/
│   ├── inventory/
│   ├── orders/
│   ├── payments/
│   └── notifications/
│
├── shared/
└── infrastructure/
```

## Learn

- [ ] Module boundaries
- [ ] Dependency inversion
- [ ] Clean Architecture
- [ ] Domain layer
- [ ] Application layer
- [ ] Infrastructure layer
- [ ] Domain events
- [ ] Bounded contexts

Avoid direct database access from every module.

Bad:

```text
Controller
   ↓
MongoDB
```

Better:

```text
Controller
   ↓
Use Case
   ↓
Repository
   ↓
Database
```

---

# Phase 3 — Service Boundaries

**Estimated time: 1 week**

Learn how to decide what should become a service.

Do not create services based purely on database tables.

Bad:

```text
UserService
AddressService
PhoneService
NameService
```

Better:

```text
Identity Service
Event Service
Order Service
Inventory Service
Payment Service
Notification Service
```

## Learn

- [ ] Bounded Context
- [ ] Business capability
- [ ] Aggregate
- [ ] Entity
- [ ] Value Object
- [ ] Domain Event
- [ ] Service boundaries
- [ ] Data ownership

The key question:

> If this becomes a separate service, what business responsibility does it own?

---

# Phase 4 — First Microservice

**Estimated time: 1–2 weeks**

Extract one module from the monolith.

Example:

```text
Order Service
      │
      │ HTTP
      ↓
Payment Service
```

## Learn

- [ ] Service-to-service HTTP
- [ ] REST APIs
- [ ] Request validation
- [ ] Error handling
- [ ] Timeouts
- [ ] Service configuration
- [ ] Health checks
- [ ] Service authentication

## Failure exercise

Stop the payment service:

```bash
docker stop payment-service
```

Test:

```text
Create Order
    ↓
Payment
    ↓
FAIL
```

Answer:

- What happens to the request?
- Does it timeout?
- Does it retry?
- How many times?
- What does the client receive?
- What happens when Payment comes back?

---

# Phase 5 — Database per Service

**Estimated time: 1 week**

Each service should own its persistent data.

Avoid:

```text
Order Service ─┐
Payment Service ├──► Shared Database
User Service ──┘
```

Prefer:

```text
Order Service
      ↓
Order DB

Payment Service
      ↓
Payment DB

User Service
      ↓
User DB
```

## Learn

- [ ] Data ownership
- [ ] Database-per-service
- [ ] Data duplication
- [ ] Eventual consistency
- [ ] Read models
- [ ] Cross-service queries
- [ ] Consistency boundaries

Understand:

> A microservice should not directly query another service's database.

---

# Phase 6 — Concurrency & Idempotency

**Estimated time: 1 week**

This phase is critical for real-world systems.

## Race Conditions

Understand:

```text
Stock = 1

Request A → Read stock = 1
Request B → Read stock = 1

A → decrement
B → decrement
```

## Learn

- [ ] Race conditions
- [ ] Atomic operations
- [ ] Optimistic locking
- [ ] Pessimistic locking
- [ ] Database transactions
- [ ] Idempotency
- [ ] Idempotency keys
- [ ] Distributed locks

### Example

Atomic inventory operation:

```sql
UPDATE products
SET stock = stock - 1
WHERE id = ?
AND stock > 0;
```

Only one request can successfully consume the final unit.

---

# Phase 7 — Redis

**Estimated time: 1 week**

Learn Redis as a distributed systems tool, not just as a cache.

## Learn

- [ ] Strings
- [ ] Hashes
- [ ] Sets
- [ ] Sorted Sets
- [ ] TTL
- [ ] Atomic commands
- [ ] `SET NX`
- [ ] Lua scripts / Redis Functions
- [ ] Distributed locks
- [ ] Rate limiting
- [ ] Temporary reservations
- [ ] Caching

## Event Seat Reservation

Example:

```text
Seat A10
    ↓
Redis reservation
    ↓
5 minute TTL
    ↓
Payment
    ↓
Database booking
```

Redis:

```text
seat:event123:A10
        ↓
     user123
        ↓
     TTL: 300
```

Database:

```text
event123 + A10
        ↓
      BOOKED
```

Redis handles temporary reservation.

Database remains the persistent source of truth.

---

# Phase 8 — Message Brokers

**Estimated time: 1–2 weeks**

Start with **RabbitMQ**.

Architecture:

```text
Order Service
      │
      │ OrderCreated
      ▼
   RabbitMQ
      │
      ├──────► Notification
      │
      ├──────► Inventory
      │
      └──────► Analytics
```

## Learn

- [ ] Producer
- [ ] Consumer
- [ ] Queue
- [ ] Exchange
- [ ] Routing key
- [ ] Acknowledgement
- [ ] Retry
- [ ] Dead-letter queue
- [ ] Message ordering
- [ ] Competing consumers
- [ ] At-least-once delivery
- [ ] Consumer idempotency

Important:

> At-least-once delivery means the same message may be processed more than once.

Therefore:

```text
Consumer
   ↓
Must be idempotent
```

---

# Phase 9 — Event-Driven Architecture

**Estimated time: 1 week**

Understand the difference between synchronous and asynchronous communication.

## Synchronous

```text
Order
  │
  │ HTTP
  ▼
Payment
```

## Asynchronous

```text
Order
  │
  │ PaymentRequested
  ▼
RabbitMQ
  │
  ▼
Payment
```

## Learn

- [ ] Domain events
- [ ] Integration events
- [ ] Event producers
- [ ] Consumers
- [ ] Eventual consistency
- [ ] Event-driven architecture
- [ ] Event contracts
- [ ] Event versioning

---

# Phase 10 — Outbox Pattern

**Estimated time: 3–5 days**

Learn the dual-write problem.

Bad:

```text
Database transaction
      ↓
SUCCESS

Publish event
      ↓
FAIL
```

Now your database says:

```text
Order Created
```

but RabbitMQ never received:

```text
OrderCreated
```

## Outbox

```text
Order DB
├── orders
└── outbox_events
          │
          ▼
      Publisher
          │
          ▼
       RabbitMQ
```

The order and event are written in the same database transaction.

## Learn

- [ ] Transactional Outbox
- [ ] Event publisher
- [ ] Event retries
- [ ] Duplicate events
- [ ] Idempotent consumers

---

# Phase 11 — Distributed Transactions

**Estimated time: 1–2 weeks**

Understand why traditional database transactions don't work across independent services.

Example:

```text
Create Order
     ↓
Reserve Inventory
     ↓
Charge Payment
     ↓
Confirm Order
```

What happens if:

```text
Inventory ✓
Payment ✗
```

You cannot simply:

```text
ROLLBACK
```

across independent databases.

---

# Phase 12 — Saga Pattern

**Estimated time: 1 week**

Learn two approaches.

## Choreography

```text
OrderCreated
      ↓
InventoryReserved
      ↓
PaymentCompleted
      ↓
OrderConfirmed
```

## Orchestration

```text
           Saga
        Orchestrator
        /    |     \
       ↓     ↓      ↓
    Order Inventory Payment
```

## Learn

- [ ] Saga
- [ ] Saga orchestration
- [ ] Saga choreography
- [ ] Compensating transaction
- [ ] Failure recovery
- [ ] Eventual consistency

Example:

```text
Reserve Inventory
       ↓
Payment Failed
       ↓
Release Inventory
```

---

# Phase 13 — Resilience Patterns

**Estimated time: 1 week**

Distributed systems fail.

Design for failure.

## Learn

### Timeouts

```text
Service A
   ↓
Service B
   ↓
timeout
```

### Retries

```text
1s
2s
4s
8s
```

Learn exponential backoff.

### Circuit Breaker

```text
Payment failing
      ↓
Circuit OPEN
      ↓
Stop calling Payment
```

### Bulkhead

Isolate resources between dependencies.

### Rate Limiting

Protect services from overload.

### Backpressure

Prevent producers from overwhelming consumers.

## Checklist

- [ ] Timeout
- [ ] Retry
- [ ] Exponential backoff
- [ ] Jitter
- [ ] Circuit breaker
- [ ] Bulkhead
- [ ] Rate limiting
- [ ] Backpressure

---

# Phase 14 — API Gateway

**Estimated time: 3–5 days**

Architecture:

```text
                 ┌── Identity
                 │
Client → Gateway ├── Events
                 │
                 ├── Orders
                 │
                 ├── Payments
                 │
                 └── Inventory
```

## Learn

- [ ] Routing
- [ ] Authentication
- [ ] Authorization
- [ ] Rate limiting
- [ ] Request aggregation
- [ ] Timeouts
- [ ] API composition

Understand the difference between:

```text
Reverse Proxy
API Gateway
Load Balancer
Service Mesh
```

They are not the same thing.

---

# Phase 15 — Authentication & Authorization

**Estimated time: 1 week**

Learn authentication in a distributed environment.

Example:

```text
Client
  │
  │ JWT
  ▼
Gateway
  │
  ▼
Order Service
  │
  ▼
Payment Service
```

## Learn

- [ ] JWT
- [ ] Access tokens
- [ ] Refresh tokens
- [ ] OAuth 2.0
- [ ] OpenID Connect
- [ ] Service-to-service authentication
- [ ] Service identities
- [ ] Authorization
- [ ] Scopes
- [ ] Permissions

Understand what each service is allowed to trust.

---

# Phase 16 — Observability

**Estimated time: 1–2 weeks**

With multiple services, debugging requires more than logs.

## Logging

Use structured logging:

```json
{
  "level": "error",
  "service": "payment",
  "requestId": "abc123",
  "message": "Payment failed"
}
```

Learn:

- [ ] Structured logging
- [ ] Correlation IDs
- [ ] Request IDs
- [ ] Log levels
- [ ] Centralized logging

## Metrics

Use:

```text
Prometheus
    ↓
Grafana
```

Monitor:

```text
request rate
error rate
latency
CPU
memory
queue depth
```

## Distributed Tracing

Learn:

```text
OpenTelemetry
```

Trace:

```text
Gateway
   ↓
Order
   ↓
Payment
   ↓
RabbitMQ
   ↓
Notification
```

---

# Phase 17 — Production Docker

**Estimated time: 1 week**

Learn:

- [ ] Multi-stage builds
- [ ] Small images
- [ ] Non-root containers
- [ ] Health checks
- [ ] Graceful shutdown
- [ ] Resource limits
- [ ] Container networking
- [ ] Persistent volumes
- [ ] Secrets
- [ ] Configuration
- [ ] Restart policies

Deploy the complete system using Docker Compose first.

---

# Phase 18 — Kubernetes

**Estimated time: 2–4 weeks**

Only start Kubernetes after understanding the previous phases.

## Learn in this order

```text
Pod
 ↓
Deployment
 ↓
Service
 ↓
ConfigMap
 ↓
Secret
 ↓
Ingress
```

Then:

- [ ] Namespaces
- [ ] Liveness probes
- [ ] Readiness probes
- [ ] Resource requests
- [ ] Resource limits
- [ ] Rolling deployments
- [ ] Replicas
- [ ] Service discovery
- [ ] Jobs
- [ ] CronJobs
- [ ] StatefulSets
- [ ] Horizontal Pod Autoscaler

Understand what Kubernetes solves instead of memorizing YAML.

---

# Phase 19 — Kafka

**Estimated time: 1–2 weeks**

Learn Kafka after RabbitMQ.

Architecture:

```text
Producer
   ↓
Topic
   ↓
Partition
   ↓
Consumer Group
   ↓
Consumer
```

## Learn

- [ ] Topics
- [ ] Partitions
- [ ] Offsets
- [ ] Consumer groups
- [ ] Partition ordering
- [ ] Retention
- [ ] Replay
- [ ] Delivery semantics
- [ ] Consumer scaling

Compare:

```text
RabbitMQ vs Kafka
```

Understand why you would choose one over the other.

---

# Phase 20 — CI/CD

**Estimated time: 1 week**

Build:

```text
Git Push
   ↓
CI
   ↓
Tests
   ↓
Build
   ↓
Docker Image
   ↓
Security Scan
   ↓
Container Registry
   ↓
Deploy
   ↓
Health Check
```

## Learn

- [ ] GitHub Actions
- [ ] Automated tests
- [ ] Docker image publishing
- [ ] Container registry
- [ ] Environment management
- [ ] Database migrations
- [ ] Rolling deployments
- [ ] Rollbacks
- [ ] Blue/green deployment
- [ ] Canary deployment

---

# Phase 21 — Infrastructure as Code

**Estimated time: 1–2 weeks**

Learn Terraform.

Provision:

```text
VPC
EC2 / EKS
Load Balancer
Database
Redis
S3
IAM
Monitoring
```

## Learn

- [ ] Terraform
- [ ] Providers
- [ ] Resources
- [ ] Variables
- [ ] Outputs
- [ ] Modules
- [ ] State
- [ ] Remote state
- [ ] Workspaces
- [ ] AWS infrastructure

Terraform is infrastructure provisioning. It does not teach microservices architecture.

---

# Phase 22 — Advanced Distributed Systems

After the core roadmap:

## Consistency

- [ ] Strong consistency
- [ ] Eventual consistency
- [ ] Read-your-writes consistency
- [ ] CAP theorem
- [ ] Quorum
- [ ] Replication

## Data Architecture

- [ ] CQRS
- [ ] Read models
- [ ] Materialized views
- [ ] Event sourcing

## Distributed Coordination

- [ ] Leader election
- [ ] Leases
- [ ] Consensus
- [ ] Failure detection
- [ ] Distributed coordination

You don't need to implement Raft to understand why consensus exists.

---

# Phase 23 — Service Mesh

Only after Kubernetes.

Architecture:

```text
Service A
    ↓
Sidecar / Data Plane
    ↓
Service B
```

Learn:

- [ ] Service mesh
- [ ] Sidecars
- [ ] mTLS
- [ ] Traffic management
- [ ] Retries
- [ ] Observability
- [ ] Service-to-service policies

Then investigate:

- Istio
- Linkerd

Do not start here.

---

# Capstone Project

Build an **Event Ticketing Platform** throughout the roadmap.

The system should evolve as you progress.

## Architecture

```text
                         Client
                           │
                           ▼
                      API Gateway
                           │
            ┌──────────────┼──────────────┐
            ↓              ↓              ↓
       Identity         Event           Order
       Service          Service         Service
                           │              │
                           ↓              ↓
                       Inventory        Payment
                        Service         Service
                           │              │
                           └──────┬───────┘
                                  ↓
                               RabbitMQ
                                  │
                       ┌──────────┼──────────┐
                       ↓          ↓          ↓
                 Notification  Analytics    Audit
```

---

# Service Responsibilities

## Identity Service

Responsible for:

- Users
- Authentication
- Authorization
- Access tokens
- Refresh tokens

---

## Event Service

Responsible for:

- Events
- Venues
- Event metadata
- Seat maps

---

## Inventory Service

Responsible for:

- Seats
- Seat availability
- Temporary reservations
- Seat release
- Inventory state

Redis can be used for temporary seat reservations.

---

## Order Service

Responsible for:

- Orders
- Order items
- Order state
- Checkout

---

## Payment Service

Responsible for:

- Payment attempts
- Payment state
- Payment confirmation
- Refunds

---

## Notification Service

Responsible for:

- Email
- SMS
- Notifications

Consume events asynchronously.

---

# Database Architecture

```text
Identity Service
      ↓
Identity DB

Event Service
      ↓
Event DB

Inventory Service
      ↓
Inventory DB

Order Service
      ↓
Order DB

Payment Service
      ↓
Payment DB
```

No service should directly query another service's database.

---

# Redis Usage

Use Redis for:

```text
Seat reservations
Rate limiting
Caching
Distributed coordination
Temporary state
```

Example:

```text
seat:event123:A10
        ↓
     user123
        ↓
     TTL: 300s
```

Do not treat Redis as the permanent source of truth for confirmed bookings.

---

# RabbitMQ Events

Example event flow:

```text
OrderCreated
      ↓
RabbitMQ
      ↓
Payment Service

PaymentCompleted
      ↓
RabbitMQ
      ↓
Order Service

OrderConfirmed
      ↓
RabbitMQ
      ↓
Notification Service
```

---

# Concurrency Scenario

The system must correctly handle:

```text
Event
 └── Seat A10
       └── Available = 1
```

Two users:

```text
User A ─────┐
            ├──► Seat A10
User B ─────┘
```

Expected result:

```text
User A → reservation SUCCESS
User B → reservation FAILED
```

Then:

```text
User A
   ↓
Payment
   ↓
Booking confirmed
```

The database must still enforce the final invariant:

```text
(eventId, seatId) UNIQUE
```

Redis handles temporary reservation/coordination.

The database protects permanent correctness.

---

# Failure Scenarios

The capstone is incomplete if it only works when everything works.

Test:

## Payment failure

```text
Order Created
      ↓
Seat Reserved
      ↓
Payment Failed
      ↓
Seat Released
```

---

## Redis failure

```text
Redis unavailable
      ↓
What happens to seat reservation?
```

Design an explicit strategy.

---

## RabbitMQ failure

```text
Database transaction
      ↓
RabbitMQ unavailable
```

Use the Outbox Pattern.

---

## Service failure

```text
Order
  ↓
Payment
  X
```

Test:

- timeout
- retry
- circuit breaker
- recovery

---

## Duplicate request

```text
POST /orders

Idempotency-Key: abc123
```

Send it twice.

Expected:

```text
One logical order
```

---

## Duplicate event

Publish:

```text
PaymentCompleted
PaymentCompleted
```

The consumer must not create two confirmations.

---

# Production Checklist

Before calling the project "production-ready":

## Architecture

- [ ] Clear service boundaries
- [ ] Independent data ownership
- [ ] No cross-service database access
- [ ] Explicit service contracts
- [ ] Versioned events

## Reliability

- [ ] Timeouts
- [ ] Retries
- [ ] Exponential backoff
- [ ] Circuit breakers
- [ ] Idempotency
- [ ] Dead-letter queues
- [ ] Graceful shutdown

## Data

- [ ] Database transactions where required
- [ ] Unique constraints
- [ ] Concurrency control
- [ ] Outbox Pattern
- [ ] Saga where required
- [ ] Eventual consistency understood

## Security

- [ ] Authentication
- [ ] Authorization
- [ ] Service-to-service authentication
- [ ] Secrets management
- [ ] TLS
- [ ] Input validation
- [ ] Rate limiting

## Observability

- [ ] Structured logs
- [ ] Correlation IDs
- [ ] Metrics
- [ ] Dashboards
- [ ] Distributed tracing
- [ ] Alerts

## Deployment

- [ ] Docker
- [ ] Health checks
- [ ] Kubernetes
- [ ] Rolling deployments
- [ ] CI/CD
- [ ] Automated rollback strategy

---

# Recommended Learning Order

If time is limited, prioritize:

```text
1.  Distributed Systems
2.  Modular Monolith
3.  Service Boundaries
4.  HTTP Microservices
5.  Database-per-Service
6.  Concurrency
7.  Idempotency
8.  Redis
9.  RabbitMQ
10. Event-Driven Architecture
11. Outbox Pattern
12. Saga
13. Resilience
14. API Gateway
15. Authentication
16. Observability
17. Docker
18. Kubernetes
19. Kafka
20. CI/CD
21. Terraform
22. Advanced Distributed Systems
23. Service Mesh
```

---

# Rules for Learning

For every technology or pattern, answer these questions:

### 1. What problem does it solve?

Example:

```text
Redis reservation
→ Temporary concurrency control
```

### 2. What new problem does it introduce?

```text
Redis reservation
→ Consistency between Redis and database
```

### 3. What happens when it fails?

```text
Redis unavailable
→ Can users still purchase?
```

### 4. What simpler solution could solve the same problem?

```text
Redis lock
vs
Database atomic update
```

If you cannot answer these questions, you have learned the API, not the architecture.

---

# Progress Tracker

```text
## Fundamentals
- [ ] Networking
- [ ] Docker
- [ ] Distributed systems

## Architecture
- [ ] Modular monolith
- [ ] Bounded contexts
- [ ] Service boundaries
- [ ] Database-per-service

## Communication
- [ ] HTTP
- [ ] RabbitMQ
- [ ] Events
- [ ] Outbox

## Consistency
- [ ] Race conditions
- [ ] Atomic operations
- [ ] Idempotency
- [ ] Optimistic locking
- [ ] Pessimistic locking
- [ ] Saga
- [ ] Eventual consistency

## Infrastructure
- [ ] Redis
- [ ] API Gateway
- [ ] Docker production
- [ ] Kubernetes
- [ ] Kafka

## Reliability
- [ ] Timeout
- [ ] Retry
- [ ] Backoff
- [ ] Circuit breaker
- [ ] Bulkhead
- [ ] Rate limiting
- [ ] Backpressure

## Security
- [ ] JWT
- [ ] OAuth 2.0
- [ ] OpenID Connect
- [ ] Service authentication
- [ ] Authorization
- [ ] Secrets
- [ ] TLS

## Observability
- [ ] Structured logging
- [ ] Correlation IDs
- [ ] Prometheus
- [ ] Grafana
- [ ] OpenTelemetry
- [ ] Distributed tracing

## Deployment
- [ ] Docker Compose
- [ ] Kubernetes
- [ ] CI/CD
- [ ] Terraform
- [ ] AWS

## Advanced
- [ ] CQRS
- [ ] Event sourcing
- [ ] CAP theorem
- [ ] Quorum
- [ ] Consensus
- [ ] Service mesh
```

---

# Final Goal

By the end of this roadmap, you should be able to design and explain a system like:

```text
                         ┌─────────────┐
                         │ API Gateway │
                         └──────┬──────┘
                                │
          ┌─────────────────────┼─────────────────────┐
          ↓                     ↓                     ↓
     Identity               Event                  Order
     Service               Service                Service
          │                     │                     │
          ↓                     ↓                     ↓
     Identity DB             Event DB              Order DB
                                │                     │
                                ↓                     ↓
                           Inventory              Payment
                            Service               Service
                                │                     │
                                └─────────┬───────────┘
                                          ↓
                                      RabbitMQ
                                          │
                         ┌────────────────┼────────────────┐
                         ↓                ↓                ↓
                   Notification       Analytics          Audit
                         │
                         ↓
                       Redis
                  (temporary state)
```

And, more importantly, explain:

- why each service exists
- why the databases are separated
- when to use HTTP vs events
- how duplicate requests are handled
- how race conditions are prevented
- how seat reservations work
- how distributed transactions are handled
- how failures are recovered
- how messages are retried
- how consistency is maintained
- how services are authenticated
- how the system is observed
- how it is deployed and scaled

That is the actual objective of the roadmap—not simply being able to create multiple Node.js applications and call them "microservices."