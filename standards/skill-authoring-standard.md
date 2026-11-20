# AI Agent Skills Library — Skill Authoring Standard

**Version:** 1.0  
**Status:** Active  
**Scope:** All skills in the AI Agent Skills Library

## 1. Purpose

This standard defines how skills must be designed, written, organized, validated and maintained within the AI Agent Skills Library.

Its purpose is to ensure that every skill provides clear, actionable, reusable and reliable instructions for AI agents.

A skill must do more than provide information. It must guide an AI agent through a task using defined procedures, constraints and verification steps.

## 2. Core Design Principles

Every skill must follow these principles:

### 2.1 Platform independence
- Write instructions that are not unnecessarily dependent on a particular AI coding platform.
- Avoid platform-specific commands unless they are essential to the task.
- Keep platform-specific configuration in the integrations directory.
- Do not assume that every AI agent automatically discovers or loads every SKILL.md file.

### 2.2 Modularity
- Each skill must have a clearly defined responsibility.
- Avoid combining unrelated engineering tasks into one skill.
- Reference other skills when a task requires additional expertise.
- Avoid unnecessary duplication between skills.

### 2.3 Reusability
- Write instructions that can work across multiple projects.
- Use configurable examples rather than assuming a specific project structure.
- Identify technology-specific requirements clearly.
- Avoid hardcoding project-specific paths, credentials or configurations.

### 2.4 Security first
- Treat security as a development requirement, not an optional improvement.
- Never expose secrets, access tokens, passwords or private keys.
- Do not transmit private project data to unauthorized external services.
- Require authorization before destructive or sensitive operations.
- Validate untrusted inputs and external data.

### 2.5 Verifiable results
- Require agents to inspect their work.
- Include appropriate testing and validation procedures.
- Distinguish between completed, partially completed and unverified tasks.
- Never allow an agent to claim that tests passed without executing or otherwise verifying them.

## 3. Standard Skill Directory

A skill should use the following structure when its complexity requires supporting resources:

```text
skill-name/
│
├── SKILL.md
│
├── references/
│   └── supporting-documentation.md
│
├── examples/
│   └── example-implementation.md
│
└── scripts/
    └── validation-script
```

### Directory responsibilities

- `SKILL.md`: Main instructions and workflow for the AI agent.
- `references/`: Additional technical information and detailed guidance.
- `examples/`: Illustrative implementations and examples.
- `scripts/`: Optional scripts used for validation or repeatable operations.

Only create supporting directories when they provide genuine value.

## 4. Required SKILL.md Structure

Every skill must include the following sections where applicable.

### 4.1 Metadata

Use metadata compatible with the intended skill-loading platform.

Example:

```yaml
---
name: frontend-engineering
description: Guidelines for building, reviewing and maintaining frontend applications with secure, accessible and maintainable engineering practices.
---
```

The description should explain:
- What the skill does.
- When an AI agent should use it.
- The main tasks it covers.

Follow the target platform's metadata requirements when adapting the skill.

### 4.2 Role and responsibility

Define the responsibility the AI agent assumes when using the skill.

### 4.3 Activation conditions

Explain when the skill should be activated.

Include relevant:
- User requests.
- Development tasks.
- Project conditions.
- Problems the skill is designed to solve.

### 4.4 Scope and limitations

Define what the skill covers and what it does not cover.

Identify related skills that may be needed.

### 4.5 Mandatory rules

Provide clear instructions the agent must follow.

Avoid vague statements such as "write good code."

Prefer specific requirements such as "validate user-controlled input on the server before processing it."

### 4.6 Initial inspection

Explain what the agent must inspect before making changes.

Depending on the task, this may include:
- Existing source code.
- Project structure.
- Dependencies.
- Configuration files.
- Existing tests.
- Security controls.
- Development documentation.

Agents should understand existing project conventions before modifying files.

### 4.7 Execution workflow

Provide an ordered procedure for completing the task.

The workflow should identify:
1. What to inspect.
2. What to plan.
3. What to implement.
4. What to validate.
5. What to test.
6. What to report.

### 4.8 Security requirements

Include security controls relevant to the skill.

Examples:
- Secret management.
- Input validation.
- Authentication and authorization.
- Data protection.
- Dependency security.
- Secure error handling.

### 4.9 Quality requirements

Define expectations for:
- Maintainability.
- Readability.
- Reliability.
- Performance.
- Accessibility where relevant.
- Documentation.

### 4.10 Verification and testing

Specify how the agent should verify its work.

Examples:
- Run relevant automated tests.
- Check application builds.
- Run static analysis where available.
- Validate expected behavior.
- Review changes for unintended side effects.

### 4.11 Deliverables

Define what the agent should produce.

Examples:
- Modified source files.
- Tests.
- Documentation.
- Configuration changes.
- Implementation summary.

### 4.12 Completion criteria

Define the conditions that must be satisfied before the task can be reported as complete.

## 5. Instruction Writing Rules

All skill authors must:

- Use direct, unambiguous language.
- Write instructions as actionable requirements.
- Prefer numbered workflows for sequential tasks.
- Use examples to clarify complex instructions.
- Separate mandatory requirements from recommendations.
- Explain important technical terms where necessary.
- Avoid unnecessary repetition.
- Keep instructions relevant to the skill's responsibility.

Use the words MUST, MUST NOT, SHOULD, SHOULD NOT and MAY consistently to communicate requirement strength.

## 6. Agent Behavior and Decision-Making

Skills should instruct agents to:

1. Understand the user's requested outcome.
2. Inspect relevant project context.
3. Identify missing information and important assumptions.
4. Ask for clarification when a missing detail materially affects correctness or safety.
5. Avoid unnecessary modifications.
6. Preserve existing functionality unless changes are requested.
7. Explain significant implementation decisions.
8. Report limitations honestly.

Agents must not invent test results, files, configurations or implementation details.

## 7. Safe Development Requirements

Agents must:

- Never hardcode real credentials into source code.
- Never commit secrets to version control.
- Avoid destructive operations without appropriate authorization.
- Review dependency changes before introducing new packages.
- Avoid disabling security controls merely to make an implementation work.
- Protect personal and confidential information.
- Use the least privileges necessary for tools and operations.
- Review generated code before treating it as production-ready.

## 8. Cross-Platform Compatibility

The core skill instructions should remain as platform-independent as possible.

Platform-specific adaptations belong in:

```text
integrations/
├── claude-code/
├── cursor/
├── github-copilot/
└── codex/
```

When adapting a skill:

- Follow the target platform's official discovery and loading conventions.
- Preserve the original skill's engineering requirements.
- Do not silently remove important safety instructions.
- Document any platform-specific limitations.
- Test that the platform can discover and use the adapted skill.

Compatibility must be verified rather than assumed.

## 9. Skill Validation Checklist

Before publishing a skill, verify the following:

- [ ] The skill has a clear name and purpose.
- [ ] Its activation conditions are understandable.
- [ ] Its scope and limitations are defined.
- [ ] Instructions are actionable.
- [ ] Its workflow is logically ordered.
- [ ] Relevant security requirements are included.
- [ ] Quality requirements are defined.
- [ ] Testing and verification instructions are included.
- [ ] Completion criteria are measurable.
- [ ] Examples and references are accurate.
- [ ] No real secrets or private credentials are included.
- [ ] Metadata follows the target platform's requirements.
- [ ] The skill has been reviewed for unnecessary duplication.

## 10. Versioning and Maintenance

Each skill should be maintained as a version-controlled resource.

Authors SHOULD:
- Review skills when relevant technologies change.
- Update outdated examples and dependencies.
- Document significant changes.
- Test revised instructions.
- Preserve useful backward compatibility where possible.

Use semantic versioning where a skill has an independently tracked release:

- MAJOR: Significant incompatible changes.
- MINOR: New capabilities or instructions.
- PATCH: Corrections and minor improvements.

## 11. Definition of Done

A skill is ready for publication when:

1. It follows this authoring standard.
2. Its instructions are understandable and actionable.
3. Its security requirements are appropriate.
4. Its workflow can be followed by an AI agent.
5. Its verification criteria are clear.
6. Its examples and references have been reviewed.
7. Its documentation has passed the skill validation checklist.

## 12. Guiding Principle

The objective of this library is not simply to tell AI agents what good engineering looks like.

It is to provide structured instructions that help AI agents perform engineering tasks consistently, securely, efficiently and verifiably.