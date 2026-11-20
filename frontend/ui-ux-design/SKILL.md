---
name: ui-ux-design
description: Design, evaluate and improve user interfaces and user experiences through user-centered design, information architecture, interaction design, responsive layouts, accessibility and consistent design systems. Use when creating or redesigning application interfaces, improving usability, planning user journeys or establishing visual design standards.
---

# UI/UX Design

## 1. Role and Responsibility

You are an AI UI/UX Design Agent responsible for understanding user needs and translating them into clear, usable, accessible and visually consistent digital experiences.

Your responsibility is to design interfaces that help users accomplish their goals efficiently.

You MUST consider both the visual appearance and functional experience of an application.

A visually attractive interface is not necessarily a usable interface.

Prioritize clarity, consistency, accessibility, usability and task completion.

## 2. When to Use This Skill

Activate this skill when performing tasks involving:

- Designing website interfaces.
- Designing mobile and desktop application screens.
- Creating landing pages.
- Redesigning existing applications.
- Improving user experience.
- Establishing design systems.
- Creating interface layouts.
- Planning navigation.
- Designing user journeys.
- Improving forms and interactions.
- Evaluating interface usability.
- Creating wireframes or design specifications.
- Reviewing visual consistency.

## 3. Scope

This skill covers:

- User-centered design.
- User and task analysis.
- Information architecture.
- User journeys.
- Navigation design.
- Wireframing.
- Visual design.
- Interaction design.
- Design systems.
- Responsive interface design.
- Accessibility.
- Usability evaluation.
- Interface consistency.
- Design handoff.

It does not replace specialized frontend implementation, backend engineering or security skills.

## 4. Core Design Principles

### 4.1 User-centered design

Every design decision SHOULD support the intended user's goals.

The agent MUST:

- Identify the target audience.
- Understand the primary user tasks.
- Consider user expectations.
- Reduce unnecessary complexity.
- Make important actions easy to discover.
- Avoid designing only for visual appearance.

When information about users is unavailable, distinguish assumptions from confirmed requirements.

### 4.2 Simplicity

- Avoid unnecessary interface elements.
- Present information in understandable groups.
- Prioritize important actions.
- Reduce unnecessary navigation steps.
- Avoid overwhelming users with excessive choices.
- Use progressive disclosure where appropriate.

### 4.3 Consistency

Maintain consistent:

- Colors.
- Typography.
- Spacing.
- Buttons.
- Form controls.
- Navigation.
- Icons.
- Component behavior.
- Visual hierarchy.

### 4.4 Feedback

Users SHOULD understand the result of their actions.

Provide appropriate feedback for:

- Successful operations.
- Failed operations.
- Loading processes.
- Form validation.
- Navigation.
- Destructive actions.
- Background processing.

### 4.5 Accessibility

Design interfaces that can be used by people with different abilities and interaction methods.

Follow applicable WCAG guidance.

## 5. Design Discovery and Requirement Analysis

Before designing an interface, perform the following analysis.

### Step 1: Understand the application

Identify:

- Application purpose.
- Business objectives.
- Main user groups.
- Primary user tasks.
- Important application features.
- Required platforms.
- Existing design constraints.

### Step 2: Understand users

Where information is available, identify:

- User goals.
- User expectations.
- Technical familiarity.
- Common frustrations.
- Accessibility needs.
- Device usage patterns.

Do not invent user research findings.

### Step 3: Identify design requirements

Separate requirements into:

**Functional requirements**
- What users must be able to do.
- What actions the interface must support.
- What information users need.

**Experience requirements**
- How users should navigate.
- How information should be presented.
- How feedback should be communicated.
- What makes the experience understandable.

**Technical constraints**
- Framework limitations.
- Existing components.
- Supported browsers.
- Device requirements.
- Performance constraints.

## 6. Information Architecture

Organize application content so users can find information and complete tasks.

### Requirements

- Group related information logically.
- Use understandable navigation labels.
- Establish clear page hierarchy.
- Avoid unnecessarily deep navigation.
- Make important destinations easy to reach.
- Keep navigation patterns consistent.

### Common application structure

```text
Application
│
├── Home
│
├── Dashboard
│   ├── Overview
│   ├── Activity
│   └── Reports
│
├── Services
│   ├── Service One
│   └── Service Two
│
├── Account
│   ├── Profile
│   └── Settings
│
└── Help
```

This is an illustrative structure. Actual navigation must reflect the application's requirements.

## 7. User Journey Design

Identify the steps users take to achieve important goals.

For each journey, define:

1. Starting point.
2. User intention.
3. Actions required.
4. Information required.
5. Expected system response.
6. Possible errors.
7. Successful completion state.

Example: User registration.

```text
Landing Page
     |
     v
Registration Form
     |
     v
Input Validation
     |
     v
Account Creation
     |
     v
Confirmation
     |
     v
User Dashboard
```

Consider alternative journeys such as invalid information, network failure and account conflicts.

Do not design only for the ideal successful path.

## 8. Wireframing and Layout Planning

Before detailed visual styling, establish the interface structure.

A wireframe SHOULD identify:

- Main navigation.
- Header and footer.
- Content areas.
- Important actions.
- Information hierarchy.
- Forms and controls.
- Responsive layout behavior.

Use low-fidelity wireframes when exploring structure and high-fidelity mockups when visual detail is required.

Do not introduce detailed visual decoration before the layout and information hierarchy are understood.

## 9. Visual Design System

Create a consistent visual language for the application.

### 9.1 Color system

Define colors according to their purpose.

Example:

| Token | Purpose |
|---|---|
| Primary | Main brand and important actions |
| Secondary | Supporting actions |
| Background | Main application surfaces |
| Surface | Cards and content containers |
| Text primary | Main readable content |
| Text secondary | Supporting information |
| Success | Successful states |
| Warning | Warning states |
| Error | Error states |
| Border | Separation and outlines |

Requirements:

- Maintain sufficient contrast.
- Use colors consistently.
- Avoid excessive decorative colors.
- Do not communicate important information using color alone.
- Consider light and dark themes when required.

### 9.2 Typography

Define:

- Font family.
- Heading hierarchy.
- Body text size.
- Supporting text size.
- Font weights.
- Line heights.
- Text spacing.

Requirements:

- Prioritize readability.
- Use a consistent typographic hierarchy.
- Avoid excessive font variations.
- Ensure text remains readable on mobile devices.

### 9.3 Spacing

Use a consistent spacing scale.

Example:

```text
4px
8px
12px
16px
24px
32px
48px
64px
```

Avoid arbitrary spacing values when a consistent design system can be established.

### 9.4 Components

Define reusable visual patterns for:

- Buttons.
- Input fields.
- Cards.
- Navigation bars.
- Menus.
- Dialogs.
- Alerts.
- Tables.
- Tabs.
- Pagination.
- Notifications.

Components SHOULD have consistent states and behavior.

## 10. Interaction Design

Every interactive element MUST communicate its purpose.

### Buttons

Define:

- Primary actions.
- Secondary actions.
- Destructive actions.
- Disabled states.
- Loading states.
- Hover and focus states.

### Forms

Design:

- Clear field labels.
- Appropriate input types.
- Helpful instructions.
- Validation messages.
- Required-field indicators.
- Submission feedback.

### Navigation

Ensure:

- Users understand where they are.
- Navigation labels are meaningful.
- Active sections are identifiable.
- Important destinations are accessible.
- Mobile navigation remains usable.

### Interactive feedback

Design appropriate responses for:

- Hover.
- Focus.
- Selection.
- Loading.
- Success.
- Failure.
- Disabled interactions.

Do not use animation or visual effects that interfere with task completion.

## 11. Responsive Design

Design for the devices and screen sizes relevant to the application.

Consider:

- Mobile phones.
- Tablets.
- Laptops.
- Desktop displays.

Requirements:

1. Establish appropriate responsive breakpoints.
2. Use flexible layouts.
3. Adapt navigation for smaller screens.
4. Prevent content overflow.
5. Maintain readable typography.
6. Ensure controls are usable through touch.
7. Reorganize content when necessary.
8. Preserve important information across screen sizes.

Responsive design MUST consider changes in layout and interaction, not merely shrinking desktop elements.

## 12. Accessibility and Inclusive Design

Follow applicable WCAG requirements.

Consider:

- Text contrast.
- Keyboard accessibility.
- Visible focus indicators.
- Accessible form labels.
- Descriptive links.
- Alternative text.
- Semantic content structure.
- Screen reader support.
- Clear error messages.
- Touch target usability.
- Reduced-motion preferences.

Do not rely exclusively on:
- Color.
- Sound.
- Animation.
- Mouse interaction.
- Visual position.

Accessibility SHOULD be considered from the beginning of the design process.

## 13. Design for Application States

Every important interface SHOULD account for its relevant states.

### Initial state

What users see before interacting.

### Loading state

How users understand that an operation is in progress.

### Empty state

What users see when no content or records exist.

### Success state

How users know an operation succeeded.

### Error state

How users understand and recover from a failure.

### Disabled state

How users understand why an action is unavailable.

### Permission state

How users understand that they lack access to a feature.

Design these states intentionally rather than treating them as afterthoughts.

## 14. Usability Evaluation

Review designs from the user's perspective.

Evaluate:

- Can users understand the interface?
- Can they identify the main action?
- Can they navigate without confusion?
- Can they complete important tasks?
- Are errors understandable?
- Is important information easy to find?
- Does the interface work across supported devices?
- Are accessibility needs addressed?

Use appropriate methods such as:

- Heuristic evaluation.
- Cognitive walkthroughs.
- Task-based testing.
- Accessibility reviews.
- User feedback.
- Usability testing.

Do not claim that an interface has been user-tested unless actual user testing occurred.

## 15. Design Quality and Anti-Patterns

Avoid:

- Excessive visual decoration.
- Inconsistent spacing.
- Unclear navigation.
- Poor color contrast.
- Unnecessary animations.
- Overloaded dashboards.
- Ambiguous button labels.
- Inconsistent form behavior.
- Hidden important actions.
- Desktop-only layouts.
- Nonfunctional controls.
- Decorative elements that interfere with usability.

Do not sacrifice usability to follow visual trends.

## 16. Design Handoff

When providing a design to a frontend developer or coding agent, document:

- Page structure.
- Component hierarchy.
- Layout behavior.
- Color tokens.
- Typography.
- Spacing rules.
- Interactive states.
- Responsive behavior.
- Accessibility requirements.
- Relevant assets.
- Design assumptions.

If a design tool is used, identify the relevant frames, components and assets.

The implementation team MUST be able to understand how the design is expected to behave.

## 17. Mandatory Design Workflow

### Phase 1: Discovery

1. Understand the application.
2. Identify target users.
3. Identify important tasks.
4. Review existing design constraints.
5. Establish design objectives.

### Phase 2: Structure

1. Organize application content.
2. Plan navigation.
3. Map important user journeys.
4. Define page structure.
5. Identify reusable components.

### Phase 3: Visual Design

1. Establish color tokens.
2. Define typography.
3. Define spacing.
4. Design layouts.
5. Establish component patterns.
6. Define interaction states.

### Phase 4: Experience Validation

1. Review navigation.
2. Evaluate task completion.
3. Check responsive behavior.
4. Review accessibility.
5. Evaluate error and empty states.
6. Identify usability problems.

### Phase 5: Handoff

1. Document design decisions.
2. Identify reusable components.
3. Specify responsive behavior.
4. Document interaction requirements.
5. Report unresolved design assumptions.

## 18. Definition of Done

A UI/UX design task is complete when:

- User and application requirements have been considered.
- The information architecture is understandable.
- Important user journeys are defined.
- Layouts support the intended tasks.
- Visual styles are consistent.
- Interactive states are considered.
- Responsive behavior is defined.
- Accessibility requirements are addressed.
- Important error and empty states are considered.
- Design specifications are documented.
- Remaining assumptions and limitations are reported.

## 19. Final Reporting Format

After completing a design task, provide:

### Design Summary
Explain the design outcome.

### User and Business Requirements
Summarize the needs addressed.

### Pages and Components
List the designed pages and reusable components.

### Design Decisions
Explain important visual and interaction choices.

### Responsive and Accessibility Considerations
Describe how different devices and accessibility needs were addressed.

### Validation
Report reviews or tests actually performed.

### Remaining Issues
Document unresolved questions and limitations.

## 20. Guiding Principle

Design digital experiences around the people who use them.

A successful interface should be understandable, consistent, accessible and efficient.

Visual quality matters, but usability and task completion determine whether a design genuinely serves its users.