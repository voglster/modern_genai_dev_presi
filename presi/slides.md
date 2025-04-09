---

# GenAI and Software Development
Modern AI-Enhanced Development Workflows and Their Impact

Presented by:
Jim Vogel (Gravitate) & Daniel Hartig (O2X)

---
layout: image-right
image: /images/ai-tech-new.jpg
---

# Introduction

- Expectations
- Terminology Breakdown
- AI in practical use
- What AI can and cannot do
- The Complexity Gap
- How AI can improve your team's workflows
- How AI is changing the development landscape

---

# What to expect

- Current devs are "efficiently" using this
- Where to apply LLMs in your workflow 
- New tools you can take to your team

---

# Terminology

- LLMs large language models
- Context Window
- RAG (Research Augmented Generation)
  - Vectorization
- Tools API
- MCP (Model Context Protocol)
- Agents
- Prompt Engineering
- Multi Modal

---

# AI in practical use

Dan
- Derived from experience migrating a Django monolith to FastAPI microservices. 
- Dedicated time over last 1.5 months with highs & lows
- AI Stack: Enterprise Tabnine ->  Claude 3.7 and ChatGPT-4o

Jim
- Large python project over last 5 years
- AI Guru pushing for its use internally
- AI Stack: Cursor AI, Claude 3.7, Custom Agents + MCPs

<!--
I have spent a lot of my own time coding over the last two months and, for the first time in my career, I did a lot of it with an AI assistant. This presentation is the results of that work.

About me, I have been active as a code writer for my entire career, even though the last 6 or so years in a management position. At Best Buy, my last company I'd be considered one of the top engineers for Go, Kubernetes and AWS/Terraform. 

At this job I have been translating Django code to FastAPI. I have some python experience in the realm of data science but had never before been responsible for a Python project architecture, nor for creating Python servers. 

With the AI assistance, I was able to easily blast through the issues of learning the new syntax. The code completion tool at first simply corrected my Go syntax into Python as I typed until I became familiar enough to use all the indentation and colons correctly.

I would say that overall, I have personally seen a 2x to 3x speedup in code throughput. For example, re-wrote a chat service (4 tables, 7 API endpoints) with 100% test coverage in about 20-25 hours. 
-->

---

## How it works

- Example from Tabnine docs ... all AI code assistants work similarly

<img src="/images/tabnine-rag-arch.avif" alt="Tabnine RAG Architecture" style="width: 80%; max-height: 70vh; object-fit: contain;" />

<!--
The customization power for an AI code assistant derives from retrieval augumented generation or RAG. RAG generates code based on similar pieces of code that already exist in your codebase, helping the AI assistant to generate code that matches your team's style.

RAG works in two ways with Tabnine. Auto-completion prompts use a locally available RAG index stored using a Quadrant vector database maintained in a docker image on your local machine. The enterprise product enables a more powerful index held on the Tabnine server, which can either be a SaaS product or self-hosted. 
-->

---
layout: two-cols
---

## Usage

- Different people like to use the tool in different ways
- 3 primary modes of use, as tracked by TabNine
    - **Inline usage** - Type in the IDE as you normally would, use enhanced tab completion to add in proposed code the AI suggests. This is what I primarily use.
    - **Chat usage** - Ask a series of questions to the AI in chat mode. Insert code from those questions as appropriate. 
    - **Agent usage** - Ask an agent to complete a task for you. Correct the results. 

::right::

<div class="ml-4" style="display: flex; align-items: center; height: 100%;">
  <img src="/images/actual-usage.png" alt="Actual AI usage statistics" style="width: 100%" />
</div>

<!--
In general, there are three ways to interact with code. First you can use it as an advanced code completion tool. Just like bash will try to autocomplete paths that you want to write, AI can be used to suggest completions on code that you are currently typing. 

Second, you can chat with it. This is exactly the same experience as chatting with ChatGPT or Perplexity, except that the models are fine-tuned by your provider to focus on code knowledge and the answers can be generated in the context of your own codebase.

Finally, there are agents, which are the newest capability just coming online. Agents can be made for specific purposes, such as creating test plans for a piece of code, or for converting Jira issues into proposed PRs. 

We can see some real data from my team here, and that different people on the team use the tool indifferent ways. I'm the guy there with the very high auto-completion usage; I find tab-completion natural to my coding style and a very effective way to rapidly fill in boilerplate code. 
-->

---

# What AI can and cannot do - Strengths

- **Functions**. Creating small self-contained chunks of code; not only functions but also methods, objects or classes. Example prompts:
> Create a pydantic class from the json specification in path/to/file.json

> Create a method on this class that converts it to this other class

> Create a function that takes a list of this class as a parameter and writes them all to the databse

- Creating full test coverage for these functions, methods and objects/classes. 
  - Tabnine has an agent specifically for this.
  - Adding test cases into an existing table test. Just ask:
  > what test cases am I missing in test_function_name

- Following concrete examples within the same context. 
> Create a function that takes a list of this class as a parameter and writes them all to the database following the example of the function at line 123 \[of path/to/file.py\]

<!--
Especially if you are new to coding with AI, make sure that you ask it questions that are more likely to give you useful answers. If you can start from any sort of documentation, describing functions that you want to exist, AI stands a good change of creating them correctly in one go, if they are not too complex. If you have existing functions and examples of testing already in place in your RAG vector graph, there is a pretty good chance that AI will be able to create useful tests in one go. 

In addition to trying it out as a code generation tool, another way to ease into AI usage is by asking it to discuss code. For me, with limited front end experience, it does a great job explaining the nuances of mobile code written in ReactNative. You can easily ask follow up questions about libraries or functions that you see used to determine what they are doing in the context of a function. 
-->

---

# What AI can and cannot do - Weaknesses

- **Syntax**. AI tools will occasionally create code that does not compile or run.
- **Using the correct version.** Because SQLAlchemy 1.4 has been out for much longer than SQLAlchemy 2.0, if you ask for links to documentation you will often get links to SQLAlchemy 1.4, even when prompting:
> "Using SQLAlchemy 2.0, create a function that does this"

- **Imagining functions.** This is particularly frustrating when it imagines a useful function in a library that simply doesn't exist. When prompted to ask where in code is this function implemented, you may get a link to a completely irrelevant chunk of code. 

<!--
Be prepared to face the limitations of AI tools, and don't butt your heads into them. There are ways around all of these limitations. To check correctness of the code that is written, it is imperative to enable a tight code -> test cycle. If you write some code, how fast can you test it?

Also, prompt management can help you to avoid certain problems by clarifying information during queries that you don't want to type out each time. For example, in our Python project we are using SQLAlchemy 2.0. We can add a global prompt that will attach this version information to any question that any user in the organization asks. 
-->

---

# What AI can and cannot do - Maybe ???

- **Creating code from diagrams**. Specifically SQLAlchemy classes from an ER diagram; either the mermaid-markdown representation or an screenshot of the rendered image.
- **Complex relationships**. Especially infrastructure as code. 
    - Does not understand templating rules in helm charts.
    - Rarely understands how to use local terraform modules.
- **YAML, JSON and bash**. Tabnine in particular does not index these files for RAG.
    - I have had success building JSON schemas from JSON objects.
    - I have not had much success with using yaml files along with the Helm terraform provider. Tabnine can't understand the yaml syntax!

<!--
Here are some notes on things that AI may be able to do, but I've had trouble with. In general, some of the more "out of the box" things that I've seen out there on the big internet don't really work that well.

These are some of the things that are likey to be big wins in future model updates and improvements; I'll make sure to come back and test these as the next generation models get rolled out. 
-->

---
layout: two-cols
---

# What AI can and cannot do - Expectations

- AI will solve your easy problems, not your hard problems.
- Easy problem: writing basic code in a language you don't know well!
  - Now your FE team can make probably-useful contributions to backend and vice-versa. 
- Example. My problem: split a yaml file with team configurations into one file per team. 
  - Do it manually or automate?
  - Copilot got it right first try with a bash script. Total time spent: approx 1 minute. 
  - I beat the meme!

::right::

<div class="ml-4" style="display: flex; align-items: center; height: 100%;">
  <img src="/images/code-automation-meme.webp" alt="Actual AI usage statistics" style="width: 100%" />
</div>

<!--
AI is great at doing something that 10,000 other engineers thave done before, but you have not done before. There are often a lot of tasks that use a library you are not familiar with or that you might do in a different language where AI can provide you a 90% solution near instantaneosly. 

Here is an exammple from my own experience. I had to split a single yaml file container information on teams into over 20 individual yaml files. I could have done this manually in a few minutes, but like any good over-engineer, I wanted to automate this. 

With Copilot, I was able to do this instantly, getting  a bash script using yq that got it right on the first try. Not a hard problem, but a great example of saving half an hour. 
-->


---

# How to make AI work better - Linting

- The single largest frustration of the AI tools is imagining functionality in a library that does not exist. 
- Initally, I spent a lot of time looking at docs to make sure that what the AI suggested is actually possible. But a strong compiler or type checker + IDE plugins can tell you much faster. 
- A static type checker such as `mypy` is an example of a tools that, when applied through the IDE, will immediately tell you if the AI is making things up. Every language has these!
- Syntax errors and non-standard created code can often be caught and corrected by linting tools. For python we use `flake8`, `black` and `isort` together. 

<!--
AI hallucinations manifest themselves in code assistant output. An AI can suggest functions that do not exist in the package you are using, but belong to similar package in the same or even another language. 

The easiest way to catch these issues without resorting to reading documentation yourself are linting tools. Every language has real-time linting tools that can be incorporated into an IDE to flag incorect AI output immediately.

What do you do when the AI is suggesting that you do something that does not work? I take advantage of the different model providers (Claude 3.7, ChatGPT-4o, Command R+), switch to a different model and ask again. 
-->

---

# How to make AI work better - Do it the same way

- You can do things a lot of ways in a lot of languages. An example from our codebase is that there are two ways (there are actually more) to do dependency injection in FastAPI:
```python
@router.get("/events/{user_id}")
async def get_fte_events(
  handler: Handler = Depends(get_handler)
  ...
)
```
vs. 
```python
@router.get("/events/{user_id}")
async def get_fte_events(
  handler: Annotated(Handler, get_handler)
  ...
)
```

- You can use AI to eliminate these different coding styles!

> Find one instance of FastAPI dependency injection in this repository using the pattern 'handler: Handler = Dependency(get_handler)' and replace it to use Annotated instead."

<!--
Retrieval augmented generation is great for helping your code look consistent. But if your code does not look consistent in the first place, you will end up with problems. If there is something that can be written two different ways, and is written two different ways throughout your codebase, you will see all variety of interpolations between those two ways.

Do it the same way every time to get the same, expected results every time.
-->

- Don't ask the AI to do too much at once. Give it one simple task to accomplish at a time.
- Give the AI examples to follow whenever possible, by pointing it to specific code snippits you want it to follow. 
> Create a unit test for this_function in path/to/file.py following the same pattern used on line 123 of path/to/test_file.py

- Even better, ensure that what you are creating is demonstrated the same way using the same pattern in the same file!

---

# Development

- Not just code
- Group of Systems
  - Idea -> Customer
- Examples
  - Continuous Discovery
  - Tickets/Organization
  - Prototypes
  - Preview
  - Feedback

---

# How Jim sees LLMS

- Human augmentation
- Just like the phone next to you
  - gps vs maps
  - google
  - ask AI
- Democratize of Knowledge
- Brainstorming Partner
- Leverage/Amplification
- Fit them into the systems

---


# Communication

- Unbiased
- Effective communication
- cleaner status updates
- Code reviews
- Organization of tasks
  - jira
  - task boards etc
  - MCPs we can talk about later

---

# Example:
- Agent that interviews the team
- Compiles the standup information

Before:
- 30 minute standups
- Disorganized
- No notes/History

After:
- 5 minute standups
- highlights are organized
- speak up if ai got it wrong


---

# The Complexity Gap: Real Examples

As we increase complexity the chance of success drops

insert graph of the complexity

## Simple Tasks: High Success Rate
Give me basic CRUD endpoints for this user model

# Why it works
- Internet is littered with examples
- task is simple
- Nothing "new" to think about

---
layout: two-cols
---

## Complex Tasks: Success Drops

Write a function to calculate net price based on 
- a mix of customer-specific rules
- fallback brand-level defaults
- a pricing floor
- and special holiday exceptions from a config object
- return errors if any constraint is violated.

# Why it doesnt work
- too much wiggle room
- not specific enough
 
::right::

<div class="ml-4">
  <img src="/images/small_jump.png" class="rounded shadow-xl" />
  <img src="/images/big_jump.png" class="rounded shadow-xl" />
</div>






---

# Rapid Prototyping with AI
## Case Study: Math Formula Visualization
- Complex MILP model visualization
- From concept to interactive UI in minutes
- Stakeholder feedback during live calls

## Vision (Multi Modal)
- napkin drawing
- design systems

---

## Streamlit Success Stories
- What is a streamlit
- Quick prototypes during customer calls
- Interactive data exploration
- Rapid iteration on business logic

::right::

<div class="ml-4">
  <img src="/images/prototype.jpg" class="rounded shadow-xl" />
</div>

---

# Modern AI-Enhanced Workflows

## Effective Prompting
- System thinking approach
- Breaking down complex tasks
- Iterative refinement

## add an image from the effective agents page

---

# Have AI interview you
- communicate better
- create a more concise prompt

---
layout: two-cols
---

## Integration Examples
- Code generation and review
- Documentation assistance
- Test case generation

::right::

<div class="ml-4">
  <img src="/images/workflow.jpg" class="rounded shadow-xl" />
</div>

---

# Testing Flow

- write the code first
- AI review, generate answers

---

# Cons

- Amplification
  - Amplifies errors too
- Easy to get "lazy"
  - Systems approach/Checklist
- Over estimating ability
  - No common sense

---
layout: two-cols
---

# Bonus: MCP
- Tools
- Model Context protocol
  - Wealth of things available
- Agent design
- Presentation was done with cursor
- Images MCP

::right::

<div class="ml-4">
  <img src="/images/llms_agents.png" class="rounded shadow-xl" />
</div>

---

# Chaining

<div class="ml-4">
  <img src="/images/chaining.png" class="rounded shadow-xl" />
</div>
---

# Iteration (Agent + State)

<div class="ml-4">
  <img src="/images/agent_iterative_style.png" class="rounded shadow-xl" />
</div>

---

# Bonus 2: Mermaid Diagrams
- Picture work 1000 words
- Communicate better
- Demo a mermaid diagram

---

# Team and Career Impact
- get on the train, don't miss it

## Knowledge Democratization
- Faster onboarding
- Reduced knowledge silos
- Improved code quality

## Productivity Gains
- 4-10x speedup on routine tasks
- Faster prototyping
- Better stakeholder communication

---
layout: center
class: text-center
---

# Thank You

Jim Vogel (Gravitate) & Daniel Hartig (O2X)