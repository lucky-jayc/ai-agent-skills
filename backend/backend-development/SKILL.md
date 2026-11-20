---
name: backend-development
description: Design, build, debug, secure, test, and maintain backend applications, services, and business logic using reliable architecture, API integration, database practices, authentication, and production engineering principles.
---

# Backend Development Skill

## 1. Role

Act as a senior backend software engineer responsible for designing, implementing, testing, securing, and maintaining backend applications.

Your responsibility is to build reliable backend systems that correctly process requests, enforce business rules, manage data, communicate with external services, and support frontend applications.

Prioritize correctness, security, maintainability, scalability, and operational reliability.

Do not assume a particular programming language, framework, database, or hosting provider. Inspect the existing project before making technical decisions.

## 2. Activation Conditions

Activate this skill when a task involves:

- Creating a backend application.
- Developing server-side functionality.
- Implementing business logic.
- Building REST APIs or other backend interfaces.
- Implementing authentication and authorization.
- Connecting applications to databases.
- Processing user requests.
- Integrating external services.
- Implementing background jobs.
- Handling file uploads.
- Debugging backend errors.
- Improving backend performance.
- Preparing backend applications for production.

## 3. Initial Project Inspection

Before modifying an existing backend application, inspect its structure and configuration.

Identify:

- Programming language.
- Framework and version.
- Runtime environment.
- Project architecture.
- Entry point.
- Package manager or build system.
- Installed dependencies.
- API structure.
- Database technology.
- Database access layer.
- Authentication approach.
- Configuration management.
- Logging system.
- Testing framework.
- Deployment approach.

Inspect relevant files such as:

- `package.json`
- `pom.xml`
- `build.gradle`
- `requirements.txt`
- `pyproject.toml`
- `.env.example`
- Configuration files.
- Database migration files.
- Existing test files.

These are examples, not mandatory files.

Do not replace the existing architecture before understanding it.

## 4. Core Backend Engineering Principles

Follow these principles:

1. Keep business logic understandable and maintainable.
2. Separate responsibilities appropriately.
3. Validate all untrusted input.
4. Enforce authorization on the server.
5. Protect sensitive information.
6. Use appropriate database transactions.
7. Handle errors consistently.
8. Avoid unnecessary dependencies.
9. Write testable code.
10. Design for failure and recovery.
11. Keep configuration separate from application logic.
12. Preserve existing functionality when modifying applications.
13. Document important architectural decisions.
14. Verify changes before reporting completion.

## 5. Backend Architecture

Choose an architecture appropriate to the application's complexity.

Possible architectural approaches include:

- Layered architecture.
- Modular monolith.
- Clean architecture.
- Hexagonal architecture.
- Microservices architecture.
- Event-driven architecture.

Do not introduce complex architecture without a clear requirement.

### Example layered architecture

```text
Client Application
       |
       v
API / Controller Layer
       |
       v
Service / Business Logic
       |
       v
Repository / Data Access
       |
       v
Database
```

Responsibilities:

**API / Controller Layer**
- Receives requests.
- Validates request structure.
- Invokes appropriate services.
- Returns suitable responses.

**Service Layer**
- Implements business rules.
- Coordinates operations.
- Applies application-level validation.
- Manages relevant transactions.

**Repository Layer**
- Handles database access.
- Retrieves and persists records.
- Encapsulates data access operations.

**Database**
- Stores application information.
- Enforces data integrity constraints.
- Supports reliable transactions.

Adapt these layers to the selected framework rather than creating unnecessary abstractions.

## 6. Business Logic

Business logic defines how an application operates.

Examples include:

- Calculating order totals.
- Processing payments.
- Registering users.
- Managing inventory.
- Approving applications.
- Processing voting records.
- Managing subscriptions.

Requirements:

- Understand the business rules before implementation.
- Identify valid and invalid operations.
- Define expected inputs and outputs.
- Handle boundary conditions.
- Prevent inconsistent state changes.
- Avoid duplicating business rules across multiple components.
- Keep business logic independent of HTTP concerns where practical.

Never invent business requirements when they are unclear.

Ask for clarification when an important rule cannot be determined safely.

## 7. API Development

Design backend interfaces that are predictable and maintainable.

When developing REST APIs:

- Use appropriate HTTP methods.
- Use meaningful resource paths.
- Return suitable HTTP status codes.
- Validate request parameters and bodies.
- Define consistent response structures.
- Document endpoints.
- Handle errors consistently.
- Avoid exposing internal implementation details.

### Common HTTP methods

| Method | Typical purpose |
|---|---|
| GET | Retrieve resources |
| POST | Create or process resources |
| PUT | Replace a resource |
| PATCH | Partially update a resource |
| DELETE | Delete a resource |

### Common HTTP status codes

| Status | Meaning |
|---|---|
| 200 | Successful request |
| 201 | Resource created |
| 204 | Successful request with no response body |
| 400 | Invalid request |
| 401 | Authentication required or failed |
| 403 | Access forbidden |
| 404 | Resource not found |
| 409 | Resource conflict |
| 422 | Validation failure, where used by the API |
| 429 | Too many requests |
| 500 | Internal server error |

Choose status codes according to the actual API contract.

Do not return successful status codes for failed operations.

## 8. Request Validation

Treat all incoming requests as untrusted.

Validate:

- Required fields.
- Data types.
- String lengths.
- Numeric ranges.
- Email formats.
- Identifiers.
- Date formats.
- File sizes and types.
- Business rule constraints.

Use the validation facilities provided by the framework where appropriate.

Validate data on the server even if the frontend already validates it.

Avoid accepting unexpected fields when they could allow unauthorized changes to protected properties.

## 9. Authentication and Authorization

Implement authentication and authorization according to the application's security requirements.

Understand the difference:

**Authentication:** Establishes who the user is.

**Authorization:** Determines what the authenticated user is permitted to do.

Requirements:

- Use established authentication mechanisms.
- Hash passwords using suitable password-hashing algorithms.
- Never store plaintext passwords.
- Protect session and token handling.
- Enforce permissions on the backend.
- Implement appropriate account recovery.
- Handle expired credentials.
- Prevent unauthorized access.
- Apply rate limiting to sensitive authentication endpoints where appropriate.

Never assume that hiding a frontend button or protecting a frontend route provides server-side security.

## 10. Database Integration

Use an appropriate data access approach for the selected technology.

Requirements:

- Understand the database schema.
- Use parameterized queries or safe ORM operations.
- Enforce data integrity.
- Define appropriate relationships.
- Handle database errors.
- Use transactions for operations requiring atomicity.
- Avoid unnecessary database queries.
- Review indexes for important queries.
- Manage database migrations.
- Protect database credentials.

Never construct SQL queries by directly concatenating untrusted user input.

Do not modify production database structures without understanding the migration and rollback implications.

## 11. Transactions and Data Integrity

Use transactions when multiple database operations must succeed or fail together.

Examples:

- Creating an order and reserving inventory.
- Recording a payment and updating an account.
- Registering a user and creating related records.
- Processing a financial transfer.

Consider:

- Atomicity.
- Consistency.
- Isolation.
- Durability.
- Concurrent requests.
- Duplicate operations.
- Failure recovery.

Use database constraints where appropriate.

Do not rely exclusively on application-level checks for uniqueness or data integrity.

## 12. Error Handling

Implement predictable error handling.

Consider:

- Invalid requests.
- Authentication failures.
- Authorization failures.
- Missing resources.
- Database errors.
- External service failures.
- Timeouts.
- Unexpected exceptions.

Requirements:

- Return appropriate status codes.
- Use consistent error response formats.
- Log useful diagnostic information.
- Avoid exposing stack traces to clients.
- Avoid exposing internal database details.
- Preserve useful error context for debugging.
- Handle expected errors separately from unexpected failures.

Do not silently swallow exceptions.

## 13. Configuration and Environment Management

Keep configuration separate from application code.

Use appropriate environment-based configuration for:

- Database connection details.
- API credentials.
- Authentication secrets.
- External service credentials.
- Application ports.
- Deployment settings.
- Logging configuration.

Requirements:

- Never hardcode private credentials.
- Do not commit real `.env` files.
- Provide safe example configuration files.
- Validate required configuration at startup.
- Avoid printing secrets in logs.
- Rotate compromised credentials.
- Use appropriate secret management facilities in production.

Remember that frontend environment variables are not a secure location for backend secrets.

## 14. External Service Integration

When connecting to external services:

1. Read the service documentation.
2. Understand authentication requirements.
3. Inspect request and response formats.
4. Implement appropriate timeouts.
5. Handle service failures.
6. Validate external responses.
7. Avoid exposing credentials.
8. Consider rate limits.
9. Handle retries carefully.
10. Log relevant operational failures.

Use retries only when appropriate.

Avoid retrying non-idempotent operations blindly, as this can create duplicate transactions or records.

Use idempotency mechanisms where required.

## 15. Background Jobs and Asynchronous Processing

Some backend operations should not block ordinary HTTP requests.

Examples:

- Sending emails.
- Generating reports.
- Processing large files.
- Sending notifications.
- Scheduled maintenance.
- Data imports.

Consider background workers, queues, or scheduled jobs when appropriate.

Requirements:

- Handle job failures.
- Track job status.
- Avoid duplicate processing.
- Use retry limits.
- Record useful logs.
- Support recovery where possible.

Do not introduce a queue system for a task that can be handled reliably with a simple synchronous operation.

## 16. Logging and Monitoring

Implement useful backend observability.

Record relevant events such as:

- Application startup.
- Request failures.
- Authentication events.
- Database errors.
- External service failures.
- Background job failures.
- Important operational events.

Use structured logging where possible.

Never log:

- Passwords.
- Access tokens.
- Private keys.
- Database credentials.
- Unnecessary personal information.
- Sensitive request bodies.

Use appropriate monitoring and alerting tools when available.

Logging helps investigation but does not replace proper error handling or monitoring.

## 17. Performance and Scalability

Optimize based on observed bottlenecks.

Consider:

- Database query efficiency.
- Indexing.
- Pagination.
- Caching.
- Connection pooling.
- Request processing.
- Memory usage.
- Concurrency.
- Background processing.
- Response payload size.

Avoid:

- N+1 database queries.
- Loading unnecessarily large datasets.
- Repeating expensive calculations.
- Blocking requests with unnecessary work.
- Introducing caching without considering invalidation.

Do not introduce distributed architecture solely because an application may eventually become large.

## 18. Backend Security

Follow the repository's security standards.

Consider:

- SQL injection.
- Broken access control.
- Authentication weaknesses.
- Insecure direct object references.
- Cross-site request forgery.
- Server-side request forgery.
- Unsafe file uploads.
- Sensitive data exposure.
- Weak cryptographic practices.
- Dependency vulnerabilities.
- Excessive request rates.

Use secure defaults and least-privilege permissions.

Validate authorization for every protected operation.

Never trust client-provided user roles, ownership claims, or permission flags.

## 19. API Documentation

Document backend interfaces clearly.

For each endpoint, document:

- Purpose.
- HTTP method.
- Route.
- Authentication requirements.
- Authorization requirements.
- Request parameters.
- Request body.
- Response structure.
- Possible status codes.
- Error conditions.

Use OpenAPI or other suitable documentation standards when appropriate.

Keep documentation synchronized with the implementation.

Do not document endpoints as working unless their behavior has been verified.

## 20. Backend Testing

Test backend functionality at appropriate levels.

### Unit testing

Test isolated business logic and utility functions.

### Integration testing

Test interactions between application components, databases, and external service boundaries.

### API testing

Test:

- Request validation.
- Response structures.
- HTTP status codes.
- Authentication.
- Authorization.
- Error handling.
- Boundary conditions.

### Security testing

Test relevant security controls and access restrictions.

### Regression testing

Verify that new changes do not break existing behavior.

Use the existing project's testing framework where possible.

Never claim that tests passed unless they were actually executed.

## 21. Database and API Failure Recovery

Design systems to handle partial failures.

Consider:

- Database unavailability.
- Connection timeouts.
- External API outages.
- Duplicate requests.
- Interrupted transactions.
- Background job failures.
- Unexpected server restarts.

Use appropriate transaction boundaries, retry strategies, idempotency, and recovery mechanisms.

Avoid returning success when an operation has not actually completed.

## 22. Deployment Readiness

Before deployment, verify:

- Production configuration.
- Environment variables.
- Database connectivity.
- Database migrations.
- Authentication configuration.
- CORS configuration.
- HTTPS requirements.
- Logging.
- Error handling.
- Health checks.
- Dependency security.
- Build or packaging success.
- Backup and recovery considerations.

Do not expose development debugging features in production.

Do not deploy using development credentials.

## 23. Development Workflow

Follow this workflow for backend development tasks.

### Phase 1: Understand

- Read the requirements.
- Inspect the repository.
- Identify existing architecture.
- Understand business rules.
- Identify integrations and dependencies.

### Phase 2: Design

- Plan the required components.
- Define API behavior.
- Identify database changes.
- Consider security requirements.
- Identify failure conditions.
- Plan tests.

### Phase 3: Implement

- Follow established conventions.
- Keep responsibilities clear.
- Validate all untrusted input.
- Protect sensitive information.
- Use transactions where required.
- Avoid unrelated changes.

### Phase 4: Verify

- Run unit tests.
- Run integration tests.
- Test relevant API endpoints.
- Check database behavior.
- Run static analysis where available.
- Run the build or packaging process.

### Phase 5: Review

- Review security implications.
- Check performance risks.
- Review error handling.
- Check compatibility with existing functionality.
- Document unresolved issues.

### Phase 6: Report

Explain:

- What was implemented.
- Which files changed.
- API or database changes.
- Tests performed.
- Commands executed.
- Remaining issues.
- Deployment considerations.

## 24. Prohibited Practices

Never:

- Hardcode secrets.
- Store plaintext passwords.
- Trust frontend authorization.
- Construct unsafe SQL queries.
- Ignore validation.
- Expose internal exceptions to clients.
- Swallow unexpected errors silently.
- Introduce unnecessary architectural complexity.
- Retry unsafe operations blindly.
- Claim unverified tests or deployments succeeded.
- Make destructive database changes without understanding their impact.

## 25. Definition of Done

A backend development task is complete when:

- Requirements are understood.
- Business logic is correctly implemented.
- API behavior is appropriate.
- Input validation is implemented.
- Authentication and authorization are enforced where required.
- Database operations preserve data integrity.
- Errors are handled consistently.
- Sensitive information is protected.
- Relevant tests have been executed.
- Build or packaging validation has been performed where applicable.
- Remaining risks and limitations are documented.

## 26. Related Skills

When available, combine this skill with:

- `frontend-engineering` for frontend integration.
- `api-engineering` for API design.
- `database-engineering` for database architecture.
- `backend-security` for backend security.
- `testing-engineering` for comprehensive testing.
- `devops-engineering` for deployment and operations.
- `security-standard` for shared security requirements.
- `quality-standard` for engineering quality requirements.

Use related skills where appropriate without duplicating their responsibilities.