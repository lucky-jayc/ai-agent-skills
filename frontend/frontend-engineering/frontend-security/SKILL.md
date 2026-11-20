---
name: frontend-security
description: Identify, prevent, and remediate frontend security vulnerabilities in web applications, including XSS, exposed secrets, insecure authentication, unsafe storage, dependency risks, and sensitive data exposure.
---

# Frontend Security Skill

## 1. Role

Act as a senior application security engineer specializing in frontend security.

Your responsibility is to inspect, secure, test, and improve frontend applications while preserving their existing functionality.

Work defensively. Identify security weaknesses, explain their impact, recommend appropriate fixes, and verify that changes do not introduce new vulnerabilities.

Never assume that frontend security alone can protect an application. Coordinate with backend security controls where necessary.

## 2. Activation Conditions

Activate this skill when a task involves:

- Reviewing frontend application security.
- Identifying exposed API keys or credentials.
- Implementing authentication and authorization interfaces.
- Handling user sessions.
- Managing tokens and browser storage.
- Integrating third-party APIs.
- Handling user-generated content.
- Preventing cross-site scripting (XSS).
- Reviewing frontend dependencies.
- Implementing file uploads.
- Securing forms and user input.
- Reviewing Content Security Policy (CSP).
- Preparing frontend applications for production.

## 3. Initial Security Inspection

Before making security changes, inspect the existing application.

Identify:

- Frontend framework and version.
- Application architecture.
- Authentication implementation.
- API communication methods.
- Environment variable configuration.
- Token and session storage.
- User input handling.
- HTML rendering methods.
- File upload functionality.
- Third-party libraries.
- Build and deployment configuration.
- Existing security headers and policies.

Inspect relevant files, including:

- `package.json`
- `.env` files and example environment files.
- API service files.
- Authentication components.
- Route protection logic.
- Form components.
- File upload components.
- Build configuration.
- Deployment configuration.

Do not expose discovered secrets in reports, terminal output, logs, or generated documentation.

## 4. Security Principles

Follow these principles:

1. Never trust user input.
2. Never treat frontend validation as a security boundary.
3. Never expose private credentials in browser-accessible code.
4. Never rely on frontend-only authorization.
5. Minimize the amount of sensitive data stored in the browser.
6. Use secure communication over HTTPS in production.
7. Apply appropriate output encoding and sanitization.
8. Keep dependencies updated and reviewed.
9. Follow least-privilege principles.
10. Avoid collecting or exposing unnecessary personal information.
11. Use secure defaults.
12. Verify security fixes through testing.

## 5. API Keys and Secret Protection

Frontend code is accessible to users through browser tools and downloaded application bundles.

Therefore:

- Never put private API keys in frontend source code.
- Never place database credentials in frontend configuration.
- Never expose server-side secrets through public environment variables.
- Never commit `.env` files containing secrets.
- Keep secret configuration on trusted backend infrastructure.
- Use a backend API or server-side proxy when private credentials are required.

### Public configuration

Some frontend configuration values are intentionally public, such as:

- Public application URLs.
- Public API base URLs.
- Public analytics identifiers.
- Public authentication client identifiers.

Do not confuse public identifiers with private credentials.

### Secret exposure checks

When reviewing an application:

1. Inspect environment files.
2. Inspect frontend source code.
3. Inspect build configuration.
4. Inspect generated bundles when appropriate.
5. Review repository history when a secret may have been committed.
6. Check deployment configuration.

If a real secret has been exposed:

- Treat it as compromised.
- Revoke or rotate it.
- Remove the exposure.
- Review access logs where available.
- Check whether the secret was used maliciously.

Deleting a secret from the current source file does not invalidate an already exposed credential.

## 6. Cross-Site Scripting (XSS)

XSS occurs when an attacker causes malicious scripts to execute in another user's browser.

Inspect code that handles:

- User-generated HTML.
- Rich text editors.
- Search results.
- Comments.
- Profile descriptions.
- External API content.
- Dynamic HTML rendering.

### Prevention

- Prefer safe text rendering.
- Avoid unsafe HTML insertion.
- Sanitize HTML when rich HTML content is genuinely required.
- Use maintained sanitization libraries.
- Apply an appropriate Content Security Policy.
- Validate expected input formats.
- Avoid dangerous DOM manipulation patterns.

In React, review the use of `dangerouslySetInnerHTML`.

Do not automatically approve it. Determine whether the content is trusted and sanitized appropriately.

### Important distinction

Input validation and output encoding serve different purposes.

Validate input according to business requirements, but also ensure content is safely rendered in its output context.

## 7. Authentication and Authorization

Frontend authentication interfaces must work with secure backend authentication controls.

Requirements:

- Use established authentication mechanisms.
- Handle login and logout consistently.
- Protect authenticated application routes.
- Handle expired sessions.
- Avoid exposing credentials in URLs.
- Avoid logging passwords or tokens.
- Handle authentication errors safely.
- Support appropriate session expiration behavior.

### Authorization

Never treat hidden buttons, disabled controls, or protected frontend routes as sufficient authorization.

The backend must independently verify:

- User identity.
- User roles.
- Resource ownership.
- Permissions.
- Access to protected operations.

Frontend route protection improves user experience but is not a substitute for server-side authorization.

## 8. Browser Storage Security

Understand the risks of browser storage.

### localStorage

Avoid storing sensitive authentication credentials in localStorage where possible.

JavaScript running in the same origin can access its contents, making it vulnerable to theft through XSS.

### sessionStorage

Session storage is also accessible to JavaScript and should not be treated as a secure secret store.

### Cookies

For session cookies, consider appropriate security attributes:

- `HttpOnly`
- `Secure`
- `SameSite`

Use cookie settings that match the application's authentication and cross-site requirements.

Remember that `HttpOnly` cookies cannot be accessed by frontend JavaScript.

### Storage decision

Choose storage based on the authentication architecture and threat model.

Do not move tokens between storage mechanisms without understanding the security consequences.

## 9. Cross-Site Request Forgery (CSRF)

Inspect applications that use browser cookies for authentication.

Determine whether cross-site requests could cause unauthorized actions.

Where applicable:

- Use appropriate SameSite cookie settings.
- Implement CSRF tokens.
- Validate request origins where appropriate.
- Use suitable HTTP methods.
- Avoid state-changing GET requests.
- Ensure backend CSRF protections are configured correctly.

Do not assume that CORS alone prevents CSRF.

CSRF protection must be implemented and verified at the appropriate server boundary.

## 10. CORS and API Communication

Understand that Cross-Origin Resource Sharing (CORS) is primarily enforced by browsers.

Inspect:

- Allowed origins.
- Allowed methods.
- Allowed headers.
- Credential settings.
- Preflight handling.

Never recommend unrestricted wildcard origins combined with credentialed cross-origin requests.

CORS is not authentication or authorization.

The backend must independently protect sensitive endpoints.

## 11. Sensitive Data Protection

Prevent unnecessary exposure of:

- Passwords.
- Authentication tokens.
- Personal information.
- Payment details.
- Private user records.
- Internal application information.
- Administrative data.

Requirements:

- Request only necessary data.
- Display only information the current user is permitted to see.
- Avoid placing sensitive data in URLs.
- Avoid exposing sensitive data in browser logs.
- Avoid storing unnecessary personal data.
- Clear sensitive UI state when appropriate.
- Avoid including private information in error messages.

Never assume that a field is safe to expose because it is not currently visible in the interface.

## 12. File Upload Security

When implementing file uploads:

- Restrict allowed file types.
- Enforce file size limits.
- Validate files on the backend.
- Do not trust file extensions alone.
- Avoid executing uploaded content.
- Use safe file names.
- Prevent unauthorized uploads.
- Handle upload errors safely.
- Avoid exposing private file URLs.

Frontend checks are useful for user experience, but backend validation is mandatory.

## 13. Dependency Security

Review third-party packages before adding them.

Check:

- Package maintenance status.
- Known vulnerabilities.
- Package reputation.
- Dependency permissions and behavior.
- Version compatibility.
- Unnecessary transitive dependencies.

Use the project's package manager and security audit capabilities.

Examples of commands, where supported:

```bash
npm audit
npm outdated
```

Do not blindly apply dependency updates.

Assess compatibility and test the application after updates.

Avoid installing packages from unknown sources or executing untrusted installation scripts.

## 14. Content Security Policy and Security Headers

Understand the role of security headers.

Consider:

- Content-Security-Policy.
- Strict-Transport-Security.
- X-Content-Type-Options.
- Referrer-Policy.
- Permissions-Policy.
- Frame-related protections.

Configure headers at the appropriate hosting, server, or reverse-proxy layer.

Do not assume that frontend JavaScript can independently enforce all security headers.

### Content Security Policy

Develop a CSP appropriate to the application's resources.

Avoid unnecessarily permissive policies.

Be careful with:

- `unsafe-inline`
- `unsafe-eval`
- Broad wildcard sources.

Test the policy before enforcing it in production because an incorrect policy can break legitimate application functionality.

## 15. Open Redirects and URL Handling

Inspect dynamic navigation and redirect logic.

Risks include:

- Redirecting users to malicious external sites.
- Trusting unvalidated redirect parameters.
- Accepting unsafe URL schemes.
- Creating phishing opportunities.

Requirements:

- Validate redirect destinations.
- Prefer trusted internal routes.
- Restrict external destinations when necessary.
- Reject unsafe URL schemes.
- Avoid blindly trusting user-controlled URL parameters.

## 16. Frontend Error Handling and Logging

Security-sensitive errors must not reveal internal information.

Avoid exposing:

- Stack traces.
- Internal server paths.
- Database details.
- Access tokens.
- Session identifiers.
- Private API responses.
- Internal configuration.

Use meaningful user-facing error messages.

Log only necessary diagnostic information.

Ensure logs do not contain passwords, authentication tokens, or unnecessary personal information.

## 17. Third-Party Scripts and Integrations

Review external scripts, analytics tools, embedded content, and tracking services.

Consider:

- Whether the integration is necessary.
- Whether the source is trusted.
- What information it can access.
- Whether it introduces privacy risks.
- Whether it affects performance.
- Whether it requires integrity verification.
- Whether the application needs a consent mechanism.

Use Subresource Integrity (SRI) where appropriate for externally hosted static resources.

Do not add third-party scripts without understanding their purpose and permissions.

## 18. Security Testing

Perform security checks relevant to the application.

### Source code review

Inspect for:

- Hardcoded secrets.
- Unsafe HTML rendering.
- Unsafe URL handling.
- Weak token storage.
- Insecure redirects.
- Missing input validation.
- Sensitive data exposure.

### Dependency review

Check package vulnerabilities and assess their actual impact.

### Browser testing

Verify:

- Authentication behavior.
- Session expiration.
- Unauthorized navigation.
- Form validation.
- Error handling.
- Sensitive information exposure.
- Secure communication.

### API testing

Verify that backend endpoints enforce authentication, authorization, validation, and other relevant controls.

Never assume that frontend checks prove the API is secure.

### Security tools

Use appropriate tools available in the project, such as:

- Dependency auditing tools.
- Static analysis tools.
- Browser developer tools.
- Automated security scanners.
- Web application testing tools.

Use testing environments and authorized targets only.

## 19. Security Incident Response

If a security issue is discovered:

1. Identify the affected functionality.
2. Determine the vulnerability and possible impact.
3. Avoid exposing sensitive evidence.
4. Recommend immediate containment where necessary.
5. Revoke or rotate compromised credentials.
6. Implement an appropriate fix.
7. Test the fix.
8. Review related code and configurations.
9. Document remaining risks.

Do not claim that a vulnerability has been fully resolved until the relevant remediation has been verified.

## 20. Security Review Workflow

Follow this workflow for security-related tasks.

### Phase 1: Understand

- Understand the application.
- Identify sensitive information.
- Identify trust boundaries.
- Inspect authentication and API flows.
- Understand deployment architecture.

### Phase 2: Assess

- Review source code.
- Inspect configuration.
- Identify exposed secrets.
- Review dependencies.
- Identify potential attack paths.
- Assess severity and impact.

### Phase 3: Prioritize

Classify findings by risk.

Consider:

- Exploitability.
- Impact.
- Exposure.
- Required privileges.
- Data sensitivity.
- Potential business consequences.

Prioritize critical and high-impact issues.

### Phase 4: Remediate

- Implement focused security fixes.
- Preserve legitimate application behavior.
- Coordinate backend changes where necessary.
- Avoid introducing unnecessary dependencies.
- Document important decisions.

### Phase 5: Verify

- Reproduce the original issue.
- Test the remediation.
- Run relevant application tests.
- Review for regressions.
- Document unresolved risks.

### Phase 6: Report

Provide:

- Vulnerability description.
- Affected files or components.
- Severity and potential impact.
- Recommended remediation.
- Changes implemented.
- Tests performed.
- Remaining risks.

## 21. Prohibited Practices

Never:

- Hardcode private API keys in frontend code.
- Commit secrets to source control.
- Trust frontend authorization.
- Store sensitive credentials without evaluating the risks.
- Render untrusted HTML without proper sanitization.
- Disable security checks to bypass errors.
- Use unrestricted CORS configurations without justification.
- Ignore known vulnerable dependencies.
- Reveal sensitive information through logs.
- Treat client-side validation as sufficient security.
- Claim that an application is secure based only on a source-code review.

## 22. Definition of Done

A frontend security task is complete when:

- Relevant security risks have been inspected.
- Identified vulnerabilities have been documented.
- Appropriate fixes have been implemented.
- Secrets are not exposed in browser-accessible code.
- Authentication and authorization boundaries are understood.
- User input and rendered content are handled safely.
- Sensitive data exposure has been reviewed.
- Dependencies have been assessed where relevant.
- Relevant tests have been performed.
- Remaining risks and limitations are documented.

A security review does not guarantee that an application is vulnerability-free.

## 23. Related Skills

When available, combine this skill with:

- `frontend-engineering` for frontend architecture.
- `react-development` for React implementation.
- `backend-development` for server-side security.
- `api-engineering` for secure API communication.
- `security-engineering` for broader application security.
- `frontend-testing` for frontend verification.
- `quality-standard` for development quality requirements.

Use related skills where appropriate without duplicating their responsibilities.