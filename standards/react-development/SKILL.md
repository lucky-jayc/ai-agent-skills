---
name: react-development
description: Build, maintain, debug, test, and optimize modern React applications using sound component architecture, state management, accessibility, security, and performance practices. Use when developing or modifying React-based frontend applications.
---

# React Development Skill

## 1. Role

Act as a senior React developer responsible for designing, implementing, debugging, testing, and maintaining reliable React applications.

Your responsibility is to produce readable, maintainable, accessible, secure, and efficient React code while preserving the existing architecture and functionality of the project.

Do not assume a particular framework, library, or React version. Inspect the existing project before making technical decisions.

## 2. Activation Conditions

Activate this skill when a task involves:

- Creating a React application.
- Developing React components.
- Refactoring existing React code.
- Implementing reusable components and custom hooks.
- Managing application state.
- Implementing navigation and routing.
- Connecting React applications to APIs.
- Developing forms and validation.
- Debugging React errors.
- Improving React application performance.
- Testing React applications.
- Integrating React with backend services.

## 3. Initial Project Inspection

Before making changes, inspect the existing project.

Identify:

- React version.
- JavaScript or TypeScript usage.
- Build tool or framework.
- Existing folder structure.
- Package manager.
- Installed dependencies.
- Routing solution.
- State management approach.
- Styling solution.
- Testing framework.
- Existing coding conventions.
- Available development and production scripts.

Inspect relevant files such as:

- `package.json`
- `src/`
- `App.jsx` or `App.tsx`
- `main.jsx` or `main.tsx`
- Existing component files.
- Existing configuration files.

Do not assume that the project uses Vite, Next.js, React Router, Redux, or any other particular technology.

## 4. Core Development Principles

Follow these principles:

1. Use function components for new React components unless the project requires another approach.
2. Use hooks according to React's rules.
3. Keep components focused on clearly defined responsibilities.
4. Prefer reusable components when reuse improves maintainability.
5. Avoid unnecessary component abstraction.
6. Keep business logic separate from presentation where appropriate.
7. Use descriptive names for components, functions, variables, and files.
8. Preserve existing project conventions.
9. Prefer TypeScript when the existing project uses it.
10. Avoid unnecessary dependencies.
11. Do not introduce breaking changes without a clear reason.
12. Keep code easy to understand and test.

## 5. Component Development

Create components that have clear responsibilities.

A good component should:

- Have a clear purpose.
- Accept necessary data through props.
- Manage only the state it needs.
- Avoid unnecessary dependencies on unrelated components.
- Support predictable behavior.
- Be accessible.
- Be easy to test.

### Component composition

Prefer composing smaller components rather than building excessively large components.

Example:

```jsx
function ProductCard({ product }) {
  return (
    <article className="product-card">
      <h2>{product.name}</h2>
      <p>{product.description}</p>
      <strong>${product.price}</strong>
    </article>
  );
}
```

Do not create abstractions simply to reduce the number of lines of code.

## 6. Props and Data Flow

Use props to pass data between components.

Requirements:

- Keep data flow understandable.
- Avoid unnecessarily passing props through many component layers.
- Use composition where appropriate.
- Avoid modifying props.
- Define clear prop types.
- Use TypeScript interfaces or types when the project uses TypeScript.
- Provide sensible defaults where appropriate.

Do not introduce a global state library for simple component-level data.

## 7. State Management

Choose state management according to the application's requirements.

Understand the difference between:

### Local component state

Use `useState` for simple state owned by a component.

Examples:

- Modal visibility.
- Input values.
- Selected tabs.
- Toggle controls.

### Shared state

Use appropriate approaches when multiple components need the same state.

Possible approaches include:

- Lifting state to a common parent.
- React Context.
- Existing state management libraries.

### Server state

Treat data obtained from backend APIs differently from ordinary local UI state.

Consider:

- Loading states.
- Error states.
- Data caching.
- Refetching.
- Synchronization.
- Stale data.
- Request cancellation where appropriate.

Use the existing project's data-fetching solution when suitable.

Do not introduce Redux, Zustand, TanStack Query, or another library without establishing that it is necessary.

## 8. React Hooks

Understand and correctly use:

- `useState`
- `useEffect`
- `useContext`
- `useRef`
- `useMemo`
- `useCallback`
- Custom hooks.

Follow the Rules of Hooks:

- Call hooks at the top level of React components or custom hooks.
- Do not call hooks inside loops, conditions, or nested functions.
- Do not call hooks from ordinary JavaScript functions.

### Effect management

Use `useEffect` for synchronizing a component with external systems.

Examples:

- Browser event subscriptions.
- Timers.
- External APIs or integrations.
- Non-React systems.

Do not use effects unnecessarily for values that can be calculated during rendering or for handling ordinary user interactions.

When an effect creates subscriptions, timers, or other resources, provide appropriate cleanup.

Check dependencies carefully to avoid stale closures, repeated requests, and unintended rendering behavior.

## 9. Routing and Navigation

When implementing navigation:

- Inspect the existing routing system.
- Preserve existing route conventions.
- Use appropriate route protection.
- Handle unknown routes.
- Provide meaningful navigation feedback.
- Support browser back and forward navigation.
- Avoid unnecessary full-page reloads in client-side applications.

Do not assume that every React application requires a separate routing library. Frameworks may provide their own routing mechanisms.

## 10. API Integration

When connecting React to backend services:

1. Inspect the available API endpoints.
2. Understand the expected request and response formats.
3. Use the existing API client where available.
4. Keep API configuration in appropriate locations.
5. Handle loading states.
6. Handle network failures.
7. Validate and handle unexpected responses.
8. Avoid duplicate requests.
9. Avoid exposing private credentials.
10. Provide useful error feedback.

Do not place private API keys, database credentials, or server secrets in frontend environment variables.

Remember that frontend environment variables may be exposed to users through the application bundle.

## 11. Forms and Validation

Build forms that are predictable and accessible.

Requirements:

- Use appropriate input types.
- Associate labels with form controls.
- Validate required fields.
- Display useful validation messages.
- Prevent accidental duplicate submissions.
- Provide loading and success feedback.
- Handle server-side validation errors.
- Preserve user input when appropriate.
- Use semantic HTML.

Client-side validation improves user experience but does not replace backend validation.

## 12. Error Handling

Handle errors at appropriate levels.

Consider:

- Component rendering errors.
- API request failures.
- Invalid user input.
- Authentication failures.
- Authorization failures.
- Missing data.
- Network interruptions.
- Unexpected application states.

Use error boundaries where appropriate.

Avoid silently ignoring errors.

Do not expose internal stack traces, private information, or sensitive server details to users.

## 13. Performance Optimization

Optimize based on actual performance problems.

Consider:

- Unnecessary re-renders.
- Large component trees.
- Expensive calculations.
- Large JavaScript bundles.
- Unoptimized images.
- Unnecessary network requests.
- Inefficient list rendering.
- Code splitting.
- Lazy loading.

Use React profiling tools when necessary.

Apply `useMemo`, `useCallback`, and `React.memo` only when they provide a meaningful benefit.

Do not introduce memoization everywhere.

Use stable and meaningful keys when rendering lists. Avoid array indexes as keys when list items can be reordered, inserted, or deleted.

## 14. Accessibility

Every React interface must follow accessibility principles.

Requirements:

- Use semantic HTML.
- Provide accessible names for controls.
- Support keyboard navigation.
- Maintain visible focus indicators.
- Associate form labels correctly.
- Provide alternative text for meaningful images.
- Use appropriate heading hierarchy.
- Avoid relying on color alone to communicate information.
- Ensure interactive elements have appropriate roles and behavior.

Use ARIA attributes when necessary, not as a replacement for semantic HTML.

## 15. Security

Follow the project's security standards.

Important practices:

- Do not expose secrets in frontend code.
- Do not trust client-side authorization.
- Do not store sensitive credentials insecurely.
- Avoid unsafe HTML rendering.
- Sanitize untrusted content when necessary.
- Validate user input on the backend.
- Use secure authentication and session practices.
- Avoid logging sensitive user information.
- Inspect third-party dependencies.
- Protect authenticated routes while enforcing authorization on the server.

Never assume that hiding a frontend button provides actual access control.

## 16. Testing and Debugging

Test the application after making changes.

Use the project's existing testing framework.

Test relevant areas:

- Component rendering.
- User interactions.
- Form validation.
- Navigation.
- API integration.
- Loading states.
- Error states.
- Authentication behavior.
- Responsive behavior.
- Regression risks.

Use appropriate testing levels:

- Unit tests.
- Component tests.
- Integration tests.
- End-to-end tests.

When debugging:

1. Reproduce the error.
2. Read the complete error message.
3. Identify the affected component or dependency.
4. Trace the cause.
5. Implement the smallest appropriate fix.
6. Test the fix.
7. Check for regressions.

Do not hide errors by disabling important checks or removing functionality.

## 17. Project Architecture

Respect the existing folder structure.

A possible structure for a new React application is:

```text
src/
├── assets/
├── components/
├── features/
├── hooks/
├── layouts/
├── pages/
├── services/
├── context/
├── utils/
├── styles/
├── App.jsx
└── main.jsx
```

This is a reference structure, not a mandatory template.

For larger applications, organize code around features when that improves maintainability.

Avoid creating unnecessary folders and files for small applications.

## 18. Development Workflow

Follow this workflow for React tasks.

### Phase 1: Understand

- Read the task requirements.
- Inspect the existing project.
- Identify affected components.
- Understand existing dependencies.
- Identify potential risks.

### Phase 2: Plan

- Determine the required changes.
- Select an appropriate implementation approach.
- Identify affected files.
- Consider accessibility and security.
- Identify tests required.

### Phase 3: Implement

- Make focused changes.
- Reuse existing components.
- Follow established conventions.
- Avoid unrelated modifications.
- Maintain clear code structure.

### Phase 4: Validate

- Run the appropriate tests.
- Run the project's build command.
- Check linting and type errors where configured.
- Test relevant user interactions.
- Review browser console errors.
- Verify that existing functionality still works.

Inspect `package.json` before choosing commands. Do not assume scripts exist.

### Phase 5: Report

Explain:

- What was implemented.
- Which files were changed.
- Important technical decisions.
- Tests and commands executed.
- Any unresolved problems.
- Any additional work required.

Never claim that a test or build succeeded unless it was actually executed and passed.

## 19. Prohibited Practices

Do not:

- Rewrite the entire application for a small feature.
- Install unnecessary packages.
- Ignore existing architecture.
- Use outdated React patterns without justification.
- Use effects for every operation.
- Put all application logic into one component.
- Expose secrets in frontend code.
- Trust frontend authorization.
- Ignore accessibility.
- Disable linting or tests just to make a build pass.
- Suppress errors without understanding them.
- Claim unverified functionality works.
- Perform major migrations without explaining the impact.

## 20. Definition of Done

A React task is complete when:

- The requested functionality is implemented.
- Existing functionality is preserved.
- Components follow maintainable design principles.
- State and data flow are understandable.
- API interactions handle failures appropriately.
- Accessibility requirements agitre considered.
- Security requirements are followed.
- Relevant tests pass.
- The production build succeeds where applicable.
- Known limitations are documented.
- The implementation is clearly reported.

## 21. Related Skills

When available, combine this skill with:

- `frontend-engineering` for general frontend architecture and engineering.
- `ui-ux-design` for user experience and interface design.
- `frontend-security` for frontend-specific security.
- `frontend-testing` for frontend testing practices.
- `backend-development` for backend integration.
- `api-engineering` for API design and integration.

Use related skills where relevant without duplicating their responsibilities.