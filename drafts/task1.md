# Task 1: ReAct Pattern
## Task 1 — ReAct Core (Reasoning Loop)

Learn to implement the minimal ReAct (Reasoning + Acting) pattern that combines thinking through problems with taking actions based on that reasoning. This task focuses on building a core reasoning loop that follows the think-act-observe cycle, iterating through steps to solve travel planning requests. You'll implement stopping criteria, integrate with in-run memory to maintain context, and handle missing information gracefully without prompting users interactively yet. The ReAct core serves as the decision-making engine for the entire TravelWise AI application.Resources

What You'll Learn

Implement the ReAct pattern with think-act-observe cycles

Build stopping criteria with max steps and timeout constraints

Integrate reasoning loops with in-run memory for context retention

Handle missing information by marking fields rather than making assumptions

Create a solid foundation for adding tools and features in future weeks

## Definition Task 01: ReAct Pattern

### 🎯 Goal

Implement a basic AI agent for trip planning in Ukraine using the **ReAct (Reasoning + Acting)** pattern.

### 📖 What is ReAct?

**ReAct** is a pattern that combines reasoning and acting in a single loop. The agent doesn't just answer a query; it thinks step-by-step:

1. **Thought** — analyzes the request, plans actions.
2. **Reasoning** — thinks through the problem.
3. **Final Answer** — formulates the final response.

```
┌─────────────────────────────────────────────────────────────┐
│                      USER QUERY                             │
│        "Plan a trip to Lviv for 3 days"                     │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
         ┌─────────────────────────────────────┐
         │         🤔 THOUGHT #1               │
         │  "User wants to visit Lviv.         │
         │   Need to consider: sights,         │
         │   accommodation, food, budget..."   │
         └─────────────────────────────────────┘
                            │
                            ▼
         ┌─────────────────────────────────────┐
         │         🤔 THOUGHT #2               │
         │  "Lviv is a cultural capital.       │
         │   Key locations: Rynok Square,      │
         │   Opera House, High Castle..."      │
         └─────────────────────────────────────┘
                            │
                            ▼
         ┌─────────────────────────────────────┐
         │         🤔 THOUGHT #3               │
         │  "For 3 days optimal plan:          │
         │   Day 1 - center, Day 2 - museums,  │
         │   Day 3 - outskirts..."             │
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

* **Transparency** — you can see the agent's train of thought (debugging friendly).
* **Flexibility** — easy to add new tools (in future tasks).
* **Reliability** — the agent reasons before answering.
* **Foundation** — most modern agents are built on this pattern.

> 💡 **Note:** In this task, the agent relies solely on the knowledge LLM. Tools (RAG, Internet Search, MCP) will be added in subsequent tasks.

### 📋 Assignment

#### Requirements

1. **Create a console chat bot** for planning trips in Ukraine.
2. **Implement ReAct reasoning** — the agent must "think out loud".
3. **Display reasoning** — the user must see the agent's thought process.
4. **Use internal LLM knowledge** about Ukraine.

### 🎮 Usage Examples

#### Example 1: Simple Query

**Input:**

```
User: What is interesting to visit in Lviv?
```

**Expected Output (with reasoning):**

```
🤔 Thought 1: User wants to know about interesting places in Lviv.
              Lviv is the cultural capital of Ukraine, so there are many
              historical and cultural sights.

🤔 Thought 2: Main categories: architecture, museums, parks, gastronomy.
              Most famous places: Rynok Square, Opera House,
              High Castle, coffee shops.

🤔 Thought 3: I have sufficient information for a useful answer.

✅ Final Answer: 
In Lviv, you should visit:

• Rynok Square — the heart of the city with unique 14th-18th century architecture.
• Lviv Opera House — one of the most beautiful in Europe.
• High Castle — offers a great panorama of the city.
• Lychakiv Cemetery — an open-air museum.
• Coffee shops — "Lviv Coffee Mining Manufacture", "House of Legends".
```

#### Example 2: Trip Planning

**Input:**

```
User: Plan a trip to Odesa for 3 days
```

**Expected Output:**

```
🤔 Thought 1: User wants to plan a trip to Odesa for 3 days.
              Odesa is a seaside city with rich history and culture.
              Need to distribute activities by days.

🤔 Thought 2: Day 1 — City center and history.
              Day 2 — Sea and beaches.
              Day 3 — Unique locations and departure.
          
🤔 Thought 3: Also worth adding practical information:
              estimated budget, where to stay, what to try.

🤔 Thought 4: I have sufficient information for the travel plan.

✅ Final Answer:

## Trip Plan to Odesa (3 Days)

**About the city:** Odesa is the pearl by the sea with a unique atmosphere and humor.

**Day 1 — Historical Center:**
• Potemkin Stairs and Sea Port
• Walk along Deribasivska Street
• Odesa Opera House (evening performance)

**Day 2 — Sea and Relaxation:**
• Arcadia Beach
• Walk along Lanzheron embankment
• Seafood dinner

**Day 3 — Unique Odesa:**
• Pryvoz — legendary market
• Catacombs (excursion)
• Moldavanka — atmospheric district

**Estimated Budget:** 4500-6000 UAH
• Accommodation: 2000-3000 UAH
• Food: 1500-2000 UAH
• Entertainment: 1000 UAH
```

### ✅ Acceptance Criteria

### Mandatory

* [ ] Agent runs in the console (CLI interface).
* [ ] ReAct reasoning is implemented (step-by-step thinking).
* [ ] User sees the agent's reasoning (thoughts).
* [ ] Agent answers questions about travel in Ukraine.
* [ ] Supports at least 3-5 Ukrainian cities.
* [ ] Code runs via `python src/task_01/main.py` or `npx ts-node src/task_01/main.ts`.

#### Nice to have

* [ ] Implemented LLM-based tools (see "Challenge" section).
* [ ] Agent handles edge cases (unknown city, irrelevant query).
* [ ] Beautiful formatted output in console (colors, emojis).
* [ ] Typing/type hints added.

### 🏆 Challenge: LLM-based Tools (Optional)

For those who want to practice with tools right away!

Instead of hardcoded data, create tools that internally call the LLM:

```
from langchain.tools import Tool

def get_city_info(city: str) -> str:
    """Tool that uses LLM to get information"""
    response = llm.invoke(
        f"Tell me briefly about the city {city} in Ukraine. "
        f"Include: history, population, what it is famous for."
    )
    return response

def get_attractions(city: str) -> str:
    """Tool to find attractions via LLM"""
    response = llm.invoke(
        f"Name top 5 attractions in {city}, Ukraine with a short description."
    )
    return response

def calculate_budget(city: str, days: int) -> str:
    """Tool for budget calculation"""
    response = llm.invoke(
        f"Calculate estimated budget for a trip to {city} for {days} days. "
        f"Include: accommodation, food, transport, entertainment."
    )
    return response

tools = [
    Tool(name="get_city_info", func=get_city_info, 
         description="Get information about a Ukrainian city"),
    Tool(name="get_attractions", func=get_attractions,
         description="Find city attractions"),
    Tool(name="calculate_budget", func=calculate_budget,
         description="Calculate trip budget"),
]
```

**Benefits:**

* Practice with tool calling mechanics.
* Preparation for future tasks (RAG, Tavily, MCP).
* The agent decides when to call which tool.

### 🛠 Implementation Hints

#### Python + LangChain

```
from langchain_community.llms import Ollama
from langchain.prompts import PromptTemplate

# 1. Configure LLM
llm = Ollama(model="llama3.1")  # or ChatOpenAI(), etc.

# 2. Create ReAct prompt
react_prompt = PromptTemplate.from_template("""
You are a travel agent for trips in Ukraine.

Use the ReAct approach:
1. Thought: analyze the request
2. Thought: think about the answer step-by-step
3. Final Answer: provide the final response

Important: show your train of thought!

User Query: {query}

Your Response (with Thoughts and Final Answer):
""")

# 3. Create chain
chain = react_prompt | llm

# 4. CLI loop
def main():
    print("🇺🇦 Travel Agent Ukraine")
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

#### TypeScript + LangChain.js

```
import { ChatOllama } from "@langchain/community/chat_models/ollama";
import { PromptTemplate } from "@langchain/core/prompts";
import { StringOutputParser } from "@langchain/core/output_parsers";
import * as readline from "readline";

// 1. Configure LLM
const llm = new ChatOllama({ model: "llama3.1" });

// 2. Create ReAct prompt
const reactPrompt = PromptTemplate.fromTemplate(`
You are a travel agent for trips in Ukraine.

Use the ReAct approach:
1. Thought: analyze the request
2. Thought: think about the answer step-by-step  
3. Final Answer: provide the final response

Important: show your train of thought!

User Query: {query}

Your Response (with Thoughts and Final Answer):
`);

// 3. Create a chain
const chain = reactPrompt.pipe(llm).pipe(new StringOutputParser());

// 4. CLI loop
async function main() {
  const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout,
  });

  console.log("🇺🇦 Travel Agent Ukraine");
  console.log("Type 'exit' to quit\n");

  const askQuestion = () => {
    rl.question("You: ", async (query) => {
      if (query.toLowerCase() === "exit") {
        rl.close();
        return;
      }

      const response = await chain.invoke({ query });
      console.log(`\nAgent:\n${response}\n`);
      askQuestion();
    });
  };

  askQuestion();
}

main();
```

#### File Structure

```
src/
└── 
    ├── main.py          # or main.ts - entry point
    ├── agent.py         # agent logic
    └── prompts.py       # system prompts (optional)
```

### 📚 Resources

#### Documentation and courses

* [LangChain Prompts (Python)](https://python.langchain.com/docs/modules/model_io/prompts/ "null")
* [LangChain.js Prompts](https://js.langchain.com/docs/modules/model_io/prompts/ "null")
* [Ollama + LangChain](https://python.langchain.com/docs/integrations/llms/ollama "null")
* [ReAct Paper](https://arxiv.org/abs/2210.03629 "null") — Original paper
* [Udmey LangChain- Develop AI Agents with LangChain &amp; LangGraph](https://vitech.udemy.com/course/langchain/)
* Udemy labs: [lab1](https://vitech.udemy.com/labs/building-a-context-aware-e-commerce-chatbot-with-langchain-mastering-memory-and-chains/overview/), [lab2](https://vitech.udemy.com/labs/build-a-dynamic-weather-app-with-function-calling-in-langchain/overview/), [lab3](https://vitech.udemy.com/labs/building-a-weather-report-generator-with-langchain/overview/)
* [LangChain for LLM Application Development](https://www.deeplearning.ai/short-courses/langchain-for-llm-application-development/)
* [LangChain: Chat with Your Data](https://www.deeplearning.ai/short-courses/langchain-chat-with-your-data/)
* [AI Agents in LangGraph](https://www.deeplearning.ai/short-courses/ai-agents-in-langgraph/)

#### Video

* 📺 Udemy: ReAct Pattern (see course)

### 🤔 FAQ

**Q: Can I use a different LLM?**

A: Yes! The main goal is to implement the ReAct pattern. The choice of LLM is up to you.

**Q: How to test without an API key?**

A: Use Ollama with a local model (llama3.1, mistral).

**Q: Is it mandatory to show Thoughts?**

A: Yes, this is a key part of the task — seeing the agent's reasoning.

**Q: Are tools needed in this task?**

A: No, the basic version relies only on the reasoning LLM. Tools are optional (see "Challenge").

**Q: How many cities should the agent support?**

A: The agent relies on the LLM's knowledge, so it supports all cities known to the model.
Verify with 3-5 cities for demonstration.

### 📝 Pre-submission Checklist

* [ ] Code runs without errors.
* [ ] Agent answers basic travel questions.
* [ ] ReAct reasoning is visible (Thought → ... → Final Answer).
* [ ] CLI interface works (console chat).
* [ ] Code is in `src/task_01/` folder.
* [ ] Commit named `Task 01: ReAct Pattern`.
