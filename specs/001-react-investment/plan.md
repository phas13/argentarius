# Implementation Plan: [FEATURE]

**Branch**: `[###-feature-name]` | **Date**: [DATE] | **Spec**: [link]
**Input**: Feature specification from `/specs/[###-feature-name]/spec.md`

**Note**: This template is filled in by the `/speckit.plan` command. See `.specify/templates/plan-template.md` for the execution workflow.

## Summary

The project consists of an AI Investment Portfolio Agent built using the ReAct pattern. It takes four specific user parameters (Term, Risk tolerance via drawdown %, Age, and Investment Goal) and reasons through them to output a properly allocated portfolio of ETFs or stocks. Validating inputs, reasoning transparently, and outputting structured JSON allocations are core focus areas.

## Technical Context

<!--
  ACTION REQUIRED: Replace the content in this section with the technical details
  for the project. The structure here is presented in advisory capacity to guide
  the iteration process.
-->

**Language/Version**: Python 3.11+ or TypeScript 5+ (User preference; default assumed Python)  
**Primary Dependencies**: LangChain, Ollama (or equivalent LLM provider), Pydantic (for structuring output)  
**Storage**: N/A for initial CLI (in-memory session state)
**Testing**: pytest (if Python) or vitest/jest (if TS)
**Target Platform**: CLI / Terminal Application
**Project Type**: CLI / AI Agent application
**Performance Goals**: Agent response time < 15 seconds per turn
**Constraints**: Must run against a local model or standard API securely; responses must remain strictly within financial guardrails.
**Scale/Scope**: Local usage, single user session per execution.

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

- [x] **ReAct Architecture**: Does the plan mandate a ReAct loop for agent autonomy and reasoning? -> Yes, core design principle.
- [x] **In-Run Memory**: Is there context preservation implemented for the agent session? -> Yes, session chat history tracked.
- [x] **Tool-Based Extensibility & MCP**: Are tools defined and is MCP considered for integrations? -> Yes, optional LLM tools considered (mocked for now).
- [ ] **Knowledge Grounding (RAG)**: Is knowledge retrieval architected instead of relying entirely on LLM memory? -> NEEDS CLARIFICATION: Is a vector DB needed for the initial iteration of the ETF suggestor?
- [x] **Safety-First (Input Guardrails)**: Are inputs validated and sanitized before reaching the agent? -> Yes, via Pydantic input validators.
- [x] **Human-in-the-Loop (HITL)**: Can the agent request human clarification or authorization for decisions? -> Yes, through iterative terminal chat prompts.
- [x] **Quality Evaluation**: Is there an evaluation or optimization step before returning the final response? -> Yes, LLM verifies the 100% sum rule.
- [x] **Predictable Interfaces**: Are outputs structured predictably (e.g., JSON schemas) for reliable parsing? -> Yes, JSON output schema enforced.

## Project Structure

### Documentation (this feature)

```text
specs/[###-feature]/
├── plan.md              # This file (/speckit.plan command output)
├── research.md          # Phase 0 output (/speckit.plan command)
├── data-model.md        # Phase 1 output (/speckit.plan command)
├── quickstart.md        # Phase 1 output (/speckit.plan command)
├── contracts/           # Phase 1 output (/speckit.plan command)
└── tasks.md             # Phase 2 output (/speckit.tasks command - NOT created by /speckit.plan)
```

### Source Code (repository root)
<!--
  ACTION REQUIRED: Replace the placeholder tree below with the concrete layout
  for this feature. Delete unused options and expand the chosen structure with
  real paths (e.g., apps/admin, packages/something). The delivered plan must
  not include Option labels.
-->

```text
```text
src/
├── agent.py         # Main ReAct loop and config
├── memory.py        # In-run memory tracking
├── tools/           # Custom LLM tools (e.g., risk_calculator)
├── models/          # Pydantic schemas for inputs and structured outputs
├── run.py           # CLI entry point
└── requirements.txt

tests/
├── unit/            # Validation of input guardrails and schemas
└── integration/     # Tests mocking LLM output to test the loop
```

**Structure Decision**: Option 1: Single Python project layout was chosen as this is a terminal-based CLI application primarily requiring `src` and `tests` without complex frontend layers.

## Complexity Tracking

> **Fill ONLY if Constitution Check has violations that must be justified**

| Violation | Why Needed | Simpler Alternative Rejected Because |
|-----------|------------|-------------------------------------|
| [e.g., 4th project] | [current need] | [why 3 projects insufficient] |
| [e.g., Repository pattern] | [specific problem] | [why direct DB access insufficient] |
