---
theme: default
background: /images/main-bg.jpg
title: GenAI and Software Development
info: |
  ## GenAI and Software Development
  Modern AI-Enhanced Development Workflows and Their Impact
class: text-center
drawings:
  persist: false
transition: slide-left
mdc: true
highlighter: shiki
lineNumbers: false
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

- AI in practical use
- What AI can and cannot do
- The Complexity Gap
- How AI can improve your team's workflows
- How AI is changing the development landscape



---

# AI in practical use

- The notes in here derive from experience working with migrating a Django monolith to FastAPI microservices. 
- I have personally spent a large amount of time over the last 1.5 months on this project and have experienced the highs and lows. 
- Our team uses Enterprise Tabnine, which offers Claude 3.7 and ChatGPT-4o among other options.

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
  <img src="/images/actual-usage.PNG" alt="Actual AI usage statistics" style="width: 100%" />
</div>

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

---

# What AI can and cannot do - Weaknesses

- **Syntax**. AI tools will occasionally create code that does not compile or run.
- **Using the correct veresion.** Because SQLAlchemy 1.4 has been out for much longer than SQLAlchemy 2.0, if you ask for links to documentation you will often get links to SQLAlchemy 1.4, even when prompting:
> "Using SQLAlchemy 2.0, create a function that does this"

- **Imagining functions.** This is particularly frustrating when it imagines a useful fuction in a library that simply doesn't exist. When prompted to ask where in code is this function implemented, you may get a link to a completely irrelevant chunk of code. 

---

# What AI can and cannot do - Maybe ???

- **Creating code from diagrams**. Specifically SQLAlchemy classes from an ER diagram; either the mermaid-markdown representation or an screenshot of the rendered image.
- **Complex relationships**. Especially infrastructure as code. 
    - Does not understand templating rules in helm charts.
    - Rarely understands how to use local terraform modules.
- **Repository sync**. I have chosen to unlink our TabNine enterprise instance from our GitLab account due to it using older version of the main as source. 
    - Especially true when multiple people are working in different branches. 
    - Great reason for trunk based development. 
    - Great reason to use monorepos so entire context lives locally. No need for GitHub/GitLab connector!
    - I am not sure I am doing this right!

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


---

# How to make AI work better - Linting

- The single largest frustration of the AI tools is imagining functionality in a library that does not exist. 
- Initally, I spent a lot of time looking at docs to make sure that what the AI suggested is actually possible. But a strong compiler or type checker + IDE plugins can tell you much faster. 
- A static type checker such as `mypy` is an example of a tools that, when applied through the IDE, will immediately tell you if the AI is making things up. Every language has these!
- Syntax errors and non-standard created code can often be caught and corrected by linting tools. For python we use `flake8`, `black` and `isort` together. 

---

# How to make AI work better - Do it the same way

- You can do things a lot of ways in a lot of languages. An example from our codebase is that there are two ways (there are actually more) to do dependency injection in FastAPI:
```python
handler: Handler = Depends(get_handler)
```
vs. 
```python
handler: Annotated(Handler, get_handler)
```

- If you mix these two in the context you provide to your AI, you will see all sorts of marvelous interpolations between the two. Do it the same way every time to get the same results.
- You can use AI to search of usage variations in your library and correct them.

> Find one instance of FastAPI dependency injection in this repository using the pattern 'handler: Handler = Dependency(get_handler)' and replace it to use Annotated instead."

- Repeat!
---

# How to make AI work better - Constrain complexity 

- Don't ask the AI to do too much at once. Give it one simple task to accomlish at a time.
- Give the AI examples to follow whenever possible, by pointing it to specific code snippits you want it to follow. 
> Create a unit test for this_function in path/to/file.py following the same pattern used on line 123 of path/to/test_file.py

- Even better, ensure that what you are creating is demonstrated the same way using the same pattern in the same file!



---
layout: default
---

# The Complexity Gap: Real Examples

## Simple Tasks: High Success Rate
```python
# AI nails this immediately
@app.post("/users")
def create_users(users: List[UserModel]):
    return db.users.insert_many([u.dict() for u in users])
```

---

## Complex Tasks: Success Drops
```python
# AI struggles with complex business logic
@app.post("/process-excel")
async def process_excel(
    file: UploadFile,
    rules: BusinessRules,
    config: Dict[str, Any]
):
    # AI often misses:
    # - Proper error handling
    # - Business rule validation
    # - Multiple collection updates
    # - Status reporting
```

---
layout: two-cols
---

# Rapid Prototyping with AI

---

## Case Study: Math Formula Visualization
- Complex MILP model visualization
- From concept to interactive UI in minutes
- Stakeholder feedback during live calls


---

## Streamlit Success Stories
- Quick prototypes during customer calls
- Interactive data exploration
- Rapid iteration on business logic

::right::

<div class="ml-4">
  <img src="/images/prototype.jpg" class="rounded shadow-xl" />
</div>

---
layout: default
---

# Breaking Down Complex Problems

## The Right Way
1. Decompose into smaller tasks
2. Use AI for specific syntax/patterns
3. Maintain system-level thinking
4. Validate each component


---

Write a Python function that calculates the net price after applying a 5% discount.

## Example: Pricing Engine
Simple:
```python
def calculate_discount(price: float) -> float:
    return price * 0.95  # 5% discount
```

---


Write a function to calculate net price based on a mix of customer-specific rules, fallback brand-level defaults, a pricing floor, and special holiday exceptions from a config object, and return errors if any constraint is violated.

Complex (needs decomposition):
```python
def calculate_net_price(
    base_price: float,
    customer_rules: dict,
    brand_defaults: dict,
    holiday_config: dict
) -> tuple[float, list[str]]:
    # Break this down into:
    # 1. Customer rule application
    # 2. Brand default fallbacks
    # 3. Holiday special handling
    # 4. Constraint validation
```

---
layout: two-cols
---

# Modern AI-Enhanced Workflows

## Effective Prompting
- System thinking approach
- Breaking down complex tasks
- Iterative refinement

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
layout: default
---

# Team and Career Impact

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

[GitHub](https://github.com/yourusername) · [Twitter](https://twitter.com/yourusername)
