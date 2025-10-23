---
description: Generate an actionable, dependency-ordered tasks.md for the feature based on available design artifacts.
scripts:
  sh: scripts/bash/check-prerequisites.sh --json
  ps: scripts/powershell/check-prerequisites.ps1 -Json
---

## User Input

```text
$ARGUMENTS
```

You **MUST** consider the user input before proceeding (if not empty).

## SIMPLIFIED TASK TEMPLATE (MANDATORY)

**CRITICAL**: ALL features MUST use this simplified template. 6-10 tasks total (8 tasks ± 2).

### Phase 1: Setup (2 tasks)
- [ ] T001 Review and verify project structure in my-new-project/
- [ ] T002 Configure manifest.json for ONES App configuration in my-new-project/manifest.json

### Phase 2: Core Implementation (4 tasks)
- [ ] T003 [P] Create core service/component in my-new-project/src/services/
- [ ] T004 [P] Implement main processing logic in my-new-project/src/services/
- [ ] T005 [P] Create data handling service in my-new-project/src/services/
- [ ] T006 [P] Add basic error handling in my-new-project/src/services/

### Phase 3: Integration (2 tasks)
- [ ] T007 [P] Wire components together in my-new-project/src/
- [ ] T008 [P] Add basic logging in my-new-project/src/

**TOTAL: 6-10 tasks (8 tasks ± 2) - flexible based on project complexity**

### Supported Project Types
- ✅ **Automation**: automation script, cron jobs, timer tasks, task scheduling, event listening
- ✅ **Batch Processing**: batch data processing, file processing, data conversion
- ✅ **System Integration**: external system integration, API integration, data synchronization

### Forbidden Task Types
- ❌ Complex data modeling tasks
- ❌ Advanced error handling tasks
- ❌ Performance optimization tasks
- ❌ Security implementation tasks
- ❌ Testing framework setup tasks
- ❌ Deployment configuration tasks
- ❌ Monitoring and alerting tasks

## Outline

1. **Setup**: Run `{SCRIPT}` from repo root and parse FEATURE_DIR and AVAILABLE_DOCS list. All paths must be absolute. For single quotes in args like "I'm Groot", use escape syntax: e.g 'I'\''m Groot' (or double-quote if possible: "I'm Groot").

2. **Load design documents**: Read from FEATURE_DIR:
   - **Required**: plan.md (tech stack, libraries, structure), spec.md (user stories with priorities)
   - **Optional**: data-model.md (entities), contracts/ (API endpoints), research.md (decisions), quickstart.md (test scenarios)
   - Note: Not all projects have all documents. Generate tasks based on what's available.

3. **Execute simplified task generation workflow**:
   - Load plan.md and extract tech stack, libraries, project structure
   - Load spec.md and extract user stories with their priorities (P1, P2, P3, etc.)
   - **MANDATORY**: Generate tasks using the SIMPLIFIED TASK TEMPLATE above
   - **CRITICAL**: 6-10 tasks total (8 tasks ± 2) - flexible based on project complexity
   - **Identify project type**: Determine if it's type of automation/batch-processing/system-integration
   - Map user stories to the 3-phase structure: Setup (2 tasks) → Core Implementation (4 tasks) → Integration (2 tasks)
   - Adapt task descriptions based on project type (automation triggers, batch processing, integration endpoints)
   - Ensure all tasks follow the simplified checklist format
   - Focus on essential functionality only - avoid complex features

4. **Generate tasks.md**: Use the SIMPLIFIED TASK TEMPLATE structure, fill with:
   - Correct feature name from plan.md
   - **Identify project type**: Automation/Batch Processing/System Integration
   - **Phase 1: Setup (2 tasks)** - Project structure and configuration
   - **Phase 2: Core Implementation (4 tasks)** - Essential services and logic (adapt to project type)
   - **Phase 3: Integration (2 tasks)** - Wire components and add logging
   - All tasks must follow the simplified checklist format
   - Clear file paths for each task
   - **Adapt descriptions**: Use appropriate terminology for project type
   - **NO complex features**: Avoid forbidden task types listed above

5. **Report**: Output path to generated tasks.md and summary:
   - **Total task count: MUST be 6-10 tasks (8 tasks ± 2)**
   - **Project type identified**: Automation/Batch Processing/System Integration
   - Task distribution: Setup (2) → Core Implementation (4) → Integration (2)
   - Parallel opportunities identified (marked with [P])
   - Format validation: Confirm ALL tasks follow the simplified checklist format
   - **CRITICAL**: Verify no forbidden task types are included

Context for task generation: {ARGS}

The tasks.md should be immediately executable - each task must be specific enough that an LLM can complete it without additional context.

## Task Generation Rules

**CRITICAL**: ALL features MUST use the SIMPLIFIED TASK TEMPLATE above. 6-10 tasks total (8 tasks ± 2).

**MANDATORY STRUCTURE**: 
- Phase 1: Setup (2 tasks)
- Phase 2: Core Implementation (4 tasks) 
- Phase 3: Integration (2 tasks)

**Tests are FORBIDDEN**: No test tasks allowed in simplified template.

### Simplified Checklist Format (REQUIRED)

Every task MUST strictly follow this simplified format:

```text
- [ ] T00X [P?] Description with file path
```

**Format Components**:

1. **Checkbox**: ALWAYS start with `- [ ]` (markdown checkbox)
2. **Task ID**: Sequential number (T001, T002, T003...T008) in execution order
3. **[P] marker**: Include ONLY if task is parallelizable (different files, no dependencies)
4. **Description**: Clear action with exact file path
5. **NO Story labels**: Simplified template does not use [US1], [US2] labels

**Examples**:

- ✅ CORRECT: `- [ ] T001 Review and verify ONES App structure in my-new-project/`
- ✅ CORRECT: `- [ ] T003 [P] Create event listener service in my-new-project/src/services/event-listener.service.ts`
- ✅ CORRECT: `- [ ] T007 [P] Wire services together in my-new-project/src/app.module.ts`
- ❌ WRONG: `- [ ] Create service` (missing ID and file path)
- ❌ WRONG: `T001 Create service` (missing checkbox)
- ❌ WRONG: `- [ ] [US1] Create service` (story labels forbidden in simplified template)

### Simplified Task Organization

**MANDATORY**: Use the SIMPLIFIED TASK TEMPLATE structure only:

1. **Phase 1: Setup (2 tasks)**
   - Project structure verification
   - Configuration setup (adapt to project type)

2. **Phase 2: Core Implementation (4 tasks)**
   - **Automation**: automation script, cron jobs, timer tasks, task scheduling, event listening
   - **Batch Processing**: data processing, file operations, conversion logic
   - **System Integration**: API calls, data synchronization, protocol adaptation
   - Basic error handling

3. **Phase 3: Integration (2 tasks)**
   - Component wiring
   - Basic logging

**Adapt to project type**: Use appropriate terminology and focus areas based on Automation/Batch Processing/System Integration.


