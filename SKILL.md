---
name: tactical-planner
description: "Decomposes high-level intent into a structured deployment manifest for multi-agent swarms."
version: 0.1.0
author: Ralph Hermes
---

# Tactical Planner Skill

## Purpose
The Tactical Planner is the 'Commanding Officer' logic. It transforms a single user directive (often via voice) into a machine-readable deployment plan, ensuring optimal resource allocation across local and high-reasoning models.

## Workflow
1. **Intent Analysis**: Identify the core objective and constraints.
2. **Task Decomposition**: Break the objective into a dependency graph of sub-tasks.
3. **Resource Mapping**: Assign each task a `Role` and a `Compute Tier` (Local vs. High-Reasoning).
4. **Manifest Generation**: Produce a `DEPLOYMENT_MANIFEST.md` for the Orchestrator.

## Implementation Rules
- **Always** prioritize local models (Ollama) for repetitive or low-complexity tasks to preserve compute/API credits.
- **Always** escalate complex logic or architectural decisions to the High-Reasoning tier.
- **Never** skip the dependency check; ensure sub-tasks are ordered correctly.
- **Output** must always be a valid Markdown manifest.

## Manifest Schema
Each task in the manifest MUST include:
- `id`: Unique task identifier.
- `description`: Clear, directive instruction for the subagent.
- `role`: The persona the agent should adopt.
- `compute_tier`: `local` or `high_reasoning`.
- `dependencies`: IDs of tasks that must complete first.
