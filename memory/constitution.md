<!--
Sync Impact Report:
- Version change: 1.2.1 → 1.2.2 (PATCH: Optimize manifest.json definition, enhance readability)
- Modified principles: 
  - II. ONES Platform Priority & Manifest-Driven Development: Added manifest.json definition explanation
- Added sections: None
- Removed sections: None
- Templates requiring updates: None (only optimized wording)
- Follow-up TODOs: None
- Project adaptation: Code changes restricted to `my-new-project/` directory only
-->

# ONES App Development Constitution

## Core Principles

### I. ONES App Design Pattern (Non-negotiable)
The goal is to implement ONES App. ONES Apps are plugin-style integrations, not independent services; user operations are completely within the ONES interface, with Apps implementing functionality through event responses and OpenAPI calls; unless absolutely necessary, must not create custom APIs that users need to call; prioritize ONES extension points if you want to implement a custom interface; Apps should be transparent to users, with users perceiving no additional complexity.

### II. ONES Platform Priority & Manifest-Driven Development
`manifest.json` is the single source of truth for application capabilities and must be:

- **Complete**: Every feature must explicitly reference corresponding ONES capability configuration
- **Valid**: All ONES capability declarations must be correctly configured and pass official schema validation
- **Synchronized**: Version updates must synchronously update the manifest
- **Isolated**: Non-ONES features must be clearly identified and independent of ONES integration
- **Compliant**: Applications must follow ONES application lifecycle management specifications

### III. Pre-Development Specification Validation (Non-negotiable)
Before starting any design or development work, must:

1. **Consult** `/Users/malvin/Coding/appbuilder/ones-specs` directory to validate requirements
2. **Select** appropriate OpenAPI/Event/Extension/Web SDK capabilities
3. **Verify** field details and implementation requirements
4. **Stop** and seek clarification if requirements cannot be mapped to known capabilities

**CRITICAL WARNING**: 
- NEVER assume or invent ONES API endpoints, event types, or permission scopes
- All ONES capabilities MUST be explicitly documented in the specs directory
- If a required capability is not found, the feature MUST be redesigned or marked as "REQUIRES CLARIFICATION"

### IV. Incremental Development & Tech Stack Constraints (Non-negotiable)
- All code changes MUST occur only under the `my-new-project/` directory; modifying platform templates or upper-level scripts is prohibited.
- Introduction of new tech stacks/frameworks/runtimes beyond the existing ones is strictly prohibited; allowed stacks: NestJS (backend), React+Vite (frontend), TypeORM, TypeScript, SQLite.
- Changes MUST be incremental with backward compatibility favored; avoid large-scale refactors. For breaking changes, first complete impact analysis and migration plan and obtain governance approval.
- New third-party dependencies MUST justify necessity, compatibility with the existing stack, and security, and pass governance review.


### V. SIMPLICITY ENFORCEMENT (NON-NEGOTIABLE)

**MANDATORY SIMPLICITY**: All implementations MUST be Simple Script Level only.

#### Forbidden Complexity
- More than three user stories or personas
- Complex error handling or retry mechanisms
- Concurrent processing
- Multi-level data hierarchies
- Performance optimization requirements
- Advanced security implementations
- Complex UI components
- Integration with more than one external system

#### Required Simplicity
- At most three user stories only
- Basic event → action pattern
- Minimal error handling (try/catch only)
- Simple data flow (read → process → update)
- No complex dependencies or frameworks

#### Simplification Process
When user requests complex features:
1. Extract the core single action
2. Remove all complexity indicators
3. Implement only the basic use case
4. Document simplifications in assumptions

**VIOLATION**: Any attempt to implement complex features will result in ERROR and request for simplification.

## Development Workflow

### ONES Open Platform Capability Validation (Mandatory Prerequisite)
- Before starting any design or development work, must complete the full ONES capability validation process
- Consult `/Users/malvin/Coding/appbuilder/ones-specs` directory to determine specific capabilities
- Generate `ones-capabilities.md` document to record specific ONES capabilities used
- Update `research.md` to include specific ONES capability information (event types, API endpoints, field IDs, etc.)
- Update `contracts/openapi.yaml` to conform to ONES official specifications
- Complete all ONES capability validation checkpoints in the planning phase (see `.specify/templates/plan-template.md`)
- If requirements cannot be mapped to known capabilities, must stop and seek clarification
- Prohibit development based on assumptions; all implementations must be based on official documentation and specific capability mappings

### Technology Stack Requirements
- Backend must use NestJS framework
- Frontend must use React + Vite
- Database uses TypeORM + SQLite (development) / PostgreSQL (production)
- Authentication uses JWT + jsonwebtoken
- All code must use TypeScript
- Prohibit introduction of other tech stacks/frameworks/runtimes; if necessary, obtain governance approval.

### Code Quality
- All code must pass ESLint and Prettier checks
- Implement unit tests and integration tests (Jest)
- Use TypeScript for type safety
- Follow ONES development best practices
- Controllers must implement appropriate error handling and logging

### Testing Strategy
- Must test all ONES integration points
- Implement mock ONES environment for testing
- Test event handling and retry mechanisms
- Verify manifest configuration correctness

### Deployment and Monitoring
- Implement health check endpoints
- Log all critical operations
- Monitor application performance and error rates
- Implement automatic rollback mechanisms

## Governance

### Version Management
- Use semantic versioning
- Major changes must update the major version number
- Maintain backward compatibility
- Provide migration guides

### Documentation Requirements
- All ONES integrations must be documented
- Provide API documentation and examples
- Maintain change logs
- Provide troubleshooting guides

### Compliance Review
- All PRs must verify manifest configuration
- Security review is mandatory
- Performance impact must be assessed
- Must pass ONES schema validation

**Version**: 1.2.2 | **Approved**: 2024-12-19 | **Last Revised**: 2025-10-20
