# Implementation Plan: [FEATURE]

**Branch**: `[###-feature-name]` | **Date**: [DATE] | **Spec**: [link]
**Input**: Feature specification from `/specs/[###-feature-name]/spec.md`

**Note**: This template is filled in by the `/speckit.plan` command. See `.specify/templates/commands/plan.md` for the execution workflow.

**Project Integration**: This template includes capability validation to ensure all features are based on appropriate ONES capabilities and integration patterns.

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

**Project Type**: [Automation/Batch Processing/System Integration - determine project type]  
**Performance Goals**: [performance goals, e.g., 1000 req/s, 10k lines/sec, 60 fps or NEEDS CLARIFICATION]  
**Constraints**: [domain-specific, e.g., <200ms p95, <100MB memory or NEEDS CLARIFICATION]  
**Scale/Scope**: [domain-specific, e.g., 10k users, 1M LOC, 50 screens or NEEDS CLARIFICATION]

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

### ONES Capability Validation (Mandatory for ONES Apps)

*Before proceeding with any design or development work, complete ONES capability validation.*

**Capability Mapping Requirements**:
- [ ] `/Users/malvin/Coding/appbuilder/ones-specs` directory is read
- [ ] Specific event types (e.g., `ones:project:issue:updated`) and event callback structures are determined
- [ ] Specific API endpoints (e.g., `PUT /openapi/v2/project/issues/{issueID}`) and request/response schemas are determined
- [ ] Specific oauth scopes (e.g., `read:project:issue`, `write:project:issue`) are determined
- [ ] Specific extension callback structures (e.g., settings, validators, etc.) are determined

**Documentation Requirements**:
- [ ] `ones-capabilities.md` document is generated
- [ ] `research.md` is updated to include specific ONES capabilities information
- [ ] `contracts/api.yaml` is updated to conform App self-defined API specification
- [ ] (If OpenAPI is used) `contracts/openapi-structure.yaml` defines all ONES OpenAPI call structures according to ONES OpenAPI specification
- [ ] (If event subscription is used) `contracts/event-callback-structure.yaml` defines all event callback structures according to ONES event callback specification
- [ ] (If extension is used) `contracts/extension-callback-structure.yaml` defines all extension callback structures according to ONES extension callback specification  

**Validation Requirements**:
- [ ] The capability validation script is run to verify compliance
- [ ] All feature requirements are mapped to specific ONES capabilities
- [ ] All technical decisions are based on specific ONES capabilities and integration patterns
- [ ] All API calls use the correct endpoint and request/response schemas
- [ ] All ONES capabilities are properly declared in `manifest.json`
- [ ] `my-new-project/manifest.json` is completly and validated using JSON Schema

### Repository and Technology Stack Constraints (Non-negotiable)
- [ ] Code changes only occur in the `my-new-project/` directory
- [ ] No new technology stacks/frameworks/runtimes are introduced (reuse NestJS, React+Vite, TypeORM, TypeScript, SQLite)
- [ ] New dependencies have been justified for necessity, compatibility, and security, and passed governance review (if applicable)
- [ ] Incremental changes are used and backward compatibility is maintained; destructive changes come with migration and impact assessment (if applicable)

**ONES App Design Check**: 
- [Good Design] **Automation**: Are automation triggers and actions well-defined?
- [Good Design] **Batch Processing**: Are data processing steps efficient and error-handled?
- [Good Design] **System Integration**: Are integration points clearly defined and secure?
- [Bad Design] If complex custom logic is created, must explain why absolutely necessary?

**Detailed Project Design Checklist** (adapt to project type):

### Core Design Principles (adapt to project type)
- [ ] **Automation**: Efficient automation logic, proper scheduling, error handling
- [ ] **Batch Processing**: Efficient data processing, proper file handling, error recovery
- [ ] **System Integration**: Secure integration, proper data mapping, error handling

### Data Flow Design (adapt to project type)
- [ ] **Automation**: Event → Automation Logic → Action Execution
- [ ] **Batch Processing**: Data Source → Processing Pipeline → Data Output
- [ ] **System Integration**: External System → Integration Logic → Target System
- [ ] Does not create unnecessary data duplication

### Design Decision Validation (adapt to project type)
- [ ] **Automation**: Can automation be implemented with standard automation tools?
- [ ] **Batch Processing**: Can processing be implemented with standard data tools?
- [ ] **System Integration**: Can integration be implemented with standard integration patterns?
- [ ] Is custom logic only for necessary business rules (not standard functionality)?

[Gates determined based on constitution file]

## Project Structure

### Documentation (this feature)

```
specs/[###-feature]/
├── plan.md              # This file (/speckit.plan command output)
├── research.md          # Phase 0 output (/speckit.plan command)
├── ones-capabilities.md # ONES Open Platform capability mapping (adapt to project type)
├── data-model.md        # Phase 1 output (/speckit.plan command)
├── quickstart.md        # Phase 1 output (/speckit.plan command)
├── contracts/           # Phase 1 output (/speckit.plan command)
│   ├── api.yaml         # API contracts (adapt to project type)
│   ├── openapi-structure.yaml      # ONES OpenAPI call structures
│   ├── event-callback-structure.yaml   # Event subscription callback structures
│   └── extension-callback-structure.yaml # Extension callback structures (settings, validators, etc.)
├── checklists/          # Quality checklists
│   └── requirements.md  # Specification quality checklist
├── manifest.json        # ONES App manifest (Phase 1 output)
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

**Structure Decision**: Choose appropriate ONES App project structure based on project type (Automation/Batch Processing/System Integration).

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

