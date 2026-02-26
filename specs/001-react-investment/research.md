# Phase 0: Outline & Research

## Unknowns Mapped from Technical Context

1. **RAG Necessity for V1**: Is a vector DB needed for the initial iteration of the ETF suggestor, or can we rely on the LLM's parametric memory for V1 (as suggested in `task1invest.md`)?

## Research Findings

### Decision: RAG Necessity for V1
- **Decision**: No, we will NOT use RAG or a Vector Database for V1.
- **Rationale**: Based on the project guidelines outlined in `task1invest.md`, the primary goal of Task 1 is to master the *ReAct Loop* (Reasoning + Acting) and handle in-run memory. The document explicitly states: *"In this task, the agent relies solely on the knowledge LLM. Tools (RAG, Market Data Search, MCP) will be added in subsequent tasks."* Therefore, implementing RAG now violates the iterative assignment structure.
- **Alternatives considered**: Setting up ChromaDB or FAISS to ground the ETF tickers. Rejected to maintain tight scope on the reasoning mechanics first.

## Conclusion
All `NEEDS CLARIFICATION` markers from the Technical Context and Constitution Check are resolved. We will proceed to Phase 1 (Data Model & Contracts) assuming a pure LLM-driven ReAct core without external RAG retrieval for the first iteration.
