---
description: Different flavors of Agents and workflows
---

# Different types of Agent Workflow Patterns

### **The Building Block for an Agentic System**

<figure><img src="../.gitbook/assets/Building Block for AI Agents.png" alt="" width="563"><figcaption><p>The basic building block for an AI agent.</p></figcaption></figure>



The basic building block for an Agent is shown above.  Some folks might call this a **Standalone Agent.**&#x20;

For the sample workflow above, one of the steps (Step 2)  interacts with the Agent.

For most workflows, a single standalone agent will do the trick.



#### Working Memory&#x20;

The working memory for an agent involves the ability to retrieve previous conversations or details shared by the user, as well as previous generations.&#x20;

This memory allows the agent to keep track of past interaction



### **Prompt Chaining with an LLM Block**

<figure><img src="../.gitbook/assets/PromptChaining.png" alt="" width="563"><figcaption><p>Prompt Chaining</p></figcaption></figure>

I am using the "LLM Block" interchangeably with "Agent" or "Standalone Agent" based on the [diagram](different-types-of-agent-workflow-patterns.md#the-building-block-for-an-agentic-system) I drew earlier.

**Prompt chaining** helps create a more accurate agentic system.  Prompt chaining decomposes complex requests into smaller, more manageable subtasks by:

* Reducing the cognitive load on the LLM.  Yes, Cognitive load is not just for humans!
* Improving accuracy through focused prompts
* Creating a step-by-step reasoning process

#### Performance Tradeoffs

* **Pros:** Higher accuracy, more controllable.  As you see in the diagram above you can programmatically check the output.
* **Cons:** Increased latency, more API calls

```
// Here is pseudocode so that you understand Prompt Chaining
// In the diagram above, I have made one call to the LLM 
//But it's decomposed into three calls 

# Initial Broad Prompt
initial_prompt = """
Identify emerging consumer electronics trends for 2024. 
Focus on innovative products that solve real-world problems.
"""

# Example Input: Trend Identification
trends = llm.generate(initial_prompt)
# Possible Output: "Smart home devices, AI-powered health tech, sustainable electronics"

# Example Call 1 for checking: Check if the output has at least one AI reference
CheckOutput(trends)

# Example LLM Call 2: Detailed Market Analysis
market_analysis_prompt = f"""
Given these emerging trends: {trends}

For each trend, provide:
1. Specific product opportunities
2. Target market demographics
3. Potential technological challenges
"""

market_details = llm.generate(market_analysis_prompt)
# Example Call 2 for checking: Check if the output has at least two tasks
CheckOutput(market_details)


# Detailed breakdown of each trend's market potential

# Example LLM Call 3: Competitive Landscape
competitive_prompt = f"""
Analyze the competitive landscape for these product opportunities:
{market_details}

For each product opportunity, identify:
- Top 3 potential competitors
- Unique value proposition
- Estimated market entry barriers
"""

competitive_analysis = llm.generate(competitive_prompt)
```













