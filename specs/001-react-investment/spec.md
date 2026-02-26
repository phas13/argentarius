# Feature Specification: AI Investment Portfolio Agent

**Feature Branch**: `001-react-investment`  
**Created**: 2026-02-26  
**Status**: Draft  
**Input**: Create an investment portfolio generator based on the ReAct pattern handling term, risk, age, and goals.

## User Scenarios & Testing *(mandatory)*

<!--
  IMPORTANT: User stories should be PRIORITIZED as user journeys ordered by importance.
  Each user story/journey must be INDEPENDENTLY TESTABLE - meaning if you implement just ONE of them,
  you should still have a viable MVP (Minimum Viable Product) that delivers value.
  
  Assign priorities (P1, P2, P3, etc.) to each story, where P1 is the most critical.
  Think of each story as a standalone slice of functionality that can be:
  - Developed independently
  - Tested independently
  - Deployed independently
  - Demonstrated to users independently
-->

### User Story 1 - Aggressive Growth Portfolio Generation (Priority: P1)

As a young investor with high risk tolerance aiming for maximum growth over a long horizon,
I want the AI agent to output an aggressive ETF portfolio
So that I can maximize my returns over a 20-year period.

**Why this priority**: Validates the core ReAct reasoning loop across all 4 key inputs (age, term, risk, goal).

**Independent Test**: The CLI bot successfully asks for the 4 inputs and provides an output consisting of mostly equities with logical reasoning.

**Acceptance Scenarios**:

1. **Given** term=20 years, risk=30% drawdown, age=28, goal=growth, **When** I query the console agent, **Then** it visibly reasons that an aggressive allocation (e.g., 80-100% equity) is preferred.
2. **Given** the reasoning completes, **When** the final output is printed, **Then** it suggests high-growth ETFs like VTI and VXUS with 0% or low bonds.

---

### User Story 2 - Capital Preservation / Fixed Income Generation (Priority: P2)

As an older investor nearing retirement with a strict drawdown limit and short term,
I want the AI agent to output a conservative portfolio heavily skewed towards bonds/cash
So that my capital is protected from volatility.

**Why this priority**: Proves the reasoning loop can accurately adjust allocations to the opposite end of the spectrum based on constrained risk profiles.

**Independent Test**: The CLI bot restricts equity positions correctly when given a strict max drawdown (e.g., 5%).

**Acceptance Scenarios**:

1. **Given** term=5 years, risk=5% drawdown, age=60, goal=fixed income, **When** I query the agent, **Then** it concludes equity risk must be minimized.
2. **Given** the reasoning completes, **When** the final output is printed, **Then** it recommends mostly bonds and short-term treasuries (e.g., VGSH, BND).

---

### User Story 3 - Explanation of Conflicting Goals (Priority: P3)

As an investor with unrealistic expectations,
I want the AI agent to explain why my goals conflict (e.g., high growth but no drawdown)
So that I understand the constraints of the market.

**Why this priority**: Validates the input guardrails and reasoning robustness limits.

**Independent Test**: The agent identifies the conflict instead of hallucinating an impossible portfolio.

**Acceptance Scenarios**:

1. **Given** I input 100% growth with 0% max drawdown, **When** the agent reasons, **Then** it spots the contradiction.
2. **Given** the contradiction is spotted, **When** it provides the final answer, **Then** it politely explains why high returns intrinsically carry drawdown risk and asks to compromise on one of the parameters.

### Edge Cases

<!--
  ACTION REQUIRED: The content in this section represents placeholders.
  Fill them out with the right edge cases.
-->

- What happens when a user enters non-numeric values for age or term?
- How does the system handle conflicting parameters? (e.g. 100% growth but 0% drawdown).
- What if the requested ETF category does not have 3 highly liquid options?

## Requirements *(mandatory)*

<!--
  ACTION REQUIRED: The content in this section represents placeholders.
  Fill them out with the right functional requirements.
-->

### Functional Requirements

- **FR-001**: System MUST collect 4 mandatory profile inputs from the user: Age, Term, Max Drawdown %, and Investment Goal.
- **FR-002**: System MUST utilize a ReAct Reasoning loop to explicitly display its thought process connecting the user's inputs to a specific asset allocation.
- **FR-003**: System MUST include Input Guardrails to filter malicious, irrelevant, or malformed queries.
- **FR-004**: System MUST implement Human-in-the-Loop for critical decisions or ambiguous inputs.
- **FR-005**: System MUST return its final output in a predictably structured format (e.g., JSON Schema).
- **FR-006**: System MUST output a final portfolio listing specific ETFs (or stocks) and their target percentage weights summing to 100%.

### Key Entities *(include if feature involves data)*

- **Investor Profile**: Represents the user's age, term, risk tolerance, and goal.
- **Asset Allocation**: The resultant split between equities, fixed income, and cash.
- **ETF/Asset**: The specific ticker symbol and brief description recommended for the allocation.

## Success Criteria *(mandatory)*

<!--
  ACTION REQUIRED: Define measurable success criteria.
  These must be technology-agnostic and measurable.
-->

### Measurable Outcomes

### Measurable Outcomes

- **SC-001**: The agent successfully parses and outputs a valid ReAct thought chain containing 2 or more sequential logical steps for 100% of tested profiles.
- **SC-002**: The final generated portfolio percentages sum to exactly 100% without rounding errors.
- **SC-003**: The agent correctly associates conservative inputs (elderly, short term, low drawdown) with heavy (>70%) fixed income allocations, and aggressive inputs with heavy equity (>70%) allocations in all test scenarios.
