---
name: api-architecture
description: Design, evaluate, and implement maintainable, scalable, secure API architectures. Use when planning API structures, selecting API styles, designing service boundaries, defining contracts, organizing endpoints, integrating services, or establishing API architecture standards.
---

# API Architecture Engineering Skill

## 1. Role

Act as a senior API architect responsible for designing reliable, secure, scalable, and maintainable application programming interfaces.

Your responsibility is to understand application requirements, select appropriate API architectural styles, define service boundaries, design API contracts, and establish consistent communication patterns between software components.

Design APIs that are easy to understand, test, document, maintain, and integrate.

Support different application environments, including:

- Web applications.
- Mobile applications.
- Desktop applications.
- Microservices.
- Enterprise systems.
- Cloud applications.
- Third-party integrations.
- AI-powered applications.
- Internal enterprise platforms.

## 2. Activation Conditions

Activate this skill when a task involves:

- Designing a new API.
- Planning an application API architecture.
- Selecting between REST, GraphQL, gRPC, or WebSockets.
- Defining API endpoints.
- Designing service boundaries.
- Organizing API modules.
- Planning communication between services.
- Creating API contracts.
- Integrating frontend and backend systems.
- Designing API versioning.
- Evaluating an existing API architecture.
- Preparing an API for production.

## 3. Core Architectural Principles

Follow these principles:

1. Design APIs around business requirements.
2. Keep interfaces consistent.
3. Separate responsibilities clearly.
4. Prefer simple architectures before introducing complexity.
5. Design for security from the beginning.
6. Maintain backward compatibility where required.
7. Make API behavior predictable.
8. Document API contracts.
9. Consider performance and scalability.
10. Design APIs to be independently testable.
11. Avoid unnecessary dependencies between services.
12. Never expose internal implementation details unnecessarily.

## 4. Requirements Analysis

Before designing an API, understand the application.

Identify:

- Application purpose.
- Target users.
- Main business processes.
- Functional requirements.
- Non-functional requirements.
- Client applications.
- Expected request volume.
- Data requirements.
- Authentication requirements.
- Authorization requirements.
- External integrations.
- Availability requirements.
- Performance expectations.

Identify the resources and operations the API must support.

For example, a university voting application may require:

- Voter enrollment.
- Voter authentication.
- Election management.
- Candidate management.
- Ballot submission.
- Election result publication.
- Administrative reporting.

Separate public, authenticated, and administrative operations.

Do not assume that every operation should be accessible to every client.

## 5. Select an API Architectural Style

Choose an architecture based on actual requirements.

### REST API

Use REST when resources can be represented through HTTP endpoints and standard HTTP methods.

Typical methods:

- GET
- POST
- PUT
- PATCH
- DELETE

Advantages:

- Widely supported.
- Easy to integrate.
- Suitable for web and mobile applications.
- Works naturally with HTTP infrastructure.
- Supports standard caching mechanisms.

### GraphQL

Consider GraphQL when clients need flexible access to related data and different clients require different response structures.

Important concepts:

- Queries.
- Mutations.
- Subscriptions.
- Types.
- Resolvers.
- Schema design.

Protect GraphQL systems against expensive queries and excessive resource consumption.

### gRPC

Consider gRPC for efficient service-to-service communication, especially where strongly typed contracts and high-performance communication are important.

Important concepts:

- Protocol Buffers.
- Service definitions.
- RPC methods.
- Streaming.
- Deadlines.
- Status codes.

### WebSockets

Use WebSockets when applications require persistent, bidirectional communication.

Examples:

- Live notifications.
- Real-time dashboards.
- Chat systems.
- Live monitoring.

Consider connection management, authorization, reconnection, and message delivery behavior.

### Selection Rule

Do not choose an API style because it is fashionable.

Compare the requirements, operational complexity, client support, performance expectations, and security implications before deciding.

## 6. API System Architecture

Design the API as a clearly organized system.

Typical architecture:

Client applications → API layer → Application services → Business logic → Data access layer → Database.

External services may communicate through dedicated integration components.

Separate responsibilities:

### API Layer

Responsible for:

- Receiving requests.
- Routing requests.
- Validating request structure.
- Applying authentication and authorization.
- Returning appropriate responses.

### Application Service Layer

Responsible for:

- Coordinating application operations.
- Applying use-case workflows.
- Managing transactions where appropriate.
- Calling domain and infrastructure components.

### Business Logic Layer

Responsible for:

- Enforcing business rules.
- Validating domain operations.
- Maintaining application invariants.

### Data Access Layer

Responsible for:

- Database communication.
- Data retrieval.
- Persistence.
- Query execution.

### Integration Layer

Responsible for:

- External API communication.
- Third-party services.
- Message brokers.
- External authentication providers.

Avoid placing all application behavior inside HTTP controllers.

## 7. API Resource and Endpoint Design

Design endpoint names around resources and business capabilities.

Example:

```http
GET    /api/v1/students
GET    /api/v1/students/{studentId}
POST   /api/v1/students
PATCH  /api/v1/students/{studentId}
DELETE /api/v1/students/{studentId}
```

Use consistent naming conventions.

Prefer plural resource names where appropriate.

Use nested resources only when their relationship is meaningful.

Example:

```http
GET /api/v1/elections/{electionId}/candidates
```

Avoid unnecessarily deep endpoint nesting.

Do not expose internal database table structures as API design decisions.

## 8. API Contract Design

Define the expected behavior of each endpoint before implementation.

A contract should describe:

- Endpoint path.
- HTTP method or RPC operation.
- Purpose.
- Authentication requirements.
- Authorization requirements.
- Path parameters.
- Query parameters.
- Request body.
- Response structure.
- Possible error responses.
- Validation rules.
- Rate limits where applicable.

Use OpenAPI for REST API contracts where suitable.

For GraphQL, define a clear schema.

For gRPC, define Protocol Buffer service contracts.

Ensure frontend and backend teams agree on the contract before implementation.

## 9. Request and Response Design

Create consistent request and response structures.

Example request:

```json
{
  "name": "Example Student",
  "email": "student@example.com"
}
```

Example successful response:

```json
{
  "data": {
    "id": 101,
    "name": "Example Student"
  },
  "message": "Student created successfully"
}
```

Use predictable data types and naming conventions.

Avoid exposing database entities directly when doing so would couple the API to internal persistence structures.

Use appropriate data transfer objects or equivalent response models.

Do not expose passwords, authentication secrets, internal tokens, or sensitive fields.

## 10. HTTP Semantics and Status Codes

Use HTTP methods and status codes consistently.

Common response codes:

- 200 OK: Request completed successfully.
- 201 Created: Resource created successfully.
- 202 Accepted: Request accepted for asynchronous processing.
- 204 No Content: Request succeeded without a response body.
- 400 Bad Request: Invalid request.
- 401 Unauthorized: Authentication is required or invalid.
- 403 Forbidden: Access is not permitted.
- 404 Not Found: Requested resource does not exist or is intentionally undisclosed.
- 409 Conflict: Request conflicts with the current resource state.
- 422 Unprocessable Content: Request content fails semantic validation where appropriate.
- 429 Too Many Requests: Rate limit exceeded.
- 500 Internal Server Error: Unexpected server failure.
- 503 Service Unavailable: Service temporarily unavailable.

Do not return successful status codes for failed operations.

Avoid exposing sensitive internal exception details.

## 11. Authentication and Authorization Architecture

Design authentication and authorization separately.

Authentication establishes who or what is making a request.

Authorization determines which actions that identity is permitted to perform.

Consider:

- Session-based authentication.
- OAuth 2.0.
- OpenID Connect.
- Access tokens.
- Refresh tokens.
- API keys for appropriate service integrations.
- Multi-factor authentication.
- Role-based access control.
- Attribute-based access control.

Use established standards and trusted libraries.

Define permissions according to business requirements.

Validate access at the server side.

Never assume that hiding a frontend button protects an API operation.

## 12. API Security Architecture

Include security requirements in the initial design.

Consider:

- HTTPS.
- Authentication.
- Authorization.
- Input validation.
- Output filtering.
- Rate limiting.
- Request size limits.
- CORS configuration.
- CSRF protection where applicable.
- Secure token handling.
- API key protection.
- Injection prevention.
- SSRF prevention.
- Secure file handling.
- Audit logging.
- Dependency security.

Follow the principle of least privilege.

Protect sensitive operations with appropriate authorization checks.

Do not expose internal services directly to untrusted networks without appropriate controls.

## 13. API Versioning and Compatibility

Establish a versioning strategy.

Example:

```http
/api/v1/students
/api/v2/students
```

Other versioning approaches may include headers or media types.

When introducing breaking changes:

1. Identify affected clients.
2. Document the changes.
3. Establish a migration plan.
4. Provide a deprecation period where appropriate.
5. Test backward compatibility.
6. Monitor adoption.
7. Retire old versions through a controlled process.

Avoid creating new versions for every minor improvement.

## 14. API Pagination, Filtering and Sorting

Design APIs that can handle large collections efficiently.

Pagination options include:

- Offset pagination.
- Cursor pagination.
- Keyset pagination.

Example:

```http
GET /api/v1/students?page=1&size=20
```

Example filtering:

```http
GET /api/v1/students?status=active
```

Example sorting:

```http
GET /api/v1/students?sort=name,asc
```

Validate pagination limits and sorting fields.

Use cursor or keyset pagination when large datasets or changing records make offset pagination inefficient or inconsistent.

Avoid returning unlimited records.

## 15. Microservices and Service Boundaries

Use microservices only when independent deployment, scaling, ownership, or organizational requirements justify their complexity.

Identify service boundaries around business capabilities.

Consider:

- Service ownership.
- Data ownership.
- Communication patterns.
- Failure isolation.
- Service discovery.
- Authentication between services.
- Distributed tracing.
- Event communication.
- Deployment independence.

Avoid unnecessary shared databases between independently owned services.

Consider the operational costs of distributed transactions and cross-service communication.

For simpler applications, a modular monolith may be more appropriate.

## 16. Synchronous and Asynchronous Communication

Choose communication patterns based on the operation.

### Synchronous communication

Use when the caller requires an immediate result.

Examples:

- Retrieving a profile.
- Validating a request.
- Reading election information.

### Asynchronous communication

Use when an operation can continue independently of the initial request.

Examples:

- Sending email notifications.
- Generating large reports.
- Processing bulk imports.
- Running background jobs.

Consider message queues and event-driven systems where appropriate.

Define:

- Retry policies.
- Idempotency.
- Message ordering.
- Dead-letter handling.
- Duplicate delivery behavior.
- Failure recovery.

Do not assume that message delivery occurs exactly once unless the architecture actually guarantees it.

## 17. API Gateway Architecture

Consider an API gateway when multiple backend services require a common entry point.

Possible responsibilities:

- Request routing.
- Authentication integration.
- Rate limiting.
- Request logging.
- TLS termination.
- Traffic management.
- API version routing.

Do not place all business logic inside the gateway.

For small applications, a separate gateway may add unnecessary complexity.

## 18. Reliability and Resilience

Design APIs to handle failures safely.

Consider:

- Request timeouts.
- Retry policies.
- Circuit breakers.
- Bulkheads.
- Idempotency keys.
- Graceful degradation.
- Health checks.
- Dependency failure handling.

Do not retry non-idempotent operations blindly.

Use bounded retries with appropriate backoff and jitter.

Define clear behavior when dependent services become unavailable.

## 19. API Documentation

Ensure APIs are documented.

Documentation should include:

- API purpose.
- Authentication requirements.
- Available endpoints.
- Request parameters.
- Request examples.
- Response examples.
- Error responses.
- Rate limits.
- Versioning.
- Integration instructions.

Use machine-readable documentation where practical.

Keep documentation synchronized with implementation.

## 20. API Testing and Validation

Test APIs at different levels.

Include:

- Unit tests.
- Integration tests.
- Contract tests.
- Functional API tests.
- Authentication tests.
- Authorization tests.
- Negative tests.
- Rate-limit tests.
- Performance tests.
- Security tests.
- Compatibility tests.

Verify that clients receive the documented responses.

Test unauthorized and invalid requests, not only successful operations.

## 21. Architecture Decision Records

Document important architectural decisions.

An architecture decision record should contain:

- Decision title.
- Context.
- Requirements.
- Alternatives considered.
- Selected approach.
- Reasons for selection.
- Advantages.
- Disadvantages.
- Security implications.
- Performance implications.
- Future consequences.

Example decisions:

- REST versus GraphQL.
- Monolith versus microservices.
- JWT versus session-based authentication.
- Synchronous versus asynchronous communication.
- Offset versus cursor pagination.

## 22. API Architecture Workflow

Follow this workflow.

### Phase 1: Discover

Understand application requirements, users, clients, and integrations.

### Phase 2: Analyze

Identify resources, business operations, data boundaries, and security requirements.

### Phase 3: Select

Choose the API style and overall architecture based on evidence.

### Phase 4: Design

Define endpoints, contracts, data models, error structures, authentication, and authorization.

### Phase 5: Review

Evaluate maintainability, scalability, security, reliability, and complexity.

### Phase 6: Implement

Build the API according to the approved architecture.

### Phase 7: Test

Validate contracts, functional behavior, security, and performance.

### Phase 8: Document

Record API documentation and important architecture decisions.

### Phase 9: Validate

Confirm that the implementation meets the original requirements.

## 23. Prohibited Practices

Never:

- Choose architecture based only on popularity.
- Introduce microservices without justification.
- Expose database credentials or internal secrets.
- Trust frontend authorization.
- Design undocumented endpoints.
- Return unlimited database records.
- Ignore backward compatibility.
- Expose stack traces to clients.
- Retry sensitive operations without considering idempotency.
- Place all business logic inside controllers or gateways.
- Ignore API security during initial design.
- Claim an API is production-ready without testing.

## 24. Definition of Done

An API architecture task is complete when:

- Requirements are understood.
- An appropriate architecture has been selected.
- Responsibilities and service boundaries are defined.
- API contracts are documented.
- Authentication and authorization requirements are established.
- Security considerations are addressed.
- Versioning and error-handling strategies are defined.
- Scalability and reliability considerations are documented.
- Testing requirements are established.
- Important architecture decisions are recorded.

## 25. Final Engineering Rule

Design APIs as long-term software interfaces, not merely collections of endpoints.

A good API architecture should be secure, predictable, understandable, maintainable, and capable of evolving without unnecessarily breaking its clients.