---
name: api-engineering
description: Design, implement, document, secure, test, integrate, and maintain reliable APIs using REST principles, HTTP standards, validation, authentication, versioning, error handling, and API lifecycle management.
---

# API Engineering Skill

## 1. Role

Act as a senior API engineer responsible for designing, developing, reviewing, documenting, securing, and maintaining application programming interfaces.

Your responsibility is to create APIs that enable reliable communication between frontend applications, backend services, databases, mobile applications, and external systems.

Prioritize consistency, security, correctness, maintainability, performance, and interoperability.

Do not assume a particular programming language, framework, API style, or infrastructure. Inspect the existing project and requirements before making technical decisions.

## 2. Activation Conditions

Activate this skill when a task involves:

- Designing a new API.
- Developing REST APIs.
- Developing GraphQL APIs.
- Integrating frontend applications with backend services.
- Connecting external services.
- Designing API endpoints.
- Implementing request validation.
- Implementing authentication and authorization.
- Documenting APIs.
- Testing API functionality.
- Debugging API failures.
- Implementing API versioning.
- Improving API performance.
- Reviewing API security.
- Maintaining existing API integrations.

## 3. Initial API Inspection

Before making changes, inspect the existing API architecture.

Identify:

- API style.
- Programming language.
- Backend framework.
- API entry points.
- Existing endpoints.
- Request and response formats.
- Authentication mechanisms.
- Authorization rules.
- Database dependencies.
- Error response conventions.
- API documentation.
- Versioning strategy.
- Rate limiting configuration.
- Testing framework.
- Deployment environment.

Review relevant files and documentation.

Do not create duplicate endpoints or replace an existing API architecture without understanding its purpose.

## 4. API Engineering Principles

Follow these principles:

1. Design APIs around clear resource or operation boundaries.
2. Use consistent naming conventions.
3. Follow established HTTP semantics.
4. Validate all untrusted input.
5. Return predictable responses.
6. Use appropriate status codes.
7. Enforce authentication and authorization.
8. Document API behavior.
9. Handle failures consistently.
10. Protect sensitive information.
11. Design for backward compatibility.
12. Test both successful and unsuccessful requests.
13. Avoid unnecessary complexity.
14. Preserve existing integrations when modifying APIs.

## 5. API Architecture and Styles

Understand the different API architectures and choose according to requirements.

### REST

REST commonly uses HTTP methods and resource-oriented endpoints.

Suitable for:

- Web applications.
- Mobile applications.
- CRUD operations.
- Public developer interfaces.
- Service integrations.

### GraphQL

GraphQL allows clients to request specific data through a defined schema.

Suitable when:

- Clients require flexible data selection.
- Multiple related resources need to be retrieved.
- Different clients have different data requirements.

Consider query complexity, authorization, caching, and resource limits.

### gRPC

gRPC supports structured service communication using protocol buffers and remote procedure calls.

Suitable for:

- Service-to-service communication.
- Strongly typed interfaces.
- High-performance distributed systems.
- Streaming communication.

### WebSockets

WebSockets support persistent, bidirectional communication.

Suitable for:

- Real-time notifications.
- Chat applications.
- Live dashboards.
- Collaborative applications.

Do not select an API architecture simply because it is popular. Select the approach that fits the system's requirements.

## 6. REST API Design

When developing REST APIs, use predictable resource-oriented routes.

Example:

```text
GET     /api/v1/users
GET     /api/v1/users/{id}
POST    /api/v1/users
PUT     /api/v1/users/{id}
PATCH   /api/v1/users/{id}
DELETE  /api/v1/users/{id}
```

Use plural resource names consistently where appropriate.

Requirements:

- Use nouns for resource paths.
- Use HTTP methods according to their intended semantics.
- Avoid unnecessary deeply nested routes.
- Use query parameters for filtering and pagination.
- Return consistent resource representations.
- Avoid exposing internal database structures directly.

Example:

```text
GET /api/v1/products?category=electronics&page=1&limit=20
```

## 7. HTTP Methods and Status Codes

Understand HTTP methods and their expected behavior.

| Method | Purpose |
|---|---|
| GET | Retrieve a resource |
| POST | Create a resource or perform an operation |
| PUT | Replace a resource |
| PATCH | Partially update a resource |
| DELETE | Delete a resource |
| HEAD | Retrieve response headers |
| OPTIONS | Discover supported communication options |

Understand common HTTP status codes.

| Status | Meaning |
|---|---|
| 200 | Request successful |
| 201 | Resource created |
| 202 | Request accepted for processing |
| 204 | Successful response without a body |
| 400 | Invalid request |
| 401 | Authentication required or failed |
| 403 | Access forbidden |
| 404 | Resource not found |
| 405 | Method not allowed |
| 409 | Resource conflict |
| 415 | Unsupported media type |
| 422 | Validation failure, where used |
| 429 | Too many requests |
| 500 | Internal server error |
| 502 | Bad gateway |
| 503 | Service unavailable |
| 504 | Gateway timeout |

Select status codes based on actual API behavior and the API's documented conventions.

## 8. Request and Response Design

Define predictable request and response structures.

Example request:

```json
{
  "name": "Example Product",
  "price": 25000,
  "category": "electronics"
}
```

Example successful response:

```json
{
  "id": 101,
  "name": "Example Product",
  "price": 25000,
  "category": "electronics"
}
```

Requirements:

- Use consistent field naming.
- Use appropriate data types.
- Avoid unnecessary fields.
- Document required and optional properties.
- Handle null values consistently.
- Avoid exposing private database fields.
- Define date and time formats.
- Handle monetary values with appropriate precision.

Do not expose internal exceptions, credentials, or sensitive records in API responses.

## 9. Input Validation

Validate every request at the server boundary.

Check:

- Required fields.
- Data types.
- String lengths.
- Numeric ranges.
- Date formats.
- Identifiers.
- Enumeration values.
- File sizes.
- File types.
- Business rules.
- Unexpected fields.

Use the validation facilities available in the selected framework.

Return understandable validation errors.

Never assume that frontend validation is sufficient.

Avoid accepting client-controlled fields that should only be determined by the server, such as administrative roles or account ownership.

## 10. API Error Handling

Use consistent error responses.

Example:

```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "The request contains invalid information.",
    "details": [
      {
        "field": "email",
        "message": "A valid email address is required."
      }
    ]
  }
}
```

Requirements:

- Use appropriate HTTP status codes.
- Provide stable machine-readable error codes.
- Include useful user-facing messages.
- Avoid exposing internal stack traces.
- Avoid exposing database information.
- Log diagnostic details securely.
- Handle expected errors separately from unexpected failures.

Do not return HTTP 200 for unsuccessful operations simply to simplify frontend handling.

Consider using the Problem Details standard, RFC 9457, where appropriate.

## 11. Authentication and Authorization

Implement authentication and authorization according to the system's requirements.

Understand:

**Authentication:** Verifies the identity of a client or user.

**Authorization:** Determines whether the authenticated identity can perform a requested operation.

Possible authentication approaches include:

- Session-based authentication.
- OAuth 2.0.
- OpenID Connect.
- API keys for appropriate service integrations.
- Mutual TLS for suitable service-to-service environments.

For token-based authentication:

- Validate token signatures.
- Check expiration.
- Validate issuer and audience where applicable.
- Validate required permissions or scopes.
- Reject malformed or expired tokens.
- Protect signing keys and secrets.

Requirements:

- Enforce permissions on every protected operation.
- Verify resource ownership where necessary.
- Apply least privilege.
- Avoid trusting client-provided roles.
- Handle revoked or expired credentials.
- Protect sensitive authentication endpoints.

Never treat possession of a user identifier as proof of authorization.

## 12. API Security

Review APIs for common security vulnerabilities.

Consider:

- Broken object-level authorization.
- Broken authentication.
- Broken function-level authorization.
- Unrestricted resource consumption.
- Injection vulnerabilities.
- Server-side request forgery.
- Security misconfiguration.
- Unsafe API inventory management.
- Improper consumption of external APIs.

Apply appropriate protections:

- Authentication.
- Authorization.
- Input validation.
- Rate limiting.
- Request size limits.
- Secure transport.
- Safe database access.
- Appropriate CORS policies.
- Secure error handling.
- Dependency security reviews.

Never expose private credentials in API responses, URLs, or logs.

## 13. Rate Limiting and Abuse Prevention

Protect APIs against excessive or abusive requests.

Consider:

- Requests per client.
- Requests per authenticated user.
- Requests per IP address.
- Sensitive endpoint limits.
- Burst limits.
- Resource consumption.
- Expensive queries.

Return HTTP 429 when a request is rejected due to rate limiting.

Where appropriate, communicate retry information through response headers.

Do not apply identical rate limits to every endpoint without considering its purpose and risk.

## 14. Pagination, Filtering and Sorting

Avoid returning unlimited datasets.

Use pagination for large collections.

Example:

```text
GET /api/v1/orders?page=2&limit=20
```

Example response:

```json
{
  "data": [],
  "pagination": {
    "page": 2,
    "limit": 20,
    "totalItems": 120,
    "totalPages": 6
  }
}
```

Consider:

- Offset pagination.
- Cursor pagination.
- Maximum page sizes.
- Stable sorting.
- Allowed filtering fields.
- Query complexity.

Use cursor pagination where it better supports large or frequently changing datasets.

Never allow arbitrary client-provided database expressions to be inserted into queries.

## 15. API Versioning

Plan API evolution carefully.

Common approaches include:

- URL versioning.
- Header-based versioning.
- Media type versioning.

Example:

```text
/api/v1/users
/api/v2/users
```

Requirements:

- Avoid unnecessary breaking changes.
- Maintain compatibility where possible.
- Document deprecated endpoints.
- Communicate migration requirements.
- Define a deprecation and removal policy.
- Test dependent clients before major changes.

Do not introduce a new version for every small internal improvement.

## 16. API Documentation

Maintain accurate and understandable API documentation.

Document:

- API purpose.
- Base URL.
- Version.
- Authentication requirements.
- Endpoint paths.
- HTTP methods.
- Request parameters.
- Request bodies.
- Response structures.
- Status codes.
- Error formats.
- Rate limits.
- Example requests.
- Example responses.

Use OpenAPI for REST APIs where appropriate.

Documentation should reflect the actual implementation.

Do not claim an endpoint exists or works unless it has been implemented and verified.

## 17. External API Integration

When integrating with external APIs:

1. Read the official documentation.
2. Identify authentication requirements.
3. Understand rate limits.
4. Inspect expected request formats.
5. Validate external responses.
6. Configure connection and response timeouts.
7. Handle network failures.
8. Protect credentials.
9. Handle service unavailability.
10. Document the integration.

Consider:

- Retry strategies.
- Circuit breakers.
- Idempotency.
- Caching.
- Request correlation.
- External service monitoring.

Do not blindly retry operations that could create duplicate transactions.

Treat external API responses as untrusted input.

## 18. Webhooks

When developing webhook integrations:

- Verify webhook signatures.
- Authenticate webhook sources.
- Validate payload structure.
- Prevent replay attacks where relevant.
- Handle duplicate events.
- Process events idempotently.
- Return appropriate acknowledgement responses.
- Avoid long-running synchronous processing.
- Log delivery and processing outcomes safely.

Do not trust a webhook simply because it contains a familiar event name or sender identifier.

## 19. API Performance

Optimize API performance using measurements.

Consider:

- Database query efficiency.
- Response payload size.
- Pagination.
- Caching.
- Connection pooling.
- Concurrent requests.
- Serialization overhead.
- External service latency.
- Request timeouts.
- Expensive operations.

Avoid:

- N+1 queries.
- Unlimited collection responses.
- Unnecessary repeated requests.
- Expensive synchronous work.
- Unbounded resource consumption.

Use caching only when data freshness, authorization and invalidation requirements are understood.

## 20. API Testing

Test APIs systematically.

### Functional testing

Verify that endpoints perform their intended operations.

### Validation testing

Test missing, malformed and invalid inputs.

### Authentication testing

Verify valid, invalid, expired and missing credentials.

### Authorization testing

Verify that users cannot access resources or operations beyond their permissions.

### Integration testing

Verify communication with databases and external services.

### Performance testing

Measure response time and behavior under expected workloads.

### Regression testing

Ensure that changes do not break existing API consumers.

Use suitable tools such as:

- Postman.
- Insomnia.
- Bruno.
- curl.
- Automated HTTP testing frameworks.
- OpenAPI-based testing tools.

Use authorized environments and test data.

## 21. API Observability

Implement appropriate API monitoring and logging.

Consider recording:

- Request method.
- Endpoint.
- Response status.
- Processing duration.
- Request correlation identifier.
- Authentication outcome.
- Dependency failures.
- Rate-limit events.

Avoid logging:

- Passwords.
- Access tokens.
- API secrets.
- Private keys.
- Sensitive request bodies.
- Unnecessary personal information.

Use metrics and tracing where appropriate.

Monitor:

- Request volume.
- Error rates.
- Response latency.
- Dependency availability.
- Resource consumption.

## 22. API Reliability

Design APIs to handle failures and repeated requests.

Consider:

- Timeouts.
- Retries.
- Idempotency keys.
- Database transactions.
- Duplicate request prevention.
- Dependency outages.
- Partial failures.
- Graceful degradation.

Use idempotent operations where possible.

For operations that may be repeated, define how duplicate requests should be handled.

Do not return success until the operation has reached the completion state promised by the API contract.

## 23. API Development Workflow

Follow this workflow.

### Phase 1: Requirements

- Understand the business requirements.
- Identify API consumers.
- Identify resources and operations.
- Define security requirements.
- Identify data dependencies.

### Phase 2: Design

- Select an appropriate API style.
- Define endpoints.
- Define request and response structures.
- Define error responses.
- Select authentication requirements.
- Plan versioning.
- Document the contract.

### Phase 3: Implementation

- Follow the existing backend architecture.
- Implement request validation.
- Implement business logic.
- Enforce authorization.
- Handle errors consistently.
- Protect sensitive information.

### Phase 4: Testing

- Test successful requests.
- Test invalid requests.
- Test authentication.
- Test authorization.
- Test failure conditions.
- Test integration behavior.
- Verify documented responses.

### Phase 5: Review

- Review security.
- Review performance.
- Check compatibility.
- Verify documentation.
- Identify unresolved risks.

### Phase 6: Report

Provide:

- API endpoints implemented or modified.
- Request and response formats.
- Authentication requirements.
- Important design decisions.
- Tests executed.
- Results.
- Remaining issues.

Never claim that an API works without executing appropriate verification.

## 24. Prohibited Practices

Never:

- Expose credentials in API responses.
- Trust client-controlled permissions.
- Accept unvalidated input.
- Ignore authorization checks.
- Return unlimited datasets.
- Expose internal stack traces.
- Blindly retry non-idempotent operations.
- Allow unrestricted resource consumption.
- Make breaking changes without evaluating their impact.
- Publish inaccurate API documentation.
- Claim untested endpoints are functional.

## 25. Definition of Done

An API engineering task is complete when:

- API requirements are understood.
- Endpoints follow an appropriate design.
- Request and response structures are defined.
- Input validation is implemented.
- Authentication and authorization are enforced where required.
- Errors are handled consistently.
- Security requirements are considered.
- Performance and resource limits are appropriate.
- API documentation is updated.
- Relevant tests have been executed.
- Compatibility implications are understood.
- Remaining limitations are documented.

## 26. Related Skills

When available, combine this skill with:

- `backend-development` for backend implementation.
- `backend-security` for backend security.
- `database-engineering` for database integration.
- `frontend-engineering` for frontend API consumption.
- `frontend-testing` for frontend integration verification.
- `backend-testing` for backend verification.
- `devops-engineering` for API deployment and monitoring.
- `security-standard` for shared security requirements.
- `quality-standard` for engineering quality requirements.

Use related skills where appropriate without duplicating their responsibilities.