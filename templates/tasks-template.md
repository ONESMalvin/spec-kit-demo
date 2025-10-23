---
description: "Simplified task list template for feature implementation"
---

# Tasks: [FEATURE NAME]

**Input**: Design documents from `/specs/[###-feature-name]/`
**Prerequisites**: plan.md (required), spec.md (required for user stories), research.md, data-model.md, contracts/

**CRITICAL**: ALL features MUST use this simplified template. 6-10 tasks total (8 tasks ± 2).

**Project Type**: [Automation/Batch Processing/System Integration]

## Format: `[ID] [P?] Description`
- **[P]**: Can run in parallel (different files, no dependencies)
- Include exact file paths in descriptions
- **NO Story labels**: Simplified template does not use [US1], [US2] labels

<!-- 
  ============================================================================
  IMPORTANT: The tasks below are SAMPLE TASKS for illustration purposes only.
  
  The /speckit.tasks command MUST replace these with actual tasks based on:
  - Project type identification (Automation/Batch Processing/System Integration)
  - Feature requirements from plan.md
  - User stories from spec.md (with their priorities P1, P2, P3...)
  
  Tasks MUST follow the SIMPLIFIED TEMPLATE structure:
  - Phase 1: Setup (2 tasks)
  - Phase 2: Core Implementation (4 tasks)
  - Phase 3: Integration (2 tasks)
  
  TOTAL: 6-10 tasks (8 tasks ± 2) - flexible based on project complexity
  
  DO NOT keep these sample tasks in the generated tasks.md file.
  ============================================================================
-->

## Phase 1: Setup (2 tasks)

**Purpose**: Project initialization and basic structure

- [ ] T001 Review and verify project structure in my-new-project/
- [ ] T002 Configure manifest.json for ONES App configuration in my-new-project/manifest.json

---

## Phase 2: Core Implementation (4 tasks)

**Purpose**: Essential services and logic (adapt to project type)

**Project Type Adaptations**:
- **Automation**: trigger mechanisms, execution logic, scheduler
- **Batch Processing**: data processing, file operations, conversion logic
- **System Integration**: API calls, data synchronization, protocol adaptation

- [ ] T003 [P] Create core service/component in my-new-project/src/services/
- [ ] T004 [P] Implement main processing logic in my-new-project/src/services/
- [ ] T005 [P] Create data handling service in my-new-project/src/services/
- [ ] T006 [P] Add basic error handling in my-new-project/src/services/

---

## Phase 3: Integration (2 tasks)

**Purpose**: Wire components together and add logging

- [ ] T007 [P] Wire components together in my-new-project/src/
- [ ] T008 [P] Add basic logging in my-new-project/src/

**TOTAL: 6-10 tasks (8 tasks ± 2) - flexible based on project complexity**

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies - can start immediately
- **Core Implementation (Phase 2)**: Depends on Setup completion
- **Integration (Phase 3)**: Depends on Core Implementation completion

### Task Dependencies

- **T001 → T002**: Project structure must be verified before configuration
- **T003, T004, T005, T006**: Can run in parallel (marked with [P])
- **T007, T008**: Can run in parallel (marked with [P]) after Phase 2 completion

### Parallel Opportunities

- **Phase 1**: T001 and T002 must run sequentially
- **Phase 2**: T003, T004, T005, T006 can all run in parallel
- **Phase 3**: T007 and T008 can run in parallel

---

## Parallel Examples

### Phase 2: Core Implementation (4 parallel tasks)

```bash
# Launch all Core Implementation tasks together:
Task: "Create core service/component in my-new-project/src/services/"
Task: "Implement main processing logic in my-new-project/src/services/"
Task: "Create data handling service in my-new-project/src/services/"
Task: "Add basic error handling in my-new-project/src/services/"
```

### Phase 3: Integration (2 parallel tasks)

```bash
# Launch both Integration tasks together:
Task: "Wire components together in my-new-project/src/"
Task: "Add basic logging in my-new-project/src/"
```

---

## Implementation Strategy

### Sequential Execution

1. Complete Phase 1: Setup (T001 → T002)
2. Complete Phase 2: Core Implementation (T003, T004, T005, T006 in parallel)
3. Complete Phase 3: Integration (T007, T008 in parallel)
4. **VALIDATE**: Test complete feature independently


---

## Notes

- [P] tasks = different files, no dependencies
- **NO Story labels**: Simplified template does not use [US1], [US2] labels
- **Flexible task count**: TOTAL: 6-10 tasks (8 tasks ± 2) - flexible based on project complexity
- **Project type adaptation**: Adapt task descriptions based on Automation/Batch Processing/System Integration
- Commit after each task or logical group
- **Forbidden task types**: Avoid complex data modeling, advanced error handling, performance optimization, security implementation, testing framework setup, deployment configuration, monitoring and alerting
- Focus on essential functionality only



