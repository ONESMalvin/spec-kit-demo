# ONES App Design Checklist

**Purpose**: Use this checklist when designing ONES App features to ensure following correct design patterns

## Core Design Principles Check

### User Interaction Patterns
- [ ] User operations are completely within the ONES system (native interface or interface implemented through feature extensions)
- [ ] Use ONES App feature extensions to add new pages for users
- [ ] Features triggered by operations in ONES native interface are mainly implemented by listening to ONES events and responding (rather than custom APIs)

### Technical Integration Patterns
- [ ] Mainly implement functionality through event responses (rather than custom APIs)
- [ ] Use ONES OpenAPI for data operations
- [ ] Prioritize ONES extension points (when needed)
- [ ] Only store necessary audit or configuration data (not duplicating ONES data)

### Data Flow Design
- [ ] Main data flow 1: User operation → ONES event → App processing → ONES OpenAPI call
- [ ] Main data flow 2: User operation → App page → ONES OpenAPI call
- [ ] Configuration data flow: User operation → App page → App custom API call → App storage
- [ ] Connect other systems: User operation → App page → App custom API call → Other system API call
- [ ] Connect other systems: Other system → App custom API call → ONES OpenAPI call

## Design Decision Check

### Avoided Design Patterns
- [ ] Duplicate storage of ONES data (unnecessary cases)
- [ ] Design complex custom data models
- [ ] Require users to jump to other system interfaces
- [ ] Create interfaces that duplicate ONES functionality

### Recommended Design Patterns
- [ ] Event-driven automated processing
- [ ] Calculations and aggregations based on existing ONES data
- [ ] Provide configuration through ONES extension points (when needed)
- [ ] Transparently enhance existing ONES functionality

## Specific Check Items

### Feature Design
- [ ] Can functionality be implemented by listening to ONES events?
- [ ] Can data updates be completed by calling ONES OpenAPI?
- [ ] Can users complete all operations within the ONES interface?
- [ ] Is it necessary to create custom user interfaces?

### Data Design
- [ ] Has storage that duplicates ONES data been created?
- [ ] Is only necessary audit or configuration data stored?

## Common Error Patterns

### Reject Microservice Thinking
- Create independent REST APIs
- Design complex data models
- Require users to call custom interfaces

### Reject Replacement Thinking
- Create interfaces that duplicate ONES functionality
- Require users to leave the ONES system
- Design independent user workflows

### Adopt Plugin Thinking
- Respond to ONES events
- Enhance existing ONES functionality
- Maintain consistency in user operations

## Usage Guide

1. **Pre-design Check**: Before starting design, first answer the core design principles check
2. **Post-design Validation**: After completing design, use specific check items for validation
3. **Avoid Error Patterns**: Ensure microservice or replacement thinking is not adopted
4. **Stick to Plugin Thinking**: Always aim to enhance ONES functionality

## Examples

### Good Design
- Listen to `ones:project:issue:updated` event
- Automatically calculate parent task story point totals
- Call ONES OpenAPI to update parent task
- Users only need to edit story points in ONES

### Bad Design
- Create `/api/v1/story-points/update` interface
- Require users to call custom APIs
- Create complex data models
- Users need to learn new operation methods
