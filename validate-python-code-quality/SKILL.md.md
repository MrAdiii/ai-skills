---
name: validate-python-code-quality
description: Review, write, refactor, and validate Python code for semantic correctness, naming, module/package structure, maintainability, error handling, typing, and idiomatic Python. Use whenever Python code quality or structure is being evaluated or improved.
---

# Python Code Quality & Semantics

## Purpose

Review Python code for correctness, clarity, maintainability, and semantic consistency.

Do not limit validation to syntax or formatting. Evaluate whether the code's names, structure, types, abstractions, and behavior accurately represent its intent.

Prioritize:
1. Correctness
2. Semantic accuracy
3. Architecture
4. Maintainability
5. Idiomatic Python
6. Style

## Naming

Follow standard Python conventions:

| Element | Convention |
|---|---|
| Variables | `snake_case` |
| Functions | `snake_case` |
| Methods | `snake_case` |
| Classes | `PascalCase` |
| Constants | `UPPER_SNAKE_CASE` |
| Modules/files | `snake_case.py` |
| Packages/directories | `snake_case` |
| Private members | `_snake_case` |

Validate semantic accuracy, not just formatting.

Prefer:
```python
customer = get_customer()
```

over:
```python
data = get_customer()
```

Boolean names should communicate meaning:
```python
is_active
has_permission
can_retry
should_process
```

Avoid vague names such as `data`, `value`, `flag`, `status`, or `check` when a precise name is available.

## Modules and Packages

Treat a `.py` file as a module and a directory containing related modules as a package.

Prefer cohesive modules organized around related responsibilities.

Example:
```text
users/
├── __init__.py
├── models.py
├── repository.py
├── service.py
└── validators.py
```

Avoid both:
- Huge modules containing unrelated responsibilities
- Excessive fragmentation into trivial one-concept files

Evaluate boundaries based on cohesion and responsibility.

## Semantic Validation

Check whether implementation and naming agree.

Look for:
- Functions whose names do not describe their behavior
- Variables whose values do not match their names
- Incorrect return-value assumptions
- Misleading abstractions
- Contradictory conditions
- Dead or unreachable logic
- Functions performing unrelated operations
- Parameters whose semantics are unclear

## Imports

Check for:
- Unused imports
- Circular dependencies
- Incorrect import paths
- Wildcard imports
- Architectural dependency violations
- Imports of implementation details when a public interface exists

Prefer explicit imports:
```python
from users.service import UserService
```

Avoid:
```python
from users.service import *
```

## Functions

Evaluate:
- Clear responsibility
- Meaningful name
- Appropriate parameters
- Accurate return value
- Side effects
- Error behavior
- Complexity

Do not split functions merely to make them shorter. Split them when boundaries improve meaning, reuse, testing, or maintainability.

## Classes

Use classes when they provide meaningful state, behavior, or abstraction.

Check:
- Cohesive responsibility
- Appropriate methods
- State management
- Whether inheritance is justified
- Whether composition is clearer

Do not create classes simply because everything can be represented as an object.

## Types

When type hints are used or appropriate, verify that they accurately describe values.

Check:
- Incorrect annotations
- Missing useful annotations
- Overly broad types
- Incorrect `Optional` usage
- Inconsistent return types
- Misleading generic types

Prefer:
```python
users: list[User]
```

over:
```python
users: list
```

Do not add type hints mechanically when they provide little value.

## Error Handling

Avoid broad exception suppression:

```python
try:
    ...
except Exception:
    pass
```

unless there is a deliberate, documented reason.

Check:
- Correct exception boundary
- Specific exception types
- Whether errors should be propagated
- Whether useful context is preserved
- Whether errors are silently swallowed

## Python Idioms

Prefer idiomatic Python when it improves clarity.

Prefer:
```python
for user in users:
    ...
```

over unnecessary index-based iteration.

Prefer:
```python
if users:
    ...
```

over:
```python
if len(users) > 0:
    ...
```

Prefer context managers:
```python
with open(path) as file:
    ...
```

Do not apply idioms mechanically if they reduce readability.

## Constants

Use `UPPER_SNAKE_CASE` for meaningful application-level constants:

```python
MAX_RETRIES = 3
DEFAULT_TIMEOUT = 30
```

Do not turn every literal into a constant. Promote values when their meaning, reuse, configuration, or domain significance makes that useful.

## Documentation

Document:
- Public APIs
- Complex algorithms
- Non-obvious business rules
- Important side effects
- External integrations
- Configuration requirements

Avoid comments that merely restate the code.

Good comments explain why, not what.

## Dead Code and Redundancy

Identify:
- Unused variables
- Unreachable code
- Duplicate logic
- Redundant conditions
- Redundant conversions
- Unnecessary wrappers
- Unused functions
- Obsolete commented-out code

Do not remove unusual code without establishing that it is actually unnecessary.

## Maintainability

Consider how another developer would modify the code later.

Look for:
- Hidden coupling
- Excessive complexity
- Global mutable state
- Magic values
- Deep nesting
- Long functions
- Large classes
- Unclear dependencies
- Leaky abstractions
- Inconsistent patterns

Prefer straightforward code over clever code.

## Severity

Use these levels:

### CRITICAL
Incorrect, unsafe, or fundamentally broken behavior.

Examples:
- Data corruption
- Security issue
- Incorrect business logic
- Broken critical contract

### HIGH
Likely to cause bugs or significant maintenance problems.

Examples:
- Incorrect semantic behavior
- Wrong return type
- Broken abstraction
- Circular dependency
- Major error-handling problem

### MEDIUM
Works but has meaningful design or maintainability problems.

Examples:
- Misleading naming
- Poor module boundaries
- Significant coupling
- Significant duplication

### LOW
Minor improvement.

Examples:
- Small naming refinement
- Minor idiomatic improvement
- Small readability issue

Do not report cosmetic issues as high severity.

## Review Process

When reviewing Python code:

1. Understand intended behavior.
2. Identify domain concepts.
3. Validate names against those concepts.
4. Validate behavior against intent.
5. Check module/package boundaries.
6. Check imports and dependencies.
7. Check types and contracts.
8. Check error handling.
9. Check Python idioms.
10. Check maintainability.
11. Report only actionable findings.

Do not rewrite working code unnecessarily.

## Output Format

For findings, use:

```text
[SEVERITY] Issue
Location: <file>:<line>

Problem:
<what is wrong>

Why:
<why it matters>

Recommendation:
<specific change>
```

If there are no meaningful issues, say:

```text
No significant semantic, structural, or Python-quality issues found.
```

Do not invent problems simply to produce findings.

## Core Rule

Validate meaning before style.

Perfect formatting does not make code good Python if its names, abstractions, structure, or behavior do not accurately represent its intent.
