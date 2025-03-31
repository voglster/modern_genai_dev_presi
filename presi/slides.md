---
# You can also start simply with 'default'
theme: default
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: /images/main-bg.jpg
# some information about your slides (markdown enabled)
title: GenAI and Software Development
info: |
  ## GenAI and Software Development
  Modern AI-Enhanced Development Workflows and Their Impact
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
# open graph
# seoMeta:
#  ogImage: https://cover.sli.dev
highlighter: shiki
lineNumbers: false
---

# GenAI and Software Development
Modern AI-Enhanced Development Workflows and Their Impact

---
layout: intro
---

# Introduction

- GenAI/LLMs as leverage tools for developers
- The amplification effect
- How AI is changing the development landscape

::right::

<div class="ml-4">
  <img src="/images/ai-tech-new.jpg" class="rounded shadow-xl" />
</div>

---
layout: two-cols
---

# The Amplification Effect

- AI magnifies both skills and mistakes
- Junior developers: mistakes get amplified
- Senior developers: 4-10x speedup with careful use

---

## Real-World Example
"I need a MongoDB aggregation pipeline..."
- SQL background → MongoDB syntax not natural
- AI instantly provides correct syntax
- Validates against common pitfalls

::right::

<div class="ml-4">
  <img src="/images/coding-new.jpg" class="rounded shadow-xl" />
</div>

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
