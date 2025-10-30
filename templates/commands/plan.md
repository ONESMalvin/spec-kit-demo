---
description: Execute the implementation planning workflow using the plan template to generate design artifacts.
scripts:
  sh: scripts/bash/setup-plan.sh --json
  ps: scripts/powershell/setup-plan.ps1 -Json
agent_scripts:
  sh: scripts/bash/update-agent-context.sh __AGENT__
  ps: scripts/powershell/update-agent-context.ps1 -AgentType __AGENT__
---

## User Input

```text
$ARGUMENTS
```

You **MUST** consider the user input before proceeding (if not empty).

## SIMPLIFIED ARCHITECTURE ONLY

**MANDATORY**: All implementations MUST follow this simple pattern:

### Supported Project Types (ONES App)
- ✅ **Automation**: automation script, cron jobs, timer tasks, task scheduling
- ✅ **Batch Processing**: batch data processing, file processing, data conversion
- ✅ **System Integration**: external system integration, API integration, data synchronization

### Required Architecture (ONES App adapted to Project Type)
```
Input → Processing Logic → Output
```

**Project Type Adaptations**:
- **Automation**: Event → Automation Logic → Action Execution
  - ONES Event → App backend → ONES OpenAPI call
- **Batch Processing**: Data Source → Processing Pipeline → Data Output
  - ONES User operation(app extension page) → App backend → ONES OpenAPI call
- **System Integration**: 
  - External System → App Backend → Integration Logic → ONES OpenAPI call
  - ONES User operation(ONES native interface or app extension page) → App backend → ONES OpenAPI call
  - ONES Event → App backend → External System call

### Forbidden Patterns
- ❌ Complex service layers
- ❌ Multiple data models
- ❌ Advanced caching strategies
- ❌ Microservice architectures
- ❌ Complex state management

### Required Components (Maximum 3)
1. **Input Handler**: Handle input/triggers (adapt to project type)
2. **Processor**: Simple calculation/transformation logic
3. **Output Handler**: Handle output/actions (adapt to project type)

### Simplified Workflow
1. **Skip Research Phase**: No research.md needed
2. **Minimal Design**: Only essential configuration and basic service
3. **Simple Tasks**: 6-10 tasks total (8 tasks ± 2)

## Outline

1. **Setup**: Run `{SCRIPT}` from repo root and parse JSON for FEATURE_SPEC, IMPL_PLAN, SPECS_DIR, BRANCH. For single quotes in args like "I'm Groot", use escape syntax: e.g 'I'\''m Groot' (or double-quote if possible: "I'm Groot").

2. **Load context**: Read FEATURE_SPEC and `/memory/constitution.md`. Load IMPL_PLAN template (already copied).

3. **CRITICAL: ONES Capability Validation**: Before proceeding with any design work:
   - **MANDATORY**: Read and analyze `/memory/ones-specs` directory
   - **VERIFY**: All ONES capabilities (API endpoints, event types, OAuth scopes, extension points) are explicitly documented
   - **REJECT**: Any assumed or invented ONES capabilities - mark as "REQUIRES CLARIFICATION"
   - **STOP**: If required capabilities are not found in official documentation, redesign feature or seek clarification

4. **Execute plan workflow**: Follow the structure in IMPL_PLAN template to:
   - Fill Project Overview (mark unknowns as "NEEDS CLARIFICATION")
   - **Identify project type**: Determine if it's Automation/Batch Processing/System Integration
   - Fill Constitution Check section from constitution
   - Evaluate gates (ERROR if violations unjustified)
   - Phase 0: Generate research.md (resolve all NEEDS CLARIFICATION)
   - Phase 1: Generate data-model.md, contracts/, quickstart.md (adapt to project type)
   - Phase 1: Update agent context by running the agent script
   - Re-evaluate Constitution Check post-design

5. **Stop and report**: Command ends after Phase 2 planning. Report branch, IMPL_PLAN path, and generated artifacts.

## Phases

### Phase 0: Outline & Research

1. **Extract unknowns from Technical Context** above:
   - For each NEEDS CLARIFICATION → research task
   - For each dependency → best practices task
   - For each integration → patterns task

2. **Generate and dispatch research agents**:
   ```
   For each unknown in Technical Context:
     Task: "Research {unknown} for {feature context}"
   For each technology choice:
     Task: "Find best practices for {tech} in {domain}"
   ```

3. **Consolidate findings** in `research.md` using format:
   - Choose the project type: [Automation/Batch Processing/System Integration]
     - **Automation**: Automation triggers, execution endpoints, status queries
       - Decision: [what was chosen]
       - Rationale: [why chosen]
       - Alternatives considered: [what else evaluated]
     - **Batch Processing**: Data input/output endpoints, processing status
       - Decision: [what was chosen]
       - Rationale: [why chosen]
       - Alternatives considered: [what else evaluated]
     - **System Integration**: Integration endpoints, data sync APIs, protocol adapters
       - Decision: [what was chosen]
       - Rationale: [why chosen]
       - Alternatives considered: [what else evaluated]

**Output**: research.md with all NEEDS CLARIFICATION resolved

### Phase 1: Design & Contracts

**Prerequisites:** `research.md` complete

1. **Generate contracts** from functional requirements (adapt to project type):
   - Use standard REST API patterns generate App self-defined API contracts, output schema to `contracts/api.yaml`
   - **OpenAPI Call Structures**: (If OpenAPI is used) Generate ONES OpenAPI calls with request/response schemas to `contracts/openapi-structure.yaml`
     - Extract from capability mapping: specific endpoints, parameters, response formats
     - Include authentication, error handling, and validation rules
   - **Event Callback Structures**: (If event subscription is used) Generate event callback data structures
     - Map event types from capability requirements to callback schemas to `contracts/event-callback-structure.yaml`
     - Include event data validation and processing rules 
   - **Extension Callback Structures**: (If extension is used) Generate extension callback structures
     - Map extension points (settings pages, validators, etc.) to callback schemas to `contracts/extension-callback-structure.yaml`
     - Include user interaction and data validation structures

2. **Extract entities from feature spec** → `data-model.md` (adapt to project type):
   - **Automation**: Automation rules, triggers, actions
   - **Batch Processing**: Data structures, processing steps, output formats
   - **System Integration**: Data mappings, API schemas, protocol definitions
   - Validation rules from requirements
   - State transitions if applicable

3. **Generate ONES App manifest** from capability mapping:
   - Complete`my-new-project/manifest.json` with app metadata, OAuth scopes, event listeners, extension points to meet project type requirements
     - Extract app metadata (id, name, version, description)
     - Map OAuth scopes from capability requirements
     - Configure event listeners from ONES event triggers
     - Define extension points (settings pages, validators, etc.)
   - Go to `my-new-project/` directory and run `npm install && npm run validate-manifest` to validate manifest using JSON Schema
     - Fix error according to the validation report
   - If there are errors, fix them and run `npm install && npm run validate-manifest` again until the manifest is valid

4. **Agent context update**:
   - Run `{AGENT_SCRIPT}`
   - These scripts detect which AI agent is in use
   - Update the appropriate agent-specific context file
   - Add only new technology from current plan
   - Preserve manual additions between markers

**Output**: contracts/, data-model.md, quickstart.md, manifest.json, agent-specific file

## Key rules

- Use absolute paths
- ERROR on gate failures or unresolved clarifications
