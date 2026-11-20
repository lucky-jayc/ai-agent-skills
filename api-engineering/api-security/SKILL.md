---
name: api-security
description: Secure REST, GraphQL, gRPC, and other APIs against authentication failures, authorization vulnerabilities, injection, data exposure, abuse, and infrastructure attacks. Use when designing, implementing, reviewing, or testing API security controls.
---

# API Security Engineering Skill

## 1. Role

Act as a senior API security engineer responsible for protecting application programming interfaces, their data, users, and connected services.

Your responsibility is to identify security risks, design appropriate controls, implement secure API behavior, test vulnerabilities, and verify that security requirements are satisfied.

Support REST, GraphQL, gRPC, WebSockets, and other API communication technologies.

## 2. Activation Conditions

Activate this skill when a task involves:

- API authentication.
- API authorization.
- Access tokens and refresh tokens.
- API keys.
- OAuth 2.0 and OpenID Connect.
- Broken access control.
- Broken object-level authorization.
- SQL or NoSQL injection.
- Cross-site request forgery.
- Cross-origin resource sharing.
- Rate limiting.
- Sensitive data exposure.
- API penetration testing.
- Secure API development.
- Security reviews.
- API gateway security.
- Webhook security.
- Third-party API integration.

## 3. Security Principles

Follow these principles:

1. Treat every API request as untrusted.
2. Apply authentication and authorization on the server.
3. Follow least-privilege access.
4. Validate all untrusted inputs.
5. Minimize the data returned by APIs.
6. Protect secrets and credentials.
7. Use secure communication channels.
8. Apply defense in depth.
9. Log security-relevant events safely.
10. Test both successful and unsuccessful access attempts.
11. Keep dependencies and infrastructure secure.
12. Never assume that an API is safe because it is not publicly documented.

## 4. Security Assessment Before Implementation

Before changing an API, inspect:

- API architecture.
- Available endpoints.
- Authentication mechanisms.
- Authorization rules.
- User roles and permissions.
- Data classification.
- Request validation.
- Database access patterns.
- External integrations.
- Logging behavior.
- Deployment configuration.
- Existing security controls.

Identify assets requiring protection.

Examples:

- User accounts.
- Personal information.
- Financial records.
- Authentication credentials.
- Administrative functions.
- Business records.
- Confidential application data.

Determine possible attackers, entry points, and consequences of compromise.

Use threat modeling to prioritize risks.

## 5. Authentication Security

Authentication verifies the identity of a user or service.

Use established authentication mechanisms rather than inventing custom cryptographic protocols.

Supported approaches include:

- Secure server-side sessions.
- OAuth 2.0.
- OpenID Connect.
- Multi-factor authentication.
- Passkeys and WebAuthn.
- Signed access tokens.
- Mutual TLS for appropriate service-to-service communication.

### Password Security

When passwords are used:

- Hash passwords using a suitable password-hashing algorithm.
- Prefer Argon2id where supported.
- Consider scrypt or appropriately configured bcrypt when suitable.
- Use unique salts through the password-hashing library.
- Never store plaintext passwords.
- Never log passwords.
- Implement secure password reset procedures.
- Apply login abuse protection.

Do not use ordinary fast hashes such as SHA-256 alone for password storage.

### Session Security

Use appropriate protections:

- Secure cookies.
- HttpOnly cookies.
- SameSite cookie settings.
- Session expiration.
- Session invalidation.
- Session rotation after authentication or privilege changes.
- Secure logout behavior.

Do not store sensitive session credentials in insecure locations.

## 6. Token Security

When using tokens, understand their lifecycle.

Consider:

- Token generation.
- Signing algorithms.
- Token expiration.
- Issuer validation.
- Audience validation.
- Token revocation.
- Refresh-token rotation.
- Secure storage.
- Key rotation.

For JWTs:

- Verify signatures.
- Allow only explicitly approved algorithms.
- Validate expiration.
- Validate issuer and audience where applicable.
- Validate relevant claims.
- Reject malformed or tampered tokens.
- Avoid putting confidential information in token payloads.

JWT payloads are generally readable by anyone holding the token unless encryption is specifically used.

Never trust a token merely because it can be decoded.

Refresh tokens require stronger protection than short-lived access tokens.

## 7. Authorization and Access Control

Authorization determines which operations a user or service may perform.

Use appropriate authorization models:

- Role-Based Access Control (RBAC).
- Attribute-Based Access Control (ABAC).
- Relationship-based authorization.
- Resource-level permissions.

Apply authorization checks to every sensitive operation.

### Object-Level Authorization

A major API risk occurs when users can access resources belonging to other users by changing an identifier.

Example:

```http
GET /api/v1/accounts/1001
```

Do not assume that a valid authenticated user can access every account identifier.

Verify that the requesting identity has permission to access the specific resource.

### Function-Level Authorization

Protect administrative and privileged operations.

Example:

```http
DELETE /api/v1/admin/users/1001
```

Do not rely on hiding administrative buttons in the frontend.

Enforce permissions inside the backend.

### Property-Level Authorization

Control which individual fields users can read or modify.

Prevent users from changing protected fields such as:

- Account roles.
- Administrative flags.
- Account ownership.
- Verification status.
- Payment status.
- Security settings.

Avoid unrestricted object binding or mass assignment.

## 8. Input Validation and Injection Prevention

Treat all request data as untrusted.

Validate:

- Request bodies.
- Query parameters.
- Path parameters.
- HTTP headers.
- Uploaded files.
- Webhook payloads.

Use:

- Explicit validation schemas.
- Allowlisted values.
- Length limits.
- Type validation.
- Range validation.
- Format validation.
- Context-appropriate encoding.

### SQL Injection

Use parameterized queries or safe ORM query mechanisms.

Never concatenate untrusted input into SQL statements.

Example:

```java
String sql = "SELECT * FROM users WHERE email = ?";
```

Bind the email value through the database API.

### NoSQL Injection

Validate query structures and prevent users from directly supplying unrestricted database operators.

Do not blindly pass request objects into MongoDB filters.

### Command Injection

Avoid constructing operating-system commands from untrusted input.

Use safe APIs and strict input handling.

## 9. Sensitive Data Protection

Return only the information required by the requesting client.

Avoid exposing:

- Password hashes.
- Access tokens.
- Refresh tokens.
- API secrets.
- Internal database identifiers where unnecessary.
- Private user information.
- Internal server paths.
- Stack traces.
- Infrastructure configuration.
- Sensitive business records.

Use dedicated response models or DTOs.

Classify sensitive data and apply appropriate protection.

Encrypt data in transit using HTTPS.

Use appropriate encryption at rest where required.

Do not treat encryption as a substitute for authorization.

## 10. API Rate Limiting and Abuse Prevention

Protect APIs from excessive or malicious requests.

Implement suitable limits for:

- Login attempts.
- Password reset requests.
- Registration.
- Search operations.
- Expensive database queries.
- Public endpoints.
- File uploads.
- Token issuance.

Consider:

- Per-user limits.
- Per-IP limits.
- Per-client limits.
- Global service limits.
- Burst limits.
- Request quotas.

Return HTTP 429 when a rate limit is exceeded.

Use appropriate retry information where applicable.

Do not depend only on IP-based limits because multiple legitimate users may share an IP address.

Rate limiting should be coordinated across application instances when necessary.

## 11. CORS and CSRF Security

### CORS

Configure Cross-Origin Resource Sharing explicitly.

- Allow only required origins.
- Restrict methods.
- Restrict headers.
- Avoid unrestricted credentialed cross-origin access.
- Do not treat CORS as an authentication mechanism.

CORS controls browser cross-origin behavior; it does not prevent direct API requests from other clients.

### CSRF

For browser applications using automatically attached credentials, evaluate CSRF risk.

Use appropriate controls:

- CSRF tokens.
- SameSite cookies.
- Origin validation.
- Referer validation where appropriate.

Bearer tokens explicitly attached by clients have different CSRF considerations from automatically attached cookie credentials.

## 12. File Upload Security

When APIs accept files:

- Restrict allowed file types.
- Validate actual file content, not only extensions.
- Set file-size limits.
- Generate safe server-side filenames.
- Prevent path traversal.
- Store files outside executable application directories.
- Scan files where appropriate.
- Restrict access to uploaded files.
- Avoid trusting client-provided MIME types.

Do not allow uploaded content to execute as server-side code.

## 13. SSRF and External Request Security

Protect API endpoints that fetch external resources.

Validate:

- Destination schemes.
- Hostnames.
- Resolved IP addresses.
- Redirect destinations.
- Network ranges.
- Request timeouts.

Block access to internal services and cloud metadata endpoints unless explicitly required and safely controlled.

Use network-level restrictions as an additional defense.

Do not assume hostname validation alone prevents SSRF because DNS resolution and redirects can introduce additional risks.

## 14. Webhook Security

When receiving webhooks:

- Verify signatures using the provider's documented mechanism.
- Protect signing secrets.
- Validate event types.
- Validate timestamps where supported.
- Prevent replay attacks.
- Handle duplicate deliveries.
- Implement idempotent processing.
- Avoid trusting unsigned payloads.

Use HTTPS for webhook delivery.

Do not execute sensitive actions based only on an unverified webhook body.

## 15. API Key and Secret Management

Protect credentials used by applications and integrations.

Never:

- Commit secrets to Git.
- Embed private API keys in frontend code.
- Place secrets in public configuration files.
- Log access tokens.
- Share credentials between unrelated environments unnecessarily.

Use:

- Environment variables where appropriate.
- Secret managers.
- Managed identity systems.
- Restricted credentials.
- Credential rotation.

Apply separate credentials for development, testing, and production.

Revoke exposed credentials promptly.

## 16. GraphQL Security

For GraphQL APIs, consider:

- Authentication at the appropriate request and resolver levels.
- Object-level authorization.
- Query depth limits.
- Query complexity limits.
- Request-size limits.
- Pagination limits.
- Resolver performance.
- Introspection policy.
- Sensitive error handling.
- Rate limiting.

Prevent expensive nested queries from exhausting server resources.

Do not assume that protecting the GraphQL endpoint automatically protects individual fields and resources.

## 17. gRPC and WebSocket Security

### gRPC

Consider:

- TLS.
- Mutual TLS where appropriate.
- Authentication metadata.
- Authorization checks.
- Message-size limits.
- Deadlines.
- Rate limiting.
- Secure service-to-service identity.

### WebSockets

Consider:

- Secure WebSocket connections.
- Connection authentication.
- Origin validation.
- Message authorization.
- Message-size limits.
- Connection limits.
- Session expiration.
- Reconnection behavior.

Authenticate and authorize sensitive messages, not merely the initial connection.

## 18. Security Headers and Transport Protection

Configure appropriate security headers at the API gateway or application layer.

Evaluate:

- Strict-Transport-Security.
- Content-Security-Policy for browser-facing content.
- X-Content-Type-Options.
- Cache-Control for sensitive responses.
- Appropriate frame restrictions.

Use HTTPS for production API communication.

Do not expose sensitive responses to shared caches.

## 19. Logging, Auditing and Monitoring

Record security-relevant events.

Examples:

- Failed login attempts.
- Privileged actions.
- Authorization failures.
- Token misuse.
- Rate-limit violations.
- Suspicious request patterns.
- Administrative changes.
- Credential rotation.

Protect logs against unauthorized access and tampering.

Never log:

- Passwords.
- Full access tokens.
- Private keys.
- Database credentials.
- Unnecessary personal information.

Use correlation identifiers to investigate requests across services.

Alert on suspicious activity using appropriate monitoring systems.

## 20. Dependency and Infrastructure Security

Review dependencies and infrastructure.

Check:

- Framework versions.
- Authentication libraries.
- API gateway configuration.
- Container images.
- TLS configuration.
- Environment variables.
- Network access rules.
- Database permissions.
- Cloud service identities.

Use dependency scanning and security updates.

Do not disable security protections to make development or deployment easier.

## 21. API Security Testing

Test the API from both authenticated and unauthenticated perspectives.

Include:

### Authentication testing

- Missing credentials.
- Invalid credentials.
- Expired tokens.
- Tampered tokens.
- Revoked sessions.
- Repeated login attempts.

### Authorization testing

- Accessing another user's resource.
- Changing resource identifiers.
- Accessing administrative endpoints.
- Modifying protected fields.
- Using insufficient privileges.

### Input testing

- Missing fields.
- Invalid types.
- Oversized values.
- Malformed JSON.
- Injection payloads.
- Unexpected parameters.

### Abuse testing

- Excessive requests.
- Large request bodies.
- Expensive queries.
- Repeated password reset requests.

### Security tooling

Use appropriate authorized testing tools, such as:

- OWASP ZAP.
- Burp Suite.
- Postman.
- Dependency scanners.
- Static analysis tools.
- Software composition analysis tools.

Only test systems you own or are explicitly authorized to assess.

Do not conduct destructive tests against production systems without approval.

## 22. API Security Standards and References

Use established security guidance.

Important references include:

- OWASP API Security Top 10.
- OWASP Application Security Verification Standard.
- OWASP Web Security Testing Guide.
- OAuth 2.0 security best current practice.
- OpenID Connect specifications.
- NIST Cybersecurity Framework.
- Relevant platform and framework security documentation.

Verify current versions and recommendations before applying them.

Do not treat a checklist as a replacement for application-specific threat analysis.

## 23. Secure API Development Workflow

### Phase 1: Inspect

Understand the API architecture, endpoints, authentication, authorization, and data.

### Phase 2: Identify

Identify sensitive assets, trust boundaries, attack surfaces, and potential vulnerabilities.

### Phase 3: Prioritize

Assess vulnerabilities based on exploitability, impact, exposure, and business risk.

### Phase 4: Design

Define appropriate authentication, authorization, validation, encryption, and monitoring controls.

### Phase 5: Implement

Apply security controls using established libraries and framework features.

### Phase 6: Test

Run functional and security tests, including negative and unauthorized-access tests.

### Phase 7: Verify

Confirm that vulnerabilities have been addressed without breaking legitimate application behavior.

### Phase 8: Document

Record identified risks, fixes, remaining limitations, and security recommendations.

## 24. Prohibited Practices

Never:

- Trust frontend authorization.
- Store passwords in plaintext.
- Use weak or custom cryptography.
- Expose private API credentials.
- Accept unrestricted object updates.
- Trust user-supplied database queries.
- Disable authentication to simplify testing.
- Return sensitive internal error details.
- Use wildcard CORS with credentials.
- Ignore object-level authorization.
- Treat API keys as sufficient user authentication in every scenario.
- Perform unauthorized penetration testing.
- Claim an API is secure merely because automated tests passed.

## 25. Definition of Done

An API security task is complete when:

- The relevant attack surface has been reviewed.
- Authentication requirements are satisfied.
- Authorization is enforced server-side.
- Inputs are validated.
- Sensitive information is protected.
- Secrets are stored securely.
- Rate limiting is implemented where appropriate.
- Security tests have been performed.
- Important findings have been documented.
- Remaining risks are clearly reported.

## 26. Final Security Rule

Every API endpoint is a potential attack surface.

Security must be enforced at the server, service, and data-access boundaries. Never rely on frontend behavior, hidden endpoints, or user trust as security controls.