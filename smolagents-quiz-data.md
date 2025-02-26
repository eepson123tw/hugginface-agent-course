# SmolaAgents Course Solutions

This README contains all the solutions for the SmolaAgents course assignments. Feel free to copy these code examples for your reference.

## Solution 1: Create a CodeAgent with DuckDuckGo search capability

```python
from smolagents import CodeAgent, DuckDuckGoSearchTool, HfApiModel 
model = HfApiModel(model_id="Qwen/Qwen2.5-Coder-32B-Instruct") 
agent = CodeAgent(tools=[DuckDuckGoSearchTool()], model=model)
```

## Solution 2: Create web agent and manager agent structure

```python
# Create web agent and manager agent structure
web_agent = ToolCallingAgent(
    tools=[
        DuckDuckGoSearchTool(),  # For web search
    ],
    model=model,                # Use the specified model
    max_steps=10,               # Set to 10 steps as required
    name="WebResearcher",       # Descriptive name
    description="Agent specialized in researching information from the web and extracting relevant data."  # Purpose description
)

# Create manager agent that manages the web agent
manager_agent = CodeAgent(
    model=model,                # Use the same model
    managed_agents=[web_agent], # Properly manage the web agent
    additional_authorized_imports=["time", "numpy", "pandas"]  # Required additional imports
)
```

## Solution 3: Set up secure code execution environment

```python
# Set up secure code execution environment
from smolagents import CodeAgent

agent = CodeAgent(
    tools=[],
    model=model,
    # Proper security configuration
    sandbox=E2BSandbox(),  # Use E2BSandbox instead of boolean flag
    additional_authorized_imports=["numpy"]  # Use only additional_authorized_imports
)
```

## Solution 4: Create a tool-calling agent

```python
# Create a tool-calling agent
from smolagents import ToolCallingAgent

agent = ToolCallingAgent(
    tools=[
        DuckDuckGoSearchTool(),  # For web search
        WebBrowserTool(),        # For browsing web pages
        WikipediaTool(),         # For retrieving information from Wikipedia
        VisitWebpageTool()       # For directly visiting specific webpages
    ],
    model=model,                # Use the specified model
    max_steps=10,               # Allow up to 10 steps in the agent's reasoning
    name="WebResearcher",       # Give the agent a name
    description="An agent specialized in researching information from the web and extracting relevant data."  # Describe the agent's purpose
)
```

## Solution 5: Configure model integration

```python
# Configure model integration
from smolagents import HfApiModel
from smolagents import LiteLLMModel

# Option 1: Configure HfApiModel with Qwen model
hf_model = HfApiModel(model_id="Qwen/Qwen2.5-Coder-32B-Instruct")

# Option 2: Configure LiteLLMModel with Claude-3-Sonnet
other_model = LiteLLMModel(model_id="anthropic/claude-3-sonnet")
```

---

## Quiz Results
**Quiz Complete!**
Your score: 100.0% Passing score: 80.0%
Your answers:
Question 1: ✅ Question 2: ✅ Question 3: ✅ Question 4: ✅ Question 5: ✅
