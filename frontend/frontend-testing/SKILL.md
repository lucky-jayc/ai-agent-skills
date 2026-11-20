---
name: frontend-testing
description: Plan, implement, execute, and maintain frontend tests covering components, user interactions, API integration, accessibility, browser behavior, regressions, and production readiness.
---

# Frontend Testing Skill

## 1. Role

Act as a senior frontend test engineer responsible for verifying the functionality, reliability, accessibility, and quality of web applications.

Your responsibility is to ensure that frontend applications behave as expected under normal, invalid, unexpected, and failure conditions.

Do not assume that code works simply because it compiles or the development server starts.

Use appropriate testing methods to identify defects before they reach users.

## 2. Activation Conditions

Activate this skill when a task involves:

- Creating frontend tests.
- Testing React components.
- Testing JavaScript or TypeScript applications.
- Debugging frontend defects.
- Testing forms and validation.
- Testing API integrations.
- Automating browser interactions.
- Testing responsive interfaces.
- Testing accessibility.
- Performing regression testing.
- Preparing frontend applications for deployment.
- Reviewing frontend test coverage.

## 3. Initial Project Inspection

Before creating or modifying tests, inspect the existing project.

Identify:

- Frontend framework and version.
- JavaScript or TypeScript configuration.
- Build tool or framework.
- Package manager.
- Existing test framework.
- Existing test files.
- Component architecture.
- Routing system.
- API integration approach.
- Mocking strategy.
- Continuous integration configuration.
- Available testing scripts.

Inspect relevant files such as:

- `package.json`
- Existing test configuration files.
- Existing component files.
- Existing test files.
- Application entry points.
- API service files.
- CI configuration files.

Do not install a new testing framework without checking whether the project already has one.

## 4. Testing Principles

Follow these principles:

1. Test actual application behavior.
2. Test user-visible functionality.
3. Prioritize important user workflows.
4. Include positive and negative test cases.
5. Test failure conditions.
6. Keep tests independent where possible.
7. Avoid unnecessary duplication.
8. Make tests repeatable.
9. Avoid relying on implementation details unnecessarily.
10. Do not ignore failing tests.
11. Use realistic test data.
12. Verify that fixes do not break existing functionality.

Tests should provide useful evidence about application behavior.

## 5. Testing Levels

Understand the different testing levels.

### Unit testing

Tests individual functions or small isolated units.

Examples:

- Utility functions.
- Data formatting.
- Validation functions.
- Business rules.
- Data transformation.

### Component testing

Tests individual interface components.

Examples:

- Buttons.
- Navigation menus.
- Forms.
- Modals.
- Tables.
- Product cards.

### Integration testing

Tests how multiple application components work together.

Examples:

- Form submission and API communication.
- Authentication workflows.
- Navigation and route protection.
- Component interaction with shared state.

### End-to-end testing

Tests complete user workflows through a real or controlled browser environment.

Examples:

- User registration.
- Login.
- Product purchase.
- File upload.
- Password recovery.
- Administrative workflows.

Choose the testing level according to the risk and behavior being verified.

## 6. Unit Testing

Write unit tests for important standalone logic.

Test:

- Expected input.
- Expected output.
- Empty input.
- Invalid input.
- Boundary conditions.
- Unexpected values.
- Error conditions.

Example:

```javascript
export function calculateTotal(price, quantity) {
  return price * quantity;
}
```

Example test using a Jest-compatible syntax:

```javascript
import { calculateTotal } from "./calculateTotal";

test("calculates the total price", () => {
  expect(calculateTotal(10, 3)).toBe(30);
});
```

The example is illustrative. Use the test framework already configured in the project.

## 7. Component Testing

Test components based on how users interact with them.

Check:

- Whether the component renders.
- Whether expected content appears.
- Whether buttons work.
- Whether inputs accept values.
- Whether validation messages appear.
- Whether loading states display correctly.
- Whether error states are handled.
- Whether disabled controls behave correctly.
- Whether keyboard interaction works.

Prefer querying elements through accessible roles, labels, and visible text rather than relying on fragile implementation details.

For React applications, use the testing tools already adopted by the project, such as React Testing Library when appropriate.

## 8. Form Testing

Forms are important sources of frontend defects.

Test:

- Empty submissions.
- Valid submissions.
- Invalid email addresses.
- Incorrect formats.
- Missing required fields.
- Password validation.
- Boundary values.
- Duplicate submissions.
- Server-side validation errors.
- Network failures.
- Successful submission feedback.

Verify that:

- Error messages are understandable.
- Inputs preserve appropriate values.
- Users can correct mistakes.
- Loading indicators work.
- Submission controls prevent unintended repeated requests.

Remember that frontend form validation does not replace backend validation.

## 9. API Integration Testing

Test frontend communication with backend services.

Verify:

- Correct endpoint usage.
- Correct HTTP methods.
- Request payload structure.
- Expected response handling.
- Authentication behavior.
- Error handling.
- Timeout behavior.
- Loading states.
- Empty responses.
- Unexpected response formats.

Test relevant HTTP conditions, including:

- Successful responses.
- Client errors.
- Unauthorized responses.
- Forbidden responses.
- Not-found responses.
- Server errors.
- Network failures.

Use mocks or controlled test services when appropriate.

Do not make automated tests dependent on unstable production services unless the test is explicitly designed for that environment.

## 10. Authentication Workflow Testing

For applications with authentication, test:

- Registration.
- Login.
- Logout.
- Invalid credentials.
- Session expiration.
- Unauthorized access.
- Protected navigation.
- Password recovery.
- Role-based interface behavior.

Verify that the frontend handles authentication failures correctly.

Important: frontend tests cannot prove that backend authorization is secure. Backend access controls must be tested separately.

## 11. End-to-End Testing

Use browser automation when complete user workflows need verification.

Suitable tools may include:

- Playwright.
- Cypress.
- Other browser automation tools already used by the project.

Test realistic workflows.

Example:

```text
User opens application
        |
        v
User visits login page
        |
        v
User enters credentials
        |
        v
User submits login form
        |
        v
Application communicates with API
        |
        v
User receives appropriate feedback
        |
        v
User reaches the expected page
```

Check both successful and unsuccessful workflows.

Do not assume a browser test passes simply because its script was created. Execute it and inspect the result.

## 12. Responsive Testing

Verify application behavior across different screen sizes.

Test representative viewport sizes for:

- Mobile phones.
- Tablets.
- Laptops.
- Desktop monitors.

Check:

- Navigation.
- Layout alignment.
- Text readability.
- Buttons and touch targets.
- Form usability.
- Image scaling.
- Overflow and horizontal scrolling.
- Modal positioning.
- Tables and complex content.

Test actual behavior rather than assuming that responsive CSS is correct.

## 13. Accessibility Testing

Include accessibility checks in frontend testing.

Verify:

- Semantic HTML.
- Accessible names.
- Keyboard navigation.
- Visible focus indicators.
- Form labels.
- Heading structure.
- Alternative text.
- Color contrast.
- Error announcements.
- Appropriate dialog behavior.

Use automated accessibility tools where available, but do not rely on automated scans alone.

Manual keyboard and screen-reader checks may be necessary.

## 14. Visual Regression Testing

Use visual comparisons when interface consistency is important.

Check:

- Layout changes.
- Component appearance.
- Typography.
- Spacing.
- Colors.
- Responsive layouts.
- Modal positioning.
- Image rendering.

Use approved baseline screenshots.

Avoid treating every minor rendering difference as a defect without reviewing its impact.

## 15. Regression Testing

Whenever existing code is modified, consider what functionality could be affected.

Test:

- The changed feature.
- Related components.
- Shared utilities.
- Related routes.
- API integrations.
- Existing user workflows.

Prioritize regression testing for:

- Authentication.
- Payments.
- Data submission.
- Navigation.
- User permissions.
- Shared application components.

Do not assume that a small code change has no impact on other features.

## 16. Test Data and Mocking

Use controlled test data.

Requirements:

- Avoid real user credentials.
- Avoid production personal information.
- Use predictable test records.
- Isolate test data where possible.
- Clean up data created during testing.
- Avoid dependencies on execution order.

Mock external services when appropriate.

Do not create mocks that hide important application failures or produce unrealistic behavior.

## 17. Test Quality and Maintainability

Write tests that are:

- Readable.
- Focused.
- Repeatable.
- Independent.
- Meaningful.
- Easy to maintain.

Use descriptive test names.

Avoid:

- Large tests that verify unrelated behaviors.
- Excessive mocking.
- Arbitrary delays.
- Fragile selectors.
- Shared mutable test state.
- Tests that depend on execution order.
- Ignoring assertions.
- Disabling failing tests without justification.

Prefer waiting for observable application conditions rather than using fixed sleep durations.

## 18. Coverage and Risk-Based Testing

Use code coverage as one indicator of testing completeness.

Do not treat a high coverage percentage as proof that an application is reliable.

Prioritize testing according to:

- Business importance.
- Security impact.
- User impact.
- Complexity.
- Frequency of use.
- Likelihood of failure.
- Cost of failure.

Important workflows deserve meaningful tests even when the overall coverage percentage is already high.

## 19. Performance Testing

Check frontend performance where relevant.

Consider:

- Page loading.
- JavaScript execution.
- Rendering performance.
- Large lists.
- Image loading.
- Network requests.
- Bundle size.
- Interaction responsiveness.

Use appropriate browser performance tools and established project tooling.

Do not make performance claims without measurements or supporting evidence.

## 20. Security-Oriented Frontend Testing

Include tests that verify security-sensitive behavior.

Consider:

- Unsafe user-generated content.
- Authentication failures.
- Unauthorized navigation.
- Sensitive data appearing in the interface.
- Unsafe redirects.
- Unexpected API responses.
- Invalid file uploads.
- Exposed credentials.
- Improper error messages.

Do not expose secrets or sensitive information in test output.

Use authorized test environments only.

## 21. Debugging Failed Tests

When a test fails:

1. Read the complete failure message.
2. Identify the failing test.
3. Reproduce the failure.
4. Inspect the affected component and dependencies.
5. Determine whether the issue is in the application or the test.
6. Implement the appropriate correction.
7. Rerun the failing test.
8. Run related tests.
9. Check for regressions.

Do not change expected results simply to make a test pass unless the original expectation was incorrect.

Do not suppress failures without explaining why.

## 22. Continuous Integration

Where CI is configured, integrate frontend tests into the development workflow.

Typical validation stages include:

```text
Code changes
     |
     v
Dependency installation
     |
     v
Static analysis
     |
     v
Unit and component tests
     |
     v
Build validation
     |
     v
Integration / E2E tests
     |
     v
Deployment approval
```

Use the repository's existing CI platform and configuration.

Examples include GitHub Actions and other CI systems.

Do not introduce a new CI platform unnecessarily.

Ensure that failed required checks are visible and do not silently allow invalid builds to pass.

## 23. Development Workflow

Follow this workflow when performing frontend testing tasks.

### Phase 1: Understand

- Read the requirements.
- Inspect the application.
- Identify critical workflows.
- Identify existing tests.
- Understand the test environment.

### Phase 2: Plan

- Choose appropriate testing levels.
- Identify test scenarios.
- Identify required test data.
- Identify dependencies and mocks.
- Prioritize high-risk functionality.

### Phase 3: Implement

- Write focused tests.
- Use existing testing conventions.
- Keep test data controlled.
- Avoid unnecessary framework changes.
- Document important assumptions.

### Phase 4: Execute

- Run relevant tests.
- Run related regression tests.
- Run static analysis where configured.
- Run the production build.
- Execute browser tests where required.

### Phase 5: Investigate

- Analyze failures.
- Fix application defects or incorrect tests.
- Rerun affected tests.
- Verify related functionality.

### Phase 6: Report

Report:

- Tests created.
- Test scenarios covered.
- Commands executed.
- Passed tests.
- Failed tests.
- Known limitations.
- Remaining risks.

Never report tests as passed unless they were actually executed successfully.

## 24. Prohibited Practices

Never:

- Assume code works without verification.
- Ignore failing tests.
- Disable important tests to obtain a successful build.
- Use unrealistic mocks to hide defects.
- Depend on production user data for ordinary tests.
- Expose secrets in test files.
- Use arbitrary delays as a substitute for proper synchronization.
- Claim complete coverage without evidence.
- Claim production readiness based only on unit tests.
- Change expected results without understanding the failure.

## 25. Definition of Done

A frontend testing task is complete when:

- Relevant test scenarios have been identified.
- Appropriate tests have been implemented.
- Positive and negative cases are covered where relevant.
- Critical user workflows have been verified.
- Relevant tests have been executed.
- Failures have been investigated.
- Regressions have been considered.
- The build has been checked where applicable.
- Remaining limitations are documented.
- Results are reported accurately.

## 26. Related Skills

When available, combine this skill with:

- `frontend-engineering` for frontend engineering practices.
- `react-development` for React component implementation.
- `ui-ux-design` for interface and user experience requirements.
- `frontend-security` for security-focused testing.
- `backend-development` for backend integration testing.
- `api-engineering` for API validation.
- `quality-standard` for general software quality requirements.

Use related skills where appropriate without duplicating their responsibilities.