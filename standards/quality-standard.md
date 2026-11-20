# AI Agent Skills Library — Quality and Verification Standard

**Version:** 1.0  
**Status:** Active  
**Scope:** All skills and software engineering workflows in this library.

## 1. Purpose

This standard defines the quality requirements AI agents must follow when creating, modifying, reviewing, testing and maintaining software.

Its purpose is to ensure that AI-generated implementations are:

- Functional.
- Reliable.
- Maintainable.
- Secure.
- Testable.
- Understandable.
- Consistent with existing project requirements.

An implementation MUST NOT be considered complete merely because code has been generated or files have been modified.

The agent must verify the result using appropriate checks.

## 2. Core Quality Principles

### 2.1 Correctness

- Implement the requested functionality.
- Follow documented requirements.
- Preserve existing behavior unless a change is requested.
- Handle expected and unexpected conditions.
- Avoid implementing assumptions as confirmed requirements.

### 2.2 Maintainability

- Use clear naming conventions.
- Organize code logically.
- Avoid unnecessary complexity.
- Prefer reusable components and functions where appropriate.
- Follow established project conventions.
- Document non-obvious decisions.

### 2.3 Reliability

- Handle errors appropriately.
- Validate inputs.
- Avoid unexpected application crashes.
- Consider edge cases.
- Protect data integrity.
- Avoid introducing unnecessary dependencies or failure points.

### 2.4 Performance

- Avoid unnecessary processing.
- Consider memory and resource consumption.
- Avoid inefficient database queries.
- Use caching only where appropriate.
- Avoid premature optimization.
- Measure performance when performance claims matter.

### 2.5 Consistency

- Follow existing architecture and coding conventions.
- Maintain consistent formatting.
- Use established error-handling patterns.
- Keep API contracts and data structures consistent.
- Avoid introducing conflicting design patterns without justification.

## 3. Mandatory Project Inspection

Before modifying an existing project, the AI agent MUST inspect relevant project context.

Depending on the task, inspection SHOULD include:

### Project structure
- Main source directories.
- Existing modules and components.
- Configuration files.
- Documentation.
- Existing architecture.

### Development environment
- Programming languages.
- Frameworks.
- Runtime versions.
- Build tools.
- Package managers.

### Existing implementation
- Related source files.
- Reusable functions and components.
- Existing services.
- API contracts.
- Database structures.

### Existing verification
- Unit tests.
- Integration tests.
- End-to-end tests.
- Build scripts.
- Linting and formatting configuration.

The agent MUST NOT assume a project uses a particular technology or architecture without checking available evidence.

## 4. Requirements Analysis

Before implementation, the agent SHOULD:

1. Identify the requested outcome.
2. Identify functional requirements.
3. Identify non-functional requirements.
4. Identify affected project components.
5. Identify dependencies and constraints.
6. Identify potential security and reliability risks.
7. Determine how success will be verified.

If a missing requirement materially affects implementation correctness, the agent SHOULD ask for clarification rather than inventing a requirement.

## 5. Implementation Quality

### 5.1 Code organization

- Keep responsibilities separated.
- Avoid unnecessarily large functions and classes.
- Use appropriate abstractions.
- Avoid duplicated logic where reuse improves maintainability.
- Avoid creating abstractions that add complexity without value.

### 5.2 Naming

Names SHOULD clearly communicate their purpose.

Avoid:
- Unclear abbreviations.
- Misleading names.
- Generic names that hide functionality.
- Inconsistent naming conventions.

### 5.3 Error handling

- Handle expected failures explicitly.
- Return appropriate error information.
- Avoid silently ignoring errors.
- Preserve useful diagnostic information.
- Do not expose confidential information through errors.
- Avoid using broad exception handling as a substitute for understanding failures.

### 5.4 Configuration

- Keep environment-specific settings outside ordinary source code where appropriate.
- Avoid hardcoding deployment-specific values.
- Document required configuration.
- Provide safe example configurations.

### 5.5 Documentation

Document:
- Important architectural decisions.
- Complex business logic.
- Public interfaces.
- Configuration requirements.
- Setup and execution procedures.
- Known limitations.

Documentation SHOULD explain why important decisions exist, not merely repeat what the code does.

## 6. Testing Requirements

Agents MUST select testing methods appropriate to the task.

### 6.1 Unit testing

Verify individual functions, classes or components independently.

Examples:
- Input validation.
- Calculation logic.
- Utility functions.
- Business rules.

### 6.2 Integration testing

Verify that connected application components work together.

Examples:
- API and database interaction.
- Authentication services.
- External service integrations.
- Backend and frontend communication.

### 6.3 End-to-end testing

Verify complete user workflows.

Examples:
- User registration.
- Login.
- Form submission.
- Payment workflows.
- Data retrieval.
- Administrative operations.

### 6.4 Regression testing

Verify that new changes have not broken previously working functionality.

### 6.5 Negative testing

Test invalid inputs, unauthorized access, missing data, unavailable services and other failure conditions.

### 6.6 Testing discipline

Agents MUST:
- Use existing test infrastructure where appropriate.
- Add tests for important new behavior.
- Avoid changing tests merely to hide implementation failures.
- Report failed tests honestly.
- Avoid claiming tests passed when they were not executed.

Not every task requires every testing category. The selected tests should match the implementation's risk and complexity.

## 7. Build and Static Validation

Where supported by the project, agents SHOULD execute appropriate validation commands.

Examples include:

### JavaScript and TypeScript
```bash
npm run lint
npm run test
npm run build
```

### Java and Spring Boot
```bash
./mvnw test
./mvnw verify
```

### Python
```bash
python -m pytest
```

### General Git review
```bash
git status
git diff --check
git diff
```

These are examples, not universal commands. Agents MUST inspect the actual project scripts and tooling before selecting commands.

On Windows, equivalent platform-specific commands or project wrappers MAY be used.

## 8. Change Management

Before making changes, agents SHOULD:

1. Identify the files that need modification.
2. Understand their dependencies.
3. Avoid unrelated modifications.
4. Consider backward compatibility.
5. Identify potentially destructive changes.

After implementation, agents SHOULD:

1. Review modified files.
2. Inspect the Git diff where available.
3. Check for accidental changes.
4. Verify that required files are present.
5. Check that configuration remains valid.
6. Run relevant tests.

Agents MUST NOT overwrite user work without appropriate authorization.

## 9. Dependency Management

When introducing or updating dependencies:

- Confirm that the dependency is needed.
- Review its compatibility.
- Consider maintenance and security status.
- Avoid unnecessary packages.
- Use the project's package manager.
- Update lockfiles where appropriate.
- Verify that the project still builds and tests.

Agents SHOULD explain significant dependency changes.

## 10. User Interface Quality

For frontend and UI-related skills, agents SHOULD verify:

- Responsive behavior.
- Accessibility.
- Keyboard navigation.
- Form validation.
- Loading states.
- Error states.
- Empty states.
- Visual consistency.
- Browser compatibility where required.
- Appropriate mobile and desktop layouts.

An interface MUST NOT be considered complete simply because it renders without errors.

## 11. API and Backend Quality

For backend and API skills, agents SHOULD verify:

- Request validation.
- Response consistency.
- Appropriate HTTP status codes.
- Authentication and authorization.
- Error handling.
- Database interactions.
- Pagination where required.
- Rate limiting where appropriate.
- Logging and monitoring.
- Compatibility with documented API contracts.

## 12. Database Quality

For database engineering skills, agents SHOULD verify:

- Data types.
- Primary keys.
- Foreign keys.
- Constraints.
- Relationships.
- Indexes.
- Transaction behavior.
- Migration safety.
- Data integrity.
- Backup and recovery considerations.

Destructive migrations MUST receive appropriate review and authorization.

## 13. Performance and Scalability

Agents SHOULD consider:

- Application response times.
- Database query efficiency.
- Network requests.
- Memory usage.
- Concurrency.
- Resource limits.
- Caching strategies.
- Expected user and data growth.

Performance claims MUST be supported by measurements or clearly identified as estimates.

## 14. Deployment Verification

Before reporting a deployment as successful, agents MUST verify the available deployment evidence.

Depending on the environment, checks SHOULD include:

- Build success.
- Deployment status.
- Application startup.
- Service availability.
- Health checks.
- Database connectivity.
- Critical user workflows.
- Environment configuration.
- Error logs.

A successful build does not automatically prove that production deployment is successful.

A successful deployment does not automatically prove that every application feature works correctly.

## 15. Completion Reporting

Every completed task SHOULD include a concise report.

The report SHOULD contain:

### Summary
What was implemented or changed.

### Files changed
Which files were created, modified or deleted.

### Verification
Which tests and checks were actually executed.

### Results
Which checks passed and which failed.

### Limitations
Any incomplete work, unresolved issues or unverified assumptions.

### Next steps
Any important remaining work.

Agents MUST distinguish between:

- Completed and verified.
- Completed but not fully verified.
- Partially completed.
- Blocked.
- Not completed.

## 16. Quality Review Checklist

Before completing a task:

- [ ] Requirements have been understood.
- [ ] Relevant project files have been inspected.
- [ ] Existing conventions have been followed.
- [ ] Changes are limited to the required scope.
- [ ] Code is understandable and maintainable.
- [ ] Error handling is appropriate.
- [ ] Security requirements have been considered.
- [ ] Relevant tests have been added or updated.
- [ ] Appropriate tests have been executed.
- [ ] Build and validation checks have been considered.
- [ ] Changes have been reviewed.
- [ ] Remaining limitations have been documented.
- [ ] Completion status is reported honestly.

## 17. Definition of Done

A task is ready to be reported as complete when:

1. The requested requirements have been implemented.
2. Relevant code and configuration have been reviewed.
3. Appropriate tests and validation checks have been performed.
4. Critical failures have been resolved or explicitly reported.
5. Security requirements have been considered.
6. No known unintended changes remain.
7. The final report accurately reflects the verification performed.

If a task cannot be fully verified, the agent MUST clearly state what remains unverified.

## 18. Guiding Principle

The quality of AI-generated software is determined not by how much code an agent produces, but by whether the resulting implementation is correct, secure, maintainable and verifiably fit for its intended purpose.