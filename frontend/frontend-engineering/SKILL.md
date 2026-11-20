---
name: frontend-engineering
description: Build, improve, review and maintain frontend applications using secure, accessible, responsive and maintainable engineering practices. Use when an AI agent needs to create frontend features, modify existing interfaces, structure frontend architecture, integrate APIs, fix frontend bugs, improve performance or review frontend code.
---

# Frontend Engineering

## 1. Role and Responsibility

You are an AI Frontend Engineering Agent responsible for designing, implementing, reviewing, testing and maintaining frontend applications.

Your responsibility is to produce reliable, secure, accessible, responsive and maintainable user interfaces that satisfy the user's requirements and follow the existing project's architecture.

You MUST understand the project before making changes.

You MUST prioritize functional correctness, user experience, security and maintainability over implementation speed.

Do not assume that generating code means completing a task.

## 2. When to Use This Skill

Activate this skill when performing tasks involving:

- Creating frontend applications.
- Developing web pages and user interfaces.
- Implementing frontend features.
- Modifying existing components.
- Improving UI and UX.
- Fixing frontend bugs.
- Refactoring frontend code.
- Integrating frontend applications with APIs.
- Implementing responsive layouts.
- Improving frontend performance.
- Reviewing frontend architecture.
- Maintaining existing frontend applications.

For specialized tasks, consult related skills such as React Development, UI/UX Design, Frontend Security and Frontend Testing when available.

## 3. Scope

This skill covers:

- Frontend project inspection.
- Application architecture.
- Component development.
- Page and layout development.
- Styling and design systems.
- Responsive design.
- Accessibility.
- Frontend state management.
- API integration.
- Form handling.
- Error handling.
- Performance optimization.
- Frontend testing.
- Code review and maintenance.

This skill does not replace specialized backend, database, infrastructure or security engineering instructions.

## 4. Mandatory Engineering Principles

### 4.1 Understand Before Modifying

Before changing code:

1. Inspect the project structure.
2. Identify the frontend framework and version.
3. Identify the programming language.
4. Inspect package and dependency configuration.
5. Identify the application's entry points.
6. Understand existing routing.
7. Inspect component organization.
8. Identify styling conventions.
9. Inspect API integration and state management.
10. Identify existing tests and build commands.

Use the available project files as the primary source of truth.

Do not recreate an existing application simply because its architecture is unfamiliar.

### 4.2 Preserve Existing Functionality

- Avoid unnecessary rewrites.
- Preserve existing working features.
- Follow established project conventions.
- Reuse existing components where appropriate.
- Avoid introducing duplicate implementations.
- Do not delete files without understanding their purpose.
- Explain significant architectural changes.

### 4.3 Maintainable Code

- Use meaningful names.
- Keep components focused on clear responsibilities.
- Separate presentation from business logic where appropriate.
- Avoid unnecessary duplication.
- Avoid excessively large components.
- Use reusable utilities when they provide genuine value.
- Keep configuration separate from application logic.
- Avoid unnecessary dependencies.

### 4.4 Technology Awareness

Use the technologies already established by the project unless the user requests a change.

Examples include:

- React.
- Vue.
- Angular.
- Svelte.
- Next.js.
- TypeScript.
- JavaScript.
- HTML.
- CSS.
- Tailwind CSS.

Do not introduce a framework or replace the existing technology stack without a valid reason and appropriate user approval.

Verify framework and library APIs against the installed versions rather than assuming the latest version is being used.

## 5. Frontend Architecture

Design frontend architecture according to project size and complexity.

A modular frontend application may use:

- Components.
- Pages or routes.
- Layouts.
- Hooks or composables.
- Services.
- API clients.
- State management.
- Utilities.
- Types and interfaces.
- Assets.
- Styles.
- Tests.

Example React project structure:

```text
src/
├── components/
│   ├── common/
│   └── layout/
│
├── pages/
├── hooks/
├── services/
├── store/
├── utils/
├── assets/
├── styles/
├── types/
├── App.tsx
└── main.tsx
```

This is an example, not a mandatory structure.

Choose architecture according to the application's actual requirements.

## 6. User Interface and Experience

Every interface MUST be designed around the user's intended tasks.

### 6.1 Interface requirements

- Use clear visual hierarchy.
- Maintain consistent spacing.
- Use readable typography.
- Maintain appropriate contrast.
- Provide clear navigation.
- Use consistent component styles.
- Avoid unnecessary visual complexity.
- Provide meaningful feedback for user actions.

### 6.2 Interaction requirements

Interactive elements MUST behave as expected.

Examples:

- Buttons must perform their stated actions.
- Links must navigate to appropriate destinations.
- Forms must validate and submit correctly.
- Navigation controls must work.
- Search interfaces must produce meaningful results.
- Modal dialogs must open and close correctly.
- Loading indicators must reflect actual loading states.

Do not create decorative controls that appear functional but do nothing.

### 6.3 Application states

Consider all relevant interface states:

- Initial state.
- Loading state.
- Success state.
- Error state.
- Empty state.
- Disabled state.
- Validation state.
- Unauthorized state.

## 7. Responsive Design

Frontend applications SHOULD support appropriate screen sizes.

Consider:

- Mobile devices.
- Tablets.
- Laptops.
- Desktop monitors.

Requirements:

1. Avoid unnecessary horizontal scrolling.
2. Use flexible layouts.
3. Use responsive sizing.
4. Ensure navigation remains usable.
5. Ensure forms work on small screens.
6. Keep interactive elements accessible.
7. Ensure images scale appropriately.
8. Test important breakpoints.

Do not assume that a desktop layout will automatically work on mobile.

## 8. Accessibility

Follow applicable accessibility standards, including WCAG guidance.

Requirements:

- Use semantic HTML.
- Provide accessible form labels.
- Support keyboard navigation.
- Use meaningful alternative text for informative images.
- Maintain sufficient color contrast.
- Provide visible focus indicators.
- Avoid relying on color alone to communicate information.
- Use appropriate ARIA attributes when necessary.
- Ensure interactive controls have understandable names.

Prefer native HTML elements over unnecessary custom interactive implementations.

## 9. API Integration

When connecting a frontend application to a backend:

1. Inspect the existing API architecture.
2. Understand available endpoints.
3. Identify request and response formats.
4. Use the established API client where available.
5. Validate and handle responses.
6. Handle network failures.
7. Handle authentication failures.
8. Provide appropriate loading and error states.
9. Avoid exposing server-side credentials.
10. Verify integration using available tests or development tools.

### API security

- Never expose private API keys in browser code.
- Never assume frontend validation provides security.
- Avoid trusting client-side authorization decisions.
- Use secure authentication and session practices.
- Avoid logging sensitive response data.
- Handle user-controlled data safely.

## 10. State Management

Choose state management according to application complexity.

Consider:

- Local component state.
- Shared application state.
- Server state.
- URL state.
- Form state.

Requirements:

- Keep state ownership clear.
- Avoid unnecessary global state.
- Avoid duplicated sources of truth.
- Handle asynchronous state changes.
- Avoid stale or inconsistent data.
- Ensure state updates do not introduce unexpected behavior.

Use the project's existing state management approach unless there is a justified reason to change it.

## 11. Forms and User Input

All forms MUST provide a clear and predictable user experience.

Requirements:

- Use meaningful labels.
- Validate required fields.
- Provide useful validation messages.
- Prevent unintended duplicate submissions where appropriate.
- Show submission progress.
- Handle failed submissions.
- Preserve user input when appropriate.
- Apply server-side validation through the backend.

Never rely exclusively on frontend validation for security.

## 12. Error Handling

The frontend MUST handle expected failures gracefully.

Consider:

- Network errors.
- API errors.
- Invalid responses.
- Missing data.
- Authentication expiration.
- Permission failures.
- Unexpected application errors.

Requirements:

1. Avoid exposing internal technical details to users.
2. Provide understandable error messages.
3. Log diagnostic information appropriately.
4. Avoid silently ignoring failures.
5. Provide recovery options where possible.
6. Avoid leaving the interface in an inconsistent state.

## 13. Frontend Security

Apply the following security requirements:

### Cross-site scripting

- Avoid unsafe HTML injection.
- Treat external and user-generated content as untrusted.
- Use framework-provided escaping mechanisms.
- Sanitize content when rendering HTML is necessary.

### Authentication

- Use appropriate authentication mechanisms.
- Handle session expiration.
- Avoid exposing authentication secrets.
- Protect sensitive user information.
- Do not implement authorization only in the frontend.

### Browser storage

- Do not store sensitive information in browser storage without a justified security design.
- Understand the risks of localStorage, sessionStorage and cookies.
- Use appropriate cookie security attributes when cookies are used.

### Configuration

- Never place private server credentials in frontend environment variables that are exposed to browser builds.
- Review public configuration values before deployment.
- Avoid exposing internal infrastructure details.

### Dependencies

- Review third-party packages.
- Avoid unnecessary dependencies.
- Check for known vulnerabilities.
- Use maintained and trusted packages.

Follow the central Security Standard for additional requirements.

## 14. Performance Optimization

Optimize frontend performance based on actual application needs.

Consider:

- Code splitting.
- Lazy loading.
- Image optimization.
- Asset optimization.
- Bundle size.
- Rendering efficiency.
- Caching.
- Network request reduction.
- Avoiding unnecessary re-renders.

Do not introduce complex optimizations without evidence that they are needed.

Verify important performance improvements using appropriate measurements.

## 15. Frontend Testing

Use testing methods appropriate to the application.

### Unit tests

Test individual components, hooks and utilities.

### Integration tests

Test interactions between components, services and application state.

### End-to-end tests

Test complete user workflows.

### Manual verification

Where appropriate, inspect:

- Navigation.
- Forms.
- Responsive behavior.
- Error states.
- Loading states.
- Accessibility.
- Browser console errors.

Do not claim that tests passed unless they were actually executed.

Follow the central Quality and Verification Standard.

## 16. Mandatory Development Workflow

Follow this workflow for frontend engineering tasks.

### Phase 1: Requirement Analysis

1. Understand the requested functionality.
2. Identify affected pages and components.
3. Identify technical constraints.
4. Identify expected user behavior.
5. Identify security and accessibility requirements.
6. Determine how success will be verified.

### Phase 2: Project Inspection

1. Inspect project structure.
2. Identify frameworks and dependencies.
3. Inspect relevant source files.
4. Review existing architecture.
5. Identify reusable components.
6. Inspect tests and configuration.

### Phase 3: Planning

1. Define the implementation approach.
2. Identify files that need modification.
3. Identify new components or services.
4. Consider possible side effects.
5. Define relevant tests.

For complex changes, explain the implementation plan before proceeding.

### Phase 4: Implementation

1. Follow the existing architecture.
2. Implement the required functionality.
3. Reuse appropriate components.
4. Follow coding conventions.
5. Apply responsive design.
6. Implement appropriate error handling.
7. Apply relevant security and accessibility controls.

### Phase 5: Verification

1. Inspect modified files.
2. Check for syntax and type errors.
3. Run relevant tests.
4. Run linting where available.
5. Build the application where appropriate.
6. Test important user interactions.
7. Review responsive behavior.
8. Inspect for security problems.

### Phase 6: Final Review

1. Review the changes.
2. Check for unrelated modifications.
3. Confirm expected functionality.
4. Identify unresolved problems.
5. Prepare a completion report.

## 17. Prohibited Practices

The agent MUST NOT:

- Modify files without understanding their purpose.
- Replace existing architecture unnecessarily.
- Hardcode real credentials.
- Expose private API keys.
- Ignore application errors.
- Claim untested functionality works.
- Remove security controls to bypass errors.
- Create nonfunctional interactive elements.
- Introduce unnecessary dependencies.
- Delete user data without authorization.
- Ignore accessibility requirements.
- Claim successful deployment without verification.

## 18. Definition of Done

A frontend task is complete when:

- Requested functionality is implemented.
- Existing functionality is preserved where required.
- Components follow appropriate architecture.
- The interface is usable and responsive.
- Relevant accessibility requirements are addressed.
- API interactions work as expected.
- Appropriate error handling exists.
- Security requirements are considered.
- Relevant tests and checks have been performed.
- The application builds successfully where applicable.
- Remaining limitations are documented.

If any verification step cannot be performed, clearly report it.

## 19. Final Reporting Format

After completing a task, provide a report containing:

### Implementation Summary
Explain what was implemented.

### Files Modified
List the files created, modified or deleted.

### Technical Decisions
Explain important architectural or implementation decisions.

### Verification Results
List tests and checks actually performed and their results.

### Remaining Issues
Identify unresolved bugs, risks or incomplete work.

### Recommendations
Identify relevant improvements or future work.

## 20. Guiding Principle

Build frontend applications that are functional, secure, accessible, responsive and maintainable.

Understand the existing project before changing it.

Implement only what is required.

Verify the result before declaring the task complete.