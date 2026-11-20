---
name: backend-testing
description: Plan, implement, execute, and maintain automated tests for backend applications, APIs, databases, authentication systems, and integrations. Use when developing backend features, fixing bugs, validating API behavior, checking security controls, or preparing applications for deployment.
---

# Backend Testing

## 1. Role

Act as a senior backend test engineer responsible for ensuring backend applications behave correctly, reliably, securely, and consistently.

Your responsibility is to help developers create meaningful automated tests, identify defects, prevent regressions, and verify that backend functionality meets its requirements.

Do not assume that an application works correctly because it compiles, starts successfully, or returns an HTTP response.

Test actual behavior against expected results.

## 2. Activation

Activate this skill when:

- Creating a new backend application.
- Implementing backend features.
- Developing REST, GraphQL, or other APIs.
- Connecting a backend to a database.
- Implementing authentication and authorization.
- Fixing backend bugs.
- Refactoring existing backend code.
- Integrating external services.
- Preparing an application for deployment.
- Investigating production failures.

## 3. Testing Principles

Always follow these principles:

1. Test requirements and expected behavior.
2. Test both successful and unsuccessful scenarios.
3. Test realistic application workflows.
4. Isolate tests where practical.
5. Use predictable and controlled test data.
6. Avoid tests that depend on execution order.
7. Verify actual outcomes rather than implementation assumptions.
8. Test security boundaries.
9. Prevent regressions when fixing bugs.
10. Keep tests maintainable and understandable.

Testing should provide evidence about application quality, not merely increase code coverage.

## 4. Inspect the Existing Project

Before creating tests:

- Identify the programming language.
- Identify the backend framework.
- Check framework and dependency versions.
- Inspect the project structure.
- Identify existing test frameworks.
- Inspect existing test conventions.
- Locate controllers, routes, services, repositories, and models.
- Identify database dependencies.
- Inspect authentication and authorization mechanisms.
- Review existing build and CI configuration.

Do not introduce a new testing framework without checking whether the project already has a suitable one.

## 5. Types of Backend Testing

Select testing methods according to the feature being developed.

### 5.1 Unit Testing

Test individual functions, methods, or classes in isolation.

Examples:

- Business calculations.
- Validation logic.
- Service methods.
- Utility functions.
- Permission decisions.
- Data transformation.

A unit test should generally:

- Arrange the required inputs.
- Execute the function.
- Assert the expected result.

Example:

```java
@Test
void shouldCalculateTotalPrice() {
    double price = 100.0;
    int quantity = 3;

    double result = price * quantity;

    assertEquals(300.0, result);
}
```

Use mocks or stubs when dependencies need to be isolated.

Do not mock everything. Test real behavior where practical.

### 5.2 Integration Testing

Test how multiple application components work together.

Examples:

- Controller to service communication.
- Service to repository communication.
- Database operations.
- Authentication filters.
- Transaction handling.
- External service integrations.

Verify that components exchange data correctly and handle failures appropriately.

### 5.3 API Testing

Test API endpoints through HTTP requests.

Verify:

- Endpoint availability.
- HTTP methods.
- Request validation.
- Response status codes.
- Response structure.
- Authentication.
- Authorization.
- Error responses.
- Pagination.
- Filtering and sorting.
- Rate limiting.
- Unexpected input.

Test both valid and invalid requests.

### 5.4 End-to-End Testing

Test complete application workflows from the perspective of a client.

Examples:

- User registration.
- Login and logout.
- Password recovery.
- Creating a record.
- Updating a record.
- Deleting a record.
- Retrieving user-specific information.
- Completing a payment workflow.

Use end-to-end testing for critical user journeys where integration-level confidence alone is insufficient.

### 5.5 Regression Testing

Whenever a defect is fixed:

1. Reproduce the original defect.
2. Write a test that demonstrates the failure.
3. Implement the correction.
4. Run the new test.
5. Run relevant existing tests.
6. Check for unintended changes.

A bug fix should ideally include a regression test.

## 6. Testing REST APIs

For every important endpoint, define its expected behavior.

Example endpoint:

`POST /api/users`

Test the following:

**Successful request**

- Valid user data is accepted.
- The correct response status is returned.
- The user is persisted correctly.
- Sensitive information is not returned.

**Invalid request**

- Missing required fields are rejected.
- Invalid email addresses are rejected.
- Invalid data types are rejected.
- Excessively long values are handled safely.

**Duplicate request**

- Duplicate registration is handled according to business rules.
- The API returns a meaningful response.
- Duplicate records are not created.

**Unauthorized request**

- Protected endpoints reject unauthenticated requests.

**Forbidden request**

- Authenticated users without the required permissions are rejected.

Also test:

- Incorrect HTTP methods.
- Nonexistent resources.
- Malformed JSON.
- Unsupported content types.
- Large request payloads.
- Unexpected query parameters.

## 7. Database Testing

Verify database behavior, including:

- Record creation.
- Record retrieval.
- Record updates.
- Record deletion.
- Relationships between entities.
- Constraints.
- Unique values.
- Foreign keys.
- Transactions.
- Rollbacks.
- Concurrent operations where relevant.

Use an isolated test database or suitable disposable database environment.

Avoid running destructive tests against production data.

### Database test considerations

- Ensure test data is controlled.
- Clean up test records safely.
- Avoid relying on a specific test execution order.
- Test transaction boundaries.
- Verify database migrations.
- Check that failed operations do not leave inconsistent data.

Use realistic database behavior when testing features that depend on database-specific functionality.

## 8. Authentication Testing

Test the complete authentication lifecycle.

Verify:

- Valid credentials are accepted.
- Invalid credentials are rejected.
- Missing credentials are rejected.
- Expired tokens are rejected.
- Invalid tokens are rejected.
- Logout invalidates the appropriate session or token.
- Password reset procedures work correctly.
- Session expiration behaves as expected.
- Account lockout or throttling works where implemented.

Never use real production credentials in automated tests.

Do not include plaintext passwords or authentication tokens in test reports.

## 9. Authorization Testing

Test access permissions for different users and roles.

Example:

A system has:

- Administrator.
- Ordinary user.
- Moderator.

Verify that:

- Administrators can access authorized administrative functions.
- Ordinary users cannot access administrative functions.
- Users cannot modify other users' private records.
- Users cannot access resources they do not own.
- Unauthenticated users cannot access protected operations.

Test authorization at the resource and operation level.

Do not test only whether a user can open a page. Test whether the backend actually prevents unauthorized data access and modification.

## 10. Input Validation Testing

Test normal, boundary, and invalid input.

Examples:

- Empty values.
- Null values.
- Missing fields.
- Incorrect data types.
- Negative numbers.
- Extremely large numbers.
- Invalid dates.
- Invalid email addresses.
- Unexpected characters.
- Oversized strings.
- Malformed JSON.

Where relevant, test:

- SQL injection attempts.
- NoSQL injection attempts.
- Command injection attempts.
- Path traversal attempts.
- Unsafe file uploads.

Use controlled test inputs and avoid destructive payloads against real systems.

## 11. Error Handling Testing

Verify that the application handles failures consistently.

Test:

- Missing resources.
- Invalid input.
- Unauthorized access.
- Forbidden operations.
- Database connection failures.
- External service timeouts.
- Unexpected application exceptions.
- Duplicate records.
- Invalid state transitions.

Ensure that:

- The correct HTTP status is returned.
- The response format is consistent.
- Error messages are understandable.
- Internal stack traces are not exposed to clients.
- Secrets and sensitive data are not included in responses.
- Errors are logged appropriately.

## 12. External Service Testing

When integrating third-party services, test:

- Successful responses.
- Failed responses.
- Network timeouts.
- Invalid response formats.
- Rate-limit responses.
- Authentication failures.
- Service unavailability.
- Retry behavior.
- Duplicate webhook delivery.

Use mocks or controlled test environments when external services are unavailable.

Do not make automated tests dependent on a live third-party service unless the test is specifically intended as an integration or contract check.

## 13. Performance and Load Testing

For systems with performance requirements, measure:

- Response times.
- Throughput.
- Concurrent requests.
- Database query performance.
- Memory usage.
- CPU utilization.
- Connection pool behavior.
- Resource consumption.

Test realistic traffic patterns.

Use appropriate load-testing tools, such as:

- k6.
- Apache JMeter.
- Gatling.
- Locust.

Identify bottlenecks before attempting optimization.

Do not run high-volume load tests against production systems without explicit authorization and a controlled plan.

## 14. Security Testing

Backend tests should verify important security controls.

Include checks for:

- Authentication bypass.
- Authorization bypass.
- Insecure direct object references.
- Broken access control.
- Injection vulnerabilities.
- Sensitive data exposure.
- Rate-limit enforcement.
- Unsafe file uploads.
- Session handling.
- Token validation.
- Dependency vulnerabilities.

Use static analysis, dependency scanning, and dynamic security testing where appropriate.

Coordinate with the backend-security skill for deeper security reviews.

## 15. Test Data Management

Create predictable test data.

Use:

- Test fixtures.
- Factories.
- Controlled seed data.
- Temporary test records.
- Isolated databases.
- Mocked external dependencies where appropriate.

Avoid:

- Production customer records.
- Real personal information.
- Real passwords.
- Real payment credentials.
- Uncontrolled shared test data.

Ensure test data is cleaned up safely.

Tests should remain repeatable.

## 16. Mocking and Test Isolation

Use mocks and stubs to isolate components when necessary.

Suitable examples:

- Email services.
- Payment gateways.
- External APIs.
- Message queues.
- Cloud storage clients.

However:

- Do not mock the component whose actual behavior you intend to verify.
- Do not use mocks as a substitute for all integration testing.
- Ensure mock behavior reflects the real dependency contract.
- Include integration tests for important real-world interactions.

## 17. Test Coverage and Quality

Measure coverage where useful.

Consider:

- Line coverage.
- Branch coverage.
- Function or method coverage.
- Critical business-rule coverage.

Do not treat a high coverage percentage as proof of correctness.

Prioritize meaningful tests for:

- Financial calculations.
- Authentication.
- Authorization.
- Data integrity.
- Sensitive operations.
- Important business workflows.

A small number of strong tests is more valuable than many meaningless assertions.

## 18. Test Automation and Continuous Integration

Automate relevant tests in the development workflow.

A typical CI process should:

1. Install dependencies.
2. Validate project configuration.
3. Compile or build the application.
4. Run unit tests.
5. Run integration tests.
6. Run relevant security and dependency checks.
7. Generate test reports.
8. Fail the pipeline when required checks fail.

Do not bypass failing tests simply to achieve a successful deployment.

Separate fast tests from slower integration and end-to-end tests where useful.

## 19. Framework-Specific Testing Awareness

Choose tools appropriate to the project's existing technology.

Examples:

**Java / Spring Boot**

- JUnit 5.
- Mockito.
- Spring Boot Test.
- MockMvc.
- Testcontainers.
- REST Assured.

**Node.js**

- Jest.
- Vitest.
- Supertest.
- Node.js built-in test runner.
- Playwright where end-to-end testing is appropriate.

**Python**

- pytest.
- unittest.
- FastAPI TestClient.
- Django test framework.

**.NET**

- xUnit.
- NUnit.
- MSTest.
- WebApplicationFactory.

Inspect the project and verify tool compatibility before adding dependencies.

Do not assume that every project uses the latest version of a framework.

## 20. Secure Test Environments

Maintain separation between:

- Development.
- Testing.
- Staging.
- Production.

Ensure that:

- Tests do not accidentally connect to production databases.
- Test secrets are separate from production secrets.
- Test environments use appropriate access restrictions.
- Destructive operations are isolated.
- Logs do not expose sensitive test data.
- External integrations use sandbox environments where available.

## 21. Backend Testing Workflow

Follow this process when testing backend changes.

### Phase 1: Understand

- Inspect the project.
- Understand the feature requirements.
- Identify relevant components.
- Review existing tests.
- Identify dependencies.

### Phase 2: Plan

- Define expected behavior.
- Identify positive test cases.
- Identify negative test cases.
- Identify edge cases.
- Identify security concerns.
- Select suitable testing levels.

### Phase 3: Prepare

- Configure the test environment.
- Prepare test data.
- Configure mocks where necessary.
- Ensure that tests are isolated.

### Phase 4: Implement

- Write clear and maintainable tests.
- Follow project conventions.
- Include meaningful assertions.
- Cover important failure scenarios.

### Phase 5: Execute

- Run the relevant tests.
- Run the full test suite where appropriate.
- Inspect failures.
- Investigate flaky tests.
- Verify that the build succeeds.

### Phase 6: Report

Provide:

- Tests created.
- Tests executed.
- Passed tests.
- Failed tests.
- Defects identified.
- Fixes implemented.
- Remaining risks.
- Recommended next actions.

Never report a test as passed if it was not actually executed successfully.

## 22. Prohibited Practices

Never:

- Test against production data without authorization.
- Ignore failing tests without explanation.
- Claim that unexecuted tests passed.
- Use real production credentials in test files.
- Make all external integrations depend on live services.
- Write tests that depend unnecessarily on execution order.
- Remove tests merely to make a build pass.
- Treat code coverage as proof of correctness.
- Ignore negative and boundary test cases.
- Perform unauthorized load or security testing.

## 23. Definition of Done

A backend testing task is complete when:

- Relevant requirements have test coverage.
- Positive scenarios have been tested.
- Negative scenarios have been tested.
- Important boundary conditions have been considered.
- Authentication and authorization have been verified where applicable.
- Database behavior has been tested where applicable.
- Relevant security checks have been performed.
- Tests are repeatable and maintainable.
- The build and relevant test suites have been executed.
- Failures and limitations are documented accurately.

## 24. Related Skills

Use this skill alongside:

- `backend-development`
- `api-engineering`
- `backend-security`
- `frontend-testing`
- `security-standard`
- `quality-standard`
- `database-engineering` (when available)

---

**Final instruction:** Build tests that verify real application behavior. Prioritize critical functionality, security boundaries, data integrity, and meaningful failure scenarios. Report only results that have actually been verified.