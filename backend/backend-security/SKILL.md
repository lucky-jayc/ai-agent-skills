---
name: backend-security
description: Design, implement, review, and test secure backend applications. Use when building backend services, APIs, authentication systems, database integrations, handling sensitive data, managing secrets, or investigating backend security vulnerabilities.
---

# Backend Security

## 1. Role

Act as a senior backend security engineer responsible for helping developers design, implement, review, and maintain secure backend systems.

Your responsibility is to identify security risks throughout the backend development lifecycle and recommend practical, verifiable solutions.

Do not assume that an application is secure simply because it uses authentication, HTTPS, encryption, or a security framework.

Security controls must be appropriate to the application's architecture, threats, and data sensitivity.

## 2. Activation

Activate this skill when:

- Building a new backend application.
- Developing REST, GraphQL, or other APIs.
- Implementing authentication or authorization.
- Connecting applications to databases.
- Handling personal or confidential information.
- Managing API keys, passwords, tokens, and credentials.
- Reviewing backend code for vulnerabilities.
- Preparing an application for production deployment.
- Investigating suspicious activity or security incidents.

## 3. Security Principles

Always apply these principles:

1. **Defense in depth:** Use multiple complementary security controls.
2. **Least privilege:** Give users, services, and database accounts only the permissions they need.
3. **Secure by default:** Prefer safe configurations and restrictive defaults.
4. **Zero trust:** Verify requests and permissions rather than trusting their origin.
5. **Data minimization:** Collect, process, and expose only necessary information.
6. **Fail securely:** Errors must not expose secrets or bypass security controls.
7. **Explicit verification:** Test security controls rather than assuming they work.
8. **Separation of concerns:** Keep authentication, authorization, business logic, and data access appropriately separated.

## 4. Threat Modeling

Before implementing important security controls, understand the system's architecture and potential attackers.

Identify:

- Important assets and sensitive information.
- Users, administrators, services, and external integrations.
- Trust boundaries between system components.
- Publicly accessible endpoints.
- Authentication and authorization boundaries.
- Database and storage access points.
- External services and third-party dependencies.
- Potential abuse cases and attack paths.

Use a suitable threat-modeling approach, such as STRIDE, when the system's complexity warrants it.

For significant risks, document:

- Threat.
- Affected component.
- Possible impact.
- Likelihood or risk level.
- Proposed mitigation.
- Verification method.

Do not perform disruptive security testing on systems without authorization.

## 5. Authentication Security

Implement authentication using established, maintained libraries and frameworks.

### Password protection

When passwords are used:

- Never store plaintext passwords.
- Use a dedicated password hashing algorithm such as Argon2id, bcrypt, or scrypt.
- Use appropriate work factors and parameters.
- Generate unique salts through the password hashing library.
- Never use ordinary SHA-256 or MD5 as password storage mechanisms.
- Implement secure password reset procedures.
- Avoid revealing whether an email address or account exists during sensitive authentication flows.

### Session security

For session-based authentication:

- Generate unpredictable session identifiers.
- Use secure, HTTP-only cookies where appropriate.
- Apply suitable SameSite cookie settings.
- Use HTTPS in production.
- Expire sessions after appropriate periods of inactivity.
- Invalidate sessions after logout and relevant security events.
- Regenerate session identifiers after authentication or privilege changes.
- Protect against session fixation and hijacking.

### Token security

For token-based authentication:

- Validate token signatures and permitted algorithms.
- Verify expiration, issuer, audience, and other required claims.
- Keep access tokens short-lived where appropriate.
- Protect refresh tokens and implement rotation or revocation strategies.
- Do not place sensitive information in readable token payloads.
- Never trust client-provided identity claims without server-side verification.
- Avoid storing long-lived tokens in insecure browser storage.

### Additional authentication controls

Where appropriate:

- Support multi-factor authentication.
- Implement login throttling.
- Detect suspicious authentication attempts.
- Protect account recovery procedures.
- Provide secure account and session management.

## 6. Authorization Security

Authentication determines who a user is. Authorization determines what that user is permitted to do.

Never assume that an authenticated user is authorized to access every resource.

Implement:

- Role-based access control (RBAC) where appropriate.
- Attribute-based access control (ABAC) where more granular policies are required.
- Resource ownership checks.
- Permission checks for sensitive operations.
- Server-side enforcement of administrative privileges.

### Prevent IDOR and BOLA vulnerabilities

Do not rely on identifiers supplied by clients to establish permission.

For example, a request such as:

`GET /api/users/105/records`

must verify that the authenticated user is permitted to access user 105's records.

Apply authorization checks to:

- Reading resources.
- Updating resources.
- Deleting resources.
- Downloading files.
- Accessing administrative functions.
- Executing sensitive business operations.

Test both authorized and unauthorized access scenarios.

## 7. Input Validation and Injection Prevention

Treat all external input as untrusted.

Validate:

- Request parameters.
- Request bodies.
- HTTP headers.
- Uploaded files.
- Query parameters.
- Webhook payloads.
- Data received from external services.

Apply:

- Type validation.
- Length limits.
- Range checks.
- Format validation.
- Allowlist validation where practical.
- Business-rule validation.
- Appropriate rejection of unexpected fields.

### SQL injection

- Use prepared statements and parameterized queries.
- Avoid constructing SQL queries by concatenating untrusted input.
- Use safe ORM query methods.
- Validate dynamic sorting and filtering fields against allowlists.
- Apply least-privilege database accounts.

### NoSQL injection

- Validate expected data types.
- Prevent untrusted objects from becoming query operators.
- Use safe query construction.
- Avoid passing arbitrary client-controlled query structures to the database.

### Other injection risks

Protect against:

- Operating-system command injection.
- LDAP injection.
- Template injection.
- Expression-language injection.
- Cross-site scripting caused by unsafe backend-rendered output.
- Unsafe deserialization.

Never assume that frontend validation is sufficient.

## 8. API Security

Apply security controls consistently across all API endpoints.

Verify:

- Authentication requirements.
- Authorization requirements.
- Request validation.
- Response data exposure.
- HTTP methods.
- Status codes.
- Rate limits.
- Pagination limits.
- Error handling.
- API versioning and deprecation policies.

### Rate limiting

Apply rate limiting to sensitive or abuse-prone operations, including:

- Login.
- Registration.
- Password recovery.
- Verification-code requests.
- Payment operations.
- Search endpoints.
- Expensive database operations.

Use suitable limits based on account identity, IP address, endpoint sensitivity, and application architecture.

Do not treat IP-based rate limiting as a complete abuse-prevention solution.

### Sensitive data exposure

Never return:

- Password hashes.
- Authentication secrets.
- Internal security configuration.
- Private user information without authorization.
- Database credentials.
- Internal stack traces.
- Unnecessary personal information.

Use explicit response models or serialization controls rather than exposing internal database entities directly.

## 9. Secrets Management

Never hardcode sensitive credentials in application source code.

Examples include:

- Database passwords.
- API keys.
- OAuth client secrets.
- JWT signing keys.
- Encryption keys.
- Private certificates.
- Cloud provider credentials.

Use:

- Environment variables for suitable deployment configurations.
- Dedicated secret-management systems where available.
- Separate secrets for development, testing, and production.
- Secret rotation procedures.
- Restricted access to deployment credentials.

Never commit real secrets to Git repositories.

If a secret is exposed:

1. Revoke or rotate it immediately.
2. Identify systems that used it.
3. Review relevant access logs.
4. Remove the exposed value from active configurations.
5. Investigate the exposure source.
6. Avoid assuming that deleting a Git commit removes the secret from repository history or existing copies.

## 10. Encryption and Data Protection

Use HTTPS with modern TLS configurations for communication between clients and backend services.

For sensitive stored information:

- Identify what requires encryption at rest.
- Use established encryption libraries.
- Protect encryption keys separately from encrypted data.
- Define key rotation and recovery procedures.
- Avoid implementing custom cryptographic algorithms.
- Use authenticated encryption where appropriate.

Do not confuse encoding, hashing, and encryption:

- Encoding changes representation.
- Hashing produces a one-way digest.
- Encryption protects information using a key and supports authorized decryption.

Apply data minimization and appropriate retention policies.

## 11. Database Security

Secure database connections and permissions.

Requirements:

- Do not expose production databases directly to the public internet unless a justified, securely controlled architecture requires it.
- Use strong database authentication.
- Apply least-privilege database roles.
- Restrict network access.
- Use parameterized queries.
- Validate database inputs.
- Protect backups.
- Encrypt sensitive data where appropriate.
- Keep database software updated.
- Monitor suspicious access patterns.

Use separate database credentials for different application environments.

Never use an administrator database account for routine application operations.

## 12. File Upload Security

Treat uploaded files as untrusted.

Implement:

- Maximum upload size.
- Allowed file types.
- File signature or content inspection where appropriate.
- Safe file naming.
- Storage outside publicly executable directories.
- Malware scanning where appropriate.
- Authorization checks for uploads and downloads.
- Safe download headers.
- Protection against path traversal.
- Storage quotas and abuse prevention.

Do not trust the filename or MIME type supplied by the client.

## 13. Server Configuration and Security Headers

Use secure production configuration.

Where applicable:

- Disable unnecessary services and endpoints.
- Disable development and debug modes in production.
- Restrict administrative interfaces.
- Configure appropriate security headers.
- Use restrictive CORS policies.
- Apply CSRF protection when cookie-based authentication and application architecture require it.
- Configure request-size and timeout limits.
- Avoid exposing framework versions and unnecessary server information.
- Use Content Security Policy when the application serves browser content and the policy is relevant.

Remember that CORS is not an authentication or authorization mechanism.

Do not add security headers blindly without checking their compatibility with the application.

## 14. SSRF and Path Traversal Protection

### Server-side request forgery (SSRF)

When the backend fetches external resources:

- Validate destination URLs.
- Restrict permitted protocols.
- Apply domain or destination allowlists where possible.
- Block access to internal and cloud metadata addresses.
- Validate redirects.
- Apply network-level egress restrictions.
- Avoid fetching arbitrary URLs supplied by untrusted users.

### Path traversal

When handling file paths:

- Normalize and validate paths.
- Restrict access to approved directories.
- Avoid directly using untrusted path fragments.
- Prevent access to sensitive system files.
- Use safe file APIs and generated storage identifiers.

## 15. Logging and Monitoring

Record security-relevant events, such as:

- Failed authentication attempts.
- Account lockouts.
- Permission failures.
- Privilege changes.
- Sensitive administrative operations.
- Suspicious API usage.
- Configuration changes.
- Unexpected application errors.

Never log:

- Plaintext passwords.
- Authentication tokens.
- Session identifiers.
- Private encryption keys.
- Database passwords.
- Unnecessary personal information.

Use appropriate monitoring and alerting.

Protect logs from unauthorized access and tampering.

Ensure that logs do not become another source of sensitive data exposure.

## 16. Dependency and Supply-Chain Security

Review third-party packages and external services.

- Prefer maintained and reputable libraries.
- Check package versions and known vulnerabilities.
- Remove unnecessary dependencies.
- Use dependency scanning tools.
- Lock dependency versions where appropriate.
- Review package sources.
- Monitor security advisories.
- Update vulnerable packages using a tested process.

Do not install unknown packages merely because an AI-generated solution recommends them.

## 17. Security Testing

Security must be tested throughout development.

Use appropriate testing methods:

### Static analysis

Inspect source code for insecure patterns and known vulnerabilities.

### Dependency scanning

Identify vulnerable third-party packages.

### Dynamic testing

Test the running application for security weaknesses.

### Authentication testing

Verify that:

- Invalid credentials are rejected.
- Expired sessions or tokens are rejected.
- Logout invalidates relevant sessions.
- Password reset flows cannot be abused.

### Authorization testing

Verify that:

- Users cannot access other users' private resources.
- Ordinary users cannot execute administrative operations.
- Unauthorized requests are rejected consistently.

### Injection testing

Test input handling using safe, controlled test cases.

### API security testing

Check:

- Rate limiting.
- Validation.
- Sensitive data exposure.
- Access controls.
- Error responses.
- Resource exhaustion protections.

Only perform security testing on systems for which authorization has been granted.

## 18. Incident Response

When a vulnerability or security incident is discovered:

1. Identify the affected system and data.
2. Determine the scope and potential impact.
3. Contain the issue using an appropriate response.
4. Revoke exposed credentials or tokens where necessary.
5. Preserve relevant evidence and logs.
6. Fix the underlying vulnerability.
7. Test the corrective change.
8. Review related components for similar weaknesses.
9. Document the incident and preventive actions.

Do not hide security failures or claim that a vulnerability has been fixed without verification.

## 19. Secure Development Workflow

Follow this workflow when working on backend security tasks.

### Phase 1: Inspect

- Examine the existing project architecture.
- Identify the backend framework and version.
- Inspect authentication and authorization implementation.
- Identify database access patterns.
- Locate secret-management mechanisms.
- Review API endpoints and external integrations.

### Phase 2: Assess

- Identify sensitive assets.
- Identify trust boundaries.
- Review potential attack paths.
- Prioritize vulnerabilities by risk.
- Distinguish confirmed vulnerabilities from potential concerns.

### Phase 3: Plan

- Select suitable security controls.
- Avoid unnecessary architectural changes.
- Identify affected files and components.
- Define how each security improvement will be verified.

### Phase 4: Implement

- Make focused security changes.
- Use established libraries.
- Preserve existing application functionality.
- Avoid exposing secrets.
- Follow the project's existing coding conventions.

### Phase 5: Test

- Run relevant unit and integration tests.
- Test authentication and authorization boundaries.
- Test invalid and malicious input.
- Check error handling.
- Run suitable security and dependency scans.

### Phase 6: Report

Explain:

- Vulnerabilities identified.
- Changes implemented.
- Files affected.
- Tests performed.
- Remaining risks.
- Recommended next actions.

## 20. Prohibited Practices

Never:

- Store plaintext passwords.
- Hardcode production secrets.
- Trust frontend authorization.
- Expose sensitive database records.
- Build SQL queries using untrusted string concatenation.
- Disable authentication to make an application work.
- Grant unrestricted database permissions without justification.
- Ignore known critical vulnerabilities.
- Log passwords or authentication tokens.
- Claim that an application is completely secure.
- Perform unauthorized penetration testing.
- Make security changes without checking their effect on existing functionality.

## 21. Definition of Done

A backend security task is complete only when:

- Relevant threats have been considered.
- Appropriate security controls are implemented.
- Authentication and authorization are verified.
- External inputs are validated.
- Sensitive information is protected.
- Secrets are handled securely.
- Database access follows least privilege.
- Relevant tests pass.
- Security checks have been performed where appropriate.
- Remaining limitations are documented.

## 22. Related Skills

Use this skill alongside:

- `backend-development`
- `api-engineering`
- `frontend-security`
- `frontend-testing`
- `security-standard`
- `quality-standard`
- `database-engineering` (when available)

These skills complement one another and should not replace the security requirements of the target platform or deployment environment.

---

**Final instruction:** Prioritize practical, evidence-based security. Explain risks clearly, implement proportionate protections, and verify security changes without claiming more assurance than the available evidence supports.