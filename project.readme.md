1. Web & Networking Fundamentals
HTTP
 HTTP request/response model
 HTTP methods
 HTTP status codes
 HTTP headers
 Cookies
 Sessions
 CORS
 Preflight requests
 Keep-Alive
 HTTP caching
 HTTP/1.1
 HTTP/2
 HTTP/3
 QUIC
 Idempotency
 Connection lifecycle
 TLS / HTTPS
Networking
 IP addresses
 IPv4
 IPv6
 Subnets
 Private vs public IP
 Ports
 TCP
 UDP
 TCP vs UDP
 DNS
 NAT
 PAT
 Routers
 Firewalls
 Latency
 Bandwidth
 Packet loss
 Jitter
2. WebSocket Fundamentals
 WebSocket protocol
 HTTP Upgrade handshake
 Persistent connections
 Full-duplex communication
 WebSocket frames
 Text frames
 Binary frames
 Ping/Pong
 Close handshake
 WebSocket close codes
 Connection lifecycle
 Heartbeats
 Connection timeout
 Reconnection
 Backoff
 Network failure handling
 Duplicate connections
 Graceful disconnect
 Graceful server shutdown
3. Socket.IO
 Socket.IO architecture
 Client
 Server
 Events
 Event listeners
 Broadcasting
 Rooms
 Namespaces
 Middleware
 Acknowledgements
 Error handling
 Connection recovery
 Volatile events
 Binary data
 Authentication
 Authorization
 Socket lifecycle
4. Event-Driven Architecture
 Events
 Commands
 Event producers
 Event consumers
 Event handlers
 Event ordering
 Event delivery
 Event duplication
 Idempotency
 At-most-once delivery
 At-least-once delivery
 Exactly-once semantics
 Event versioning
 Event schemas
 Event validation
 Event-driven architecture patterns
5. Real-Time Room Architecture
 Room creation
 Room joining
 Room leaving
 Room membership
 Participant presence
 Online/offline state
 Typing indicators
 Room permissions
 Room lifecycle
 Room cleanup
 Reconnection to room
 Duplicate room joins
 Room state synchronization
 Server-authoritative state
6. Redis
Core Redis
 Redis architecture
 Strings
 Hashes
 Lists
 Sets
 Sorted Sets
 TTL
 Expiration
 Atomic operations
 Transactions
 Pipelines
Advanced Redis
 Pub/Sub
 Redis Streams
 Consumer groups
 Distributed locks
 Rate limiting with Redis
 Distributed counters
 Cache invalidation
 Redis persistence
 Redis memory management
7. Scaling WebSockets
 Stateless WebSocket servers
 Horizontal scaling
 Load balancing
 Sticky sessions
 Redis adapter
 Redis Pub/Sub
 Cross-server broadcasting
 Shared room state
 Connection distribution
 Server failure
 Reconnection after server failure
 Graceful deployment
 Connection draining
 Backpressure
 Rate limiting

Architecture:

                Load Balancer
                /     |     \
               /      |      \
            WS-1    WS-2    WS-3
               \      |      /
                \     |     /
                   Redis

You should understand every component in that diagram.

8. WebRTC Fundamentals
 What WebRTC is
 WebRTC architecture
 Peer-to-peer communication
 RTCPeerConnection
 MediaStream
 MediaStreamTrack
 RTCRtpSender
 RTCRtpReceiver
 RTCDataChannel
 Browser media APIs
Media capture
 getUserMedia()
 Camera permissions
 Microphone permissions
 Device enumeration
 Camera selection
 Microphone selection
 Track enable/disable
 Track replacement
 Screen sharing
9. WebRTC Signaling
 Signaling concept
 SDP
 SDP Offer
 SDP Answer
 Offer/Answer model
 ICE candidates
 Candidate gathering
 Candidate exchange
 Signaling server
 Signaling state
 WebSocket-based signaling

Flow:

Client A
   │
   │ Offer
   ▼
Signaling Server
   │
   │ Offer
   ▼
Client B
   │
   │ Answer
   ▼
Signaling Server
   │
   ▼
Client A
10. WebRTC Networking
 NAT traversal
 STUN
 TURN
 ICE
 ICE candidates
 Host candidates
 Server-reflexive candidates
 Relay candidates
 ICE connectivity checks
 ICE restart
 Symmetric NAT
 Firewall restrictions
 Direct connection
 Relay connection
11. WebRTC Connection Management
 connectionState
 iceConnectionState
 signalingState
 Connection failure
 Reconnection
 ICE restart
 Network switching
 Device switching
 Track replacement
 Peer disconnection
 Cleanup
12. WebRTC Media
 RTP
 RTCP
 SRTP
 Audio codecs
 Video codecs
 VP8
 VP9
 H.264
 Opus
 Bitrate
 Resolution
 FPS
 Adaptive bitrate
 Bandwidth estimation
 Packet loss
 Jitter
 Latency
13. WebRTC Debugging & Performance
 getStats()
 RTT
 Jitter
 Packet loss
 Bitrate
 Frames dropped
 Frames received
 Connection statistics
 Chrome WebRTC internals
 Network throttling
 Poor-network testing
 Audio/video quality monitoring
14. Group Video Calling
 1-to-1 architecture
 Mesh architecture
 Mesh scaling problems
 SFU
 MCU
 Media server
 RTP forwarding
 Simulcast
 SVC
 Bandwidth optimization

Learn the architecture of:

 LiveKit
 mediasoup
 Janus

You don't need to build an SFU yourself.

15. Collaborative Code Editor
Basic synchronization
 Editor state
 Code updates
 Debouncing
 Throttling
 Broadcasting changes
 Initial state synchronization
 Conflict scenarios
Distributed editing
 Concurrent modifications
 Race conditions
 Operation ordering
 Operational Transformation
 CRDT
 Logical clocks
 Convergence
 Conflict resolution
 Yjs
16. Interview State Management
 Interview lifecycle
 Draft
 Scheduled
 Waiting
 Active
 Completed
 Cancelled
 Server-authoritative state
 State transitions
 State machine
 State validation
 Concurrent state changes
 Race conditions

Example:

CREATED
   ↓
WAITING
   ↓
ACTIVE
   ↓
COMPLETED
17. Real-Time Interview Timer
 Server-side timer
 Client-side display
 Server timestamps
 Clock synchronization
 Countdown calculation
 Timer persistence
 Timer pause
 Timer resume
 Timer expiration
 Client disconnect during timer
 Server restart during timer
18. Authentication
 Authentication
 Authorization
 Sessions
 JWT
 Access tokens
 Refresh tokens
 Token rotation
 Token expiration
 Secure cookies
 HttpOnly
 Secure
 SameSite
 CSRF
 XSS
19. Authorization
 Role-based access control
 Resource-level authorization
 Room-level authorization
 Event-level authorization
 Interviewer permissions
 Candidate permissions
 Admin permissions
 Server-side authorization

Example:

User
 ↓
Authenticated?
 ↓
Member of room?
 ↓
Role?
 ↓
Permission?
 ↓
Perform action
20. WebSocket Security
 Authentication during handshake
 Authorization per event
 Origin validation
 Input validation
 Schema validation
 Message size limits
 Rate limiting
 Connection limits
 Event abuse protection
 DoS protection
 Resource exhaustion
 Secure error handling
21. Code Execution System
 Job queue
 Worker architecture
 Producer
 Consumer
 Job state
 Job retries
 Exponential backoff
 Dead-letter queue
 Job timeout
 Worker concurrency
 Job idempotency

Architecture:

Candidate
   ↓
API
   ↓
Queue
   ↓
Worker
   ↓
Sandbox
   ↓
Execution
   ↓
Result
22. Secure Code Sandbox
 Linux processes
 Process isolation
 Linux namespaces
 cgroups
 CPU limits
 Memory limits
 Process limits
 Filesystem isolation
 Network isolation
 Execution timeout
 Container isolation
 Container security
 Resource quotas
 Sandbox threat model
23. Database
 Data modeling
 Users
 Interviews
 Participants
 Questions
 Submissions
 Results
 Interview sessions
 Audit logs
 Indexes
 Compound indexes
 Query optimization
 Transactions
 Pagination
 Data consistency
 Soft deletion
24. Message Queues
 Queue
 Producer
 Consumer
 Worker
 Job
 Retry
 Backoff
 Dead-letter queue
 Visibility timeout
 Job prioritization
 Concurrency
 Idempotency
 Failure recovery
 BullMQ
25. Testing
Unit testing
 Unit test fundamentals
 Arrange/Act/Assert
 Test doubles
 Mock
 Stub
 Spy
 Fake
 Dependency injection
 Isolation
 Boundary testing
 Error testing
 Edge cases
Integration testing
 Database integration tests
 Redis integration tests
 Queue integration tests
 Repository tests
 API integration tests
WebSocket testing
 Connection tests
 Authentication tests
 Room tests
 Broadcast tests
 Permission tests
 Reconnection tests
 Disconnect tests
 Concurrent client tests
E2E
 Playwright
 Browser automation
 Multi-user scenarios
 Interview flow
 Video-call flow
 Collaborative editing flow
26. Observability
Logging
 Structured logging
 Pino
 Log levels
 Request IDs
 Correlation IDs
 Socket IDs
 User IDs
 Room IDs
Metrics
 Prometheus
 Grafana
 Active connections
 Active rooms
 Messages/sec
 WebSocket errors
 WebRTC failures
 Code execution time
 Queue depth
 Worker utilization
 Database latency
Tracing
 OpenTelemetry
 Distributed tracing
 Trace IDs
 Spans
 Cross-service tracing
27. Deployment
 Linux
 Docker
 Docker Compose
 Multi-container architecture
 Nginx
 Reverse proxy
 WebSocket proxying
 TLS
 DNS
 Environment variables
 Secret management
 Health checks
 Readiness checks
 Liveness checks
 Graceful shutdown
28. Production Infrastructure
 Load balancer
 Horizontal scaling
 Auto scaling
 Connection draining
 Rolling deployment
 Zero-downtime deployment
 Database backups
 Redis persistence
 Disaster recovery
 Failure recovery
29. Distributed Systems
 CAP theorem
 Consistency
 Availability
 Partition tolerance
 Strong consistency
 Eventual consistency
 Race conditions
 Distributed locks
 Leader election
 Idempotency
 Retry strategies
 Backoff
 Timeouts
 Circuit breakers
 Bulkheads
 Backpressure
 Failure detection
 Clock synchronization
 Logical clocks
 Event ordering
30. System Design
 Requirements gathering
 Functional requirements
 Non-functional requirements
 Capacity estimation
 Traffic estimation
 Storage estimation
 API design
 WebSocket API design
 Database design
 Caching
 Queue architecture
 Scaling
 Failure scenarios
 Security
 Observability
 Cost analysis
Design these specifically
 1-to-1 video interview
 Group video interview
 Collaborative editor
 Real-time chat
 Online presence
 Interview scheduling
 Code execution platform
 WebSocket infrastructure
 WebRTC infrastructure
31. Advanced WebRTC

After everything above:

 Simulcast
 SVC
 Data channels
 Screen sharing
 Recording
 Media server
 SFU architecture
 MCU architecture
 RTP forwarding
 Media routing
 Bandwidth adaptation
 Network quality detection
 Active speaker detection
 Audio processing
 Echo cancellation
 Noise suppression
32. Advanced Real-Time Architecture

Eventually investigate:

 Event sourcing
 CQRS
 Event replay
 Event versioning
 Distributed event processing
 Kafka
 Redis Streams
 NATS
 Message ordering
 Partitioning
 Consumer groups
 Backpressure
 Stream processing

These are later topics, not prerequisites for your MVP.

33. Engineering Practices

Don't neglect the boring parts.

 Clean Architecture
 SOLID
 Dependency inversion
 Domain modeling
 Error handling
 Error taxonomy
 Input validation
 API versioning
 Configuration management
 Feature flags
 Database migrations
 Git
 Git branching
 Conventional commits
 CI/CD
 Code review
 Documentation
 Architecture Decision Records