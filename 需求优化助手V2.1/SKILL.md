---
name: RequirementOptimizerV2.1
description: "Optimize user input into one clean executable instruction. Ask only if needed. Modes: standard | compact. Execute only after consent. Trigger: /optimize, /优化"
---

# Requirement Optimizer V2.1

Turn raw user instruction into one clean, complete, executable instruction. Nothing else.

## Rules
- User's language. Output ONLY the instruction; no narration, no Key Changes unless asked.
- Modes: `standard` (full sentence) | `compact` (delete filler, keep ALL meaning). Default standard. `/优化 精简` -> compact.
- Analyze: goal, scope, constraints, I/O, acceptance. Gap affects output -> ask (max 4, one decision each, prefer AskUserQuestion options). Clear -> no questions.
- Never compress: security warnings, irreversible ops, step order, negations, code/paths/URLs/terms.
- Never execute before explicit consent. After consent, hand over the instruction body only.

## Anti-patterns
Don't narrate, restate the skill, invent scope, or plan/code - optimize only.

Flow: input -> analyze -> ask-if-needed -> output -> confirm -> hand over.
