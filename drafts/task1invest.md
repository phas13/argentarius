# Task 1: ReAct Pattern
## Task 1 — ReAct Core (Reasoning Loop)

Learn to implement the minimal ReAct (Reasoning + Acting) pattern that combines thinking through problems with taking actions based on that reasoning. This task focuses on building a core reasoning loop that follows the think-act-observe cycle, iterating through steps to solve investment queries. You'll implement stopping criteria, integrate with in-run memory to maintain context, and handle missing information gracefully without prompting users interactively yet. The ReAct core serves as the decision-making engine for the entire Investment AI application.

### What You'll Learn

- Implement the ReAct pattern with think-act-observe cycles
- Build stopping criteria with max steps and timeout constraints
- Integrate reasoning loops with in-run memory for context retention
- Handle missing information by marking fields rather than making assumptions
- Create a solid foundation for adding tools and features in future weeks

## Definition Task 01: ReAct Pattern

### 🎯 Goal

Implement a basic AI agent for creating an investment portfolio (based on ETFs or Stocks) using the **ReAct (Reasoning + Acting)** pattern.

### 📖 What is ReAct?

**ReAct** is a pattern that combines reasoning and acting in a single loop. The agent doesn't just answer a query; it thinks step-by-step based on the investor's profile:

1. **Thought** — analyzes the request, plans the asset allocation.
2. **Reasoning** — thinks through the problem considering risk, age, term, and goals.
3. **Final Answer** — formulates the final portfolio response.

```
┌─────────────────────────────────────────────────────────────┐
│                      USER QUERY                             │
│ "Create a portfolio for 10 years, max drawdown 15%,         │
│  age 35, goal: growth"                                      │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
         ┌─────────────────────────────────────┐
         │         🤔 THOUGHT #1               │
         │  "User has a 10 year horizon,       │
         │   moderate risk (15%), age 35.      │
         │   Goal is growth."                  │
         └─────────────────────────────────────┘
                            │
                            ▼
         ┌─────────────────────────────────────┐
         │         🤔 THOUGHT #2               │
         │  "With a 10 year horizon and        │
         │   15% max drawdown, a 60/40 or      │
         │   70/30 Stocks/Bonds split fits."   │
         └─────────────────────────────────────┘
                            │
                            ▼
         ┌─────────────────────────────────────┐
         │         🤔 THOUGHT #3               │
         │  "Selecting specific ETFs:          │
         │   VTI for total market growth,      │
         │   BND for fixed income stability."  │
         └─────────────────────────────────────┘
                            │
                            ▼
                   Sufficient info?
                    /              \
                  No               Yes
                  │                 │
                  ▼                 ▼
            (think more)    ┌──────────────┐
                            │ FINAL ANSWER │
                            └──────────────┘
```

#### Why ReAct?

* **Transparency** — you can see the agent's train of thought (crucial for financial reasoning).
* **Flexibility** — easy to add new tools (in future tasks like live price fetchers).
* **Reliability** — the agent reasons before answering, checking constraints.
* **Foundation** — most modern agents are built on this pattern.

> 💡 **Note:** In this task, the agent relies solely on the knowledge LLM. Tools (RAG, Market Data Search, MCP) will be added in subsequent tasks.

### 📋 Assignment

#### Requirements

1. **Create a console chat bot** to generate investment portfolios (ETFs or Stocks).
2. **Handle specific inputs**: Your agent must digest and process:
   - Investment term (e.g., 5 years, 20 years).
   - Investor risk profile (maximum allowable percentage drawdown, e.g., 10%, 20%).
   - Investor age.
   - Investment goal (e.g., growth, fixed income, combination, saving for a target, etc.).
3. **Implement ReAct reasoning** — the agent must "think out loud" about how the inputs affect the asset allocation.
4. **Display reasoning** — the user must see the agent's thought process.
5. **Use internal LLM knowledge** about historical ETFs and typical asset allocation strategies.

### 🎮 Usage Examples

#### Example 1: Simple Goal

**Input:**

```
User: I'm 28, I want to invest for 20 years for maximum growth. I can tolerate up to a 30% drawdown.
```

**Expected Output (with reasoning):**

```
🤔 Thought 1: User is 28 years old, which indicates a long time horizon.
              Investment term is 20 years, goal is maximum growth.
              Risk tolerance allows for up to 30% drawdown.

🤔 Thought 2: Maximum growth + high risk tolerance + long time horizon 
              suggests an aggressive portfolio. A 90/10 or even 100% equity 
              allocation is suitable here.

🤔 Thought 3: To achieve broad market exposure for growth, I'll allocate heavily 
              into a Total Stock Market ETF (e.g., VTI) and a Total International 
              Stock ETF (e.g., VXUS).

🤔 Thought 4: I have sufficient information for a useful answer.

✅ Final Answer: 
Based on your age (28), horizon (20 years), goal (maximum growth), and risk tolerance (30% drawdown), here is an aggressive, high-growth ETF portfolio:

• 80% Vanguard Total Stock Market ETF (VTI) — Core US growth.
• 20% Vanguard Total International Stock ETF (VXUS) — Global diversification.
• 0% Bonds — Given your 20-year timeline and 30% drawdown tolerance, maximizing equities will historically yield the best growth.
```

#### Example 2: Conservative Goal

**Input:**

```
User: I am 60 years old. I need to invest for 5 years to save for retirement. My goal is fixed income and capital preservation. I cannot tolerate more than a 5% drawdown.
```

**Expected Output:**

```
🤔 Thought 1: User is 60 years old, approaching retirement.
              Time horizon is very short: 5 years.
              Goal is fixed income / capital preservation.
              Drawdown limit is very strict: 5%.

🤔 Thought 2: A 5% max drawdown constraint severely limits equity exposure. 
              The portfolio must be heavily weighted in bonds and cash equivalents.
          
🤔 Thought 3: A 20/80 or 10/90 Stocks/Bonds split is necessary. 
              I'll recommend short-term treasuries and total bond market ETFs, 
              with a minimal slice of equities for inflation protection.

🤔 Thought 4: I have sufficient information for the portfolio plan.

✅ Final Answer:

## Fixed Income Portfolio Plan

**Profile Context:** You have a short 5-year horizon, a very low risk tolerance (5% max drawdown), and a goal of capital preservation.

**Asset Allocation: 10% Stocks / 90% Bonds & Cash**

**Recommended ETFs:**
• 50% Vanguard Short-Term Treasury ETF (VGSH) — Extremely low volatility, protects capital.
• 40% Vanguard Total Bond Market ETF (BND) — Provides steady fixed income.
• 10% Vanguard Dividend Appreciation ETF (VIG) — A small equity position in high-quality, dividend-paying companies to slightly outpace inflation without introducing excessive drawdown risk.
```

### ✅ Acceptance Criteria

#### Mandatory

* [ ] Agent runs in the console (CLI interface).
* [ ] Agent correctly interprets and applies the 4 main inputs (term, risk/drawdown, age, goal).
* [ ] ReAct reasoning is implemented (step-by-step thinking mapping inputs to asset allocation).
* [ ] User sees the agent's reasoning (thoughts).
* [ ] Code runs via `python src/task_01/main.py` or `npx ts-node src/task_01/main.ts`.

#### Nice to have

* [ ] Implemented LLM-based tools (see "Challenge" section).
* [ ] Agent handles edge cases (e.g., "I want 100% growth but 0% drawdown", explaining why it's impossible).
* [ ] Beautiful formatted output in console (colors, emojis).
* [ ] Typing/type hints added.

### 🏆 Challenge: LLM-based Tools (Optional)

For those who want to practice with tools right away!

Instead of hardcoded reasoning, create tools that the LLM can call to determine risk profiles or fetch specific ETF data:

```python
from langchain.tools import Tool

def map_risk_to_allocation(drawdown: float, term: int) -> str:
    """Tool that uses LLM to define safe asset allocation bounds based on age/drawdown"""
    response = llm.invoke(
        f"If an investor can tolerate a max drawdown of {drawdown}% over {term} years, "
        f"what is the maximum historical equity exposure (in %) they should have?"
    )
    return response

def suggest_etf_by_category(category: str) -> str:
    """Tool to suggest specific ETFs based on asset class"""
    response = llm.invoke(
        f"Suggest the top 3 most liquid US-based ETFs for the asset class: {category}. "
        f"Return only the tickers and a 5 word description."
    )
    return response

tools = [
     Tool(name="map_risk_to_allocation", func=map_risk_to_allocation, 
          description="Map a user's risk drawdown to an equity/bond allocation ratio"),
     Tool(name="suggest_etf_by_category", func=suggest_etf_by_category, 
          description="Suggest specific ETF tickers for an asset class"),
]
```

### 🛠 Implementation Hints

#### Python + LangChain

```python
from langchain_community.llms import Ollama
from langchain.prompts import PromptTemplate

# 1. Configure LLM
llm = Ollama(model="llama3.1")  # or ChatOpenAI(), etc.

# 2. Create ReAct prompt
react_prompt = PromptTemplate.from_template("""
You are an expert financial advisor AI.

Analyze the user's investment term, risk profile (max drawdown), age, and goal.
Use the ReAct approach:
1. Thought: analyze the investor inputs.
2. Thought: think about the asset allocation step-by-step to match the risk profile.
3. Final Answer: provide the final portfolio response using ETFs.

Important: show your train of thought!

User Query: {query}

Your Response (with Thoughts and Final Answer):
""")

# 3. Create chain
chain = react_prompt | llm

# 4. CLI loop
def main():
    print("📈 AI Portfolio Manager")
    print("Type 'exit' to quit\n")
  
    while True:
        query = input("You: ")
        if query.lower() == 'exit':
            break
    
        response = chain.invoke({"query": query})
        print(f"\nAgent:\n{response}\n")

if __name__ == "__main__":
    main()
```

### 📝 Pre-submission Checklist

* [ ] Code runs without errors.
* [ ] Agent answers investment questions based on term, age, risk, and goal.
* [ ] ReAct reasoning is visible (Thought → ... → Final Answer).
* [ ] CLI interface works (console chat).
* [ ] Code is in `src/task_01/` folder.
* [ ] Commit named `Task 01: ReAct Pattern - Investments`.

**Good luck! 🚀**
