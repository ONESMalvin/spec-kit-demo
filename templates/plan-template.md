# Implementation Plan: [FEATURE]

**Branch**: `[###-feature-name]` | **Date**: [DATE] | **Spec**: [link]
**Input**: Feature specification from `/specs/[###-feature-name]/spec.md`

**Note**: This template is filled in by the `/speckit.plan` command. See `.specify/templates/commands/plan.md` for the execution workflow.

**ONES Integration**: This template includes mandatory ONES capability validation to ensure all ONES app features are based on official platform capabilities.

## Summary

[Extract from feature spec: primary requirement + technical approach from research]

## Technical Context

**Language/Version**: TypeScript 5.x, Node.js 18+  
**Primary Dependencies**: NestJS, TypeORM, ONES OpenAPI SDK, JWT  
**Storage**: SQLite + ONES
**Testing**: Jest, Supertest  
**Target Platform**: ONES App (Linux server)  

## Project Overview

<!--
  ACTION REQUIRED: Replace the content in this section with the project implementation type, scope, constraints, and scale.
  for the project. The structure here is presented in advisory capacity to guide
  the iteration process.
-->

**Project Type**: [automation/system-integration/batch-processing/other - determine project type]  
**Performance Goals**: [performance goals, e.g., 1000 req/s, 10k lines/sec, 60 fps or NEEDS CLARIFICATION]  
**Constraints**: [domain-specific, e.g., <200ms p95, <100MB memory or NEEDS CLARIFICATION]  
**Scale/Scope**: [domain-specific, e.g., 10k users, 1M LOC, 50 screens or NEEDS CLARIFICATION]

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

### ONES Capability Validation (Mandatory for ONES Apps)

*Before proceeding with any design or development work, complete ONES capability validation.*

**Capability Mapping Requirements**:
- [ ] `/Users/malvin/Coding/appbuilder/ones-specs` directory is read
- [ ] Specific event types (e.g., `ones:project:issue:updated`) are determined
- [ ] Specific API endpoints (e.g., `PUT /openapi/v2/project/issues/{issueID}`) are determined
- [ ] Specific field IDs (e.g., `field032` corresponding to story points) are determined
- [ ] Specific oauth scopes (e.g., `read:project:issue`, `write:project:issue`) are determined

**Documentation Requirements**:
- [ ] `ones-capabilities.md` document is generated
- [ ] `research.md` is updated to include specific ONES capabilities information
- [ ] `contracts/openapi.yaml` is updated to conform to ONES specification

**Validation Requirements**:
- [ ] The capability validation script is run to verify compliance
- [ ] All feature requirements are mapped to specific ONES capabilities
- [ ] All technical decisions are based on official documentation
- [ ] All field references use the correct ID
- [ ] All API calls use the correct endpoint

### Repository and Technology Stack Constraints (Non-negotiable)
- [ ] Code changes only occur in the `my-new-project/` directory
- [ ] No new technology stacks/frameworks/runtimes are introduced (reuse NestJS, React+Vite, TypeORM, TypeScript, SQLite)
- [ ] New dependencies have been justified for necessity, compatibility, and security, and passed governance review (if applicable)
- [ ] Incremental changes are used and backward compatibility is maintained; destructive changes come with migration and impact assessment (if applicable)

**ONES App Design Check**: 
- [Good Design]Are user operations completely within ONES interface?
- [Good Design]The functionality that is triggered by user operations in ONES native interface is primarily implemented through listening to ONES events and responding (not custom APIs)?
- [Good Design]Data updates in ONES are completed by calling ONES OpenAPI?
- [Good Design]Are ONES App Extension points prioritized?
- [Bad Design]If custom APIs that users need to call are created, must explain why absolutely necessary?

**Detailed ONES App Design Checklist** (Reference: `.specify/templates/ones-app-design-checklist.md`):

### Core Design Principles
- [ ] User operations completely within ONES interface
- [ ] Prioritize using ONES App Extension points to add new pages for users to use
- [ ] The functionality that is triggered by user operations in ONES native interface is primarily implemented through listening to ONES events and responding (not custom APIs)
- [ ] Data updates in ONES are completed by calling ONES OpenAPI

### Data Flow Design
- [ ] Significant Data flow 1: User operation → ONES event → App processing → ONES OpenAPI call
- [ ] Significant Data flow 2: User operation → App page → ONES OpenAPI call
- [ ] Configuration Data flow: User operation → App page → App custom API call → App storage
- [ ] Does not create storage that duplicates ONES data

### Design Decision Validation
- [ ] Can functionality be implemented by listening to ONES events?
- [ ] Can data updates be completed by calling ONES OpenAPI?
- [ ] Is custom user interface creation necessary?
- [ ] Is storage only for necessary audit or configuration data (not duplicating ONES data)?

[Gates determined based on constitution file]

## Project Structure

### Documentation (this feature)

```
specs/[###-feature]/
├── plan.md              # This file (/speckit.plan command output)
├── research.md          # Phase 0 output (/speckit.plan command)
├── ones-capabilities.md # ONES capability mapping (mandatory for ONES apps)
├── data-model.md        # Phase 1 output (/speckit.plan command)
├── quickstart.md        # Phase 1 output (/speckit.plan command)
├── contracts/           # Phase 1 output (/speckit.plan command)
│   └── openapi.yaml     # API contracts (must conform to ONES spec)
├── checklists/          # Quality checklists
│   └── requirements.md  # Specification quality checklist
└── tasks.md             # Phase 2 output (/speckit.tasks command - NOT created by /speckit.plan)
```

### Source Code (repository root-non-negotiable)

```
src/
├── dto/
├── entities/
├── services/
├── app.controller.ts
├── app.module.ts
└── main.ts

web/
├── src/
│   ├── components/
│   ├── pages/
│   └── services/

```

**Structure Decision**: Choose a single project structure, because this is a ONES app.

## Complexity Tracking

*Fill ONLY if Constitution Check has violations that must be justified*

| Violation | Why Needed | Simpler Alternative Rejected Because |
|-----------|------------|-------------------------------------|
| [e.g., 4th project] | [current need] | [why 3 projects insufficient] |
| [e.g., Repository pattern] | [specific problem] | [why direct DB access insufficient] |

## ONES Capability Validation Errors

*Fill ONLY if ONES capability validation fails*

### Capability Mapping Failures
- **Error**: [Specific capability mapping failure]
- **Impact**: [How this affects the feature]
- **Resolution**: [How to resolve or work around]

### Documentation Failures  
- **Error**: [Specific documentation failure]
- **Impact**: [How this affects development]
- **Resolution**: [How to resolve]

### Validation Failures
- **Error**: [Specific validation failure]
- **Impact**: [How this affects compliance]
- **Resolution**: [How to resolve]

