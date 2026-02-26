# Argentarius Agent Constitution

<!-- 
Sync Impact Report
Version Change: New initialization (v1.0.0)
Modified principles: 8 core AI Agent principles defined
Added sections: Additional Architecture Constraints, Development Workflow
Removed sections: N/A
Templates requiring updates:
  - ✅ .specify/templates/plan-template.md 
  - ✅ .specify/templates/spec-template.md
  - ✅ .specify/templates/tasks-template.md
Follow-up TODOs: None. Templates successfully aligned to AI Agent principles.
-->

## Core Principles

### I. ReAct Architecture
All agents must implement a ReAct (Reasoning and Acting) loop, ensuring clear separation between thought processes, decision making, and the execution of tools to gather context or perform actions.

### II. In-Run Memory
Agents must maintain conversational context and session state for the duration of a run to support follow-up queries, complex multi-turn workflows, and continuous interactions.

### III. Tool-Based Extensibility & MCP
Agents must utilize defined tools for all external interactions (e.g. APIs, internet search). Specifically, systems should leverage the Model Context Protocol (MCP) where applicable for standardized, robust server integrations.

### IV. Knowledge Grounding (RAG)
Agents must use Retrieval-Augmented Generation to ground responses in domain-specific, verified knowledge bases rather than relying solely on the LLM's inherently limited parametric memory.

### V. Safety-First Execution (Input Guardrails)
All inputs MUST pass through guardrails for validation, filtering out irrelevant, malformed, or unsafe interactions before they are processed by the main reasoning loop.

### VI. Human-in-the-Loop (HITL)
Systems MUST integrate Human-in-the-Loop capabilities to dynamically resolve ambiguity, clarify missing constraints, and authorize critical or sensitive actions during agent execution.

### VII. Quality Evaluation & Optimization
Agent final outputs MUST go through an Evaluator or Optimizer step to proactively assess completeness, qualitative standards, and logical correctness before returning the response to the user.

### VIII. Predictable Interfaces (Structured Output)
Final system outputs and inter-agent or inter-component protocols MUST be strictly structured (typically via JSON schemas) to ensure system reliability, parsability, and predictable downstream processing.

## Additional Architecture Constraints

- **Language Support**: Implementations must be well-organized in modern Python or TypeScript environments.
- **LLM Independence**: The design should remain decoupled from a single inference vendor. Support for multiple LLMs, both local via Ollama (e.g. Llama-3, Qwen) and Cloud API models (e.g. OpenAI, Anthropic, Gemini) must be maintained.
- **Vector Database**: For RAG persistence, the integration with a reliable vector store (e.g. Chroma, FAISS) is expected.

## Development Workflow

- **Branching**: Develop features in isolated branches clearly identifying the task.
- **Committing**: Granular commits during development are encouraged, but multiple commits for a given feature/task MUST be logically squashed to maintain history linearity when feasible.
- **Iterative Growth**: The project codebase is unified. Functional increments are built on top of the established agent backbone accumulatively.

## Governance

- All Pull Requests and architectural reviews MUST verify compliance with the 8 Core AI Agent Principles.
- Complexity or deviation from these standards must be explicitly documented, justified, and ratified by the engineering team.
- Amendments to the constitution require a version bump in `CONSTITUTION_VERSION` and `LAST_AMENDED_DATE` adjustments, along with Sync Impact Report documentation at the document header.

**Version**: 1.0.0 | **Ratified**: 2026-02-26 | **Last Amended**: 2026-02-26
