---
title: Concepts
subtitle: Understanding Spec-Driven Development
description: Core concepts and methodology behind SPX and spec-driven development
date: 2025-01-01T00:00:00+0100
lastmod: 2025-01-16
keywords:
  - spec-driven development
  - methodology
  - concepts
  - workflow
---

## What is Spec-Driven Development?

Spec-Driven Development (SDD) is a methodology for managing AI-assisted development workflows. It provides structure and determinism to the inherently fluid process of working with AI coding assistants.

### Core Principles

1. **Specifications as Source of Truth**: Work items are defined in structured markdown files organized in a `specs/` directory hierarchy.

2. **Deterministic Status**: Item status (OPEN, IN PROGRESS, DONE) is determined by filesystem state, not LLM interpretation.

3. **Hierarchical Organization**: Work is organized into capabilities → features → stories, enabling clear scope and progress tracking.

4. **Session Continuity**: Context handoffs enable seamless work continuation across sessions and agents.

## Work Item Hierarchy

```
Capability
└── Feature
    └── Story
        └── Tests
```

- **Capability**: A high-level business capability (e.g., "Core CLI")
- **Feature**: A specific feature within a capability (e.g., "Pattern Matching")
- **Story**: An implementable unit of work (e.g., "Parse capability names")
- **Tests**: Verification that the story is complete

## Status Determination

Status flows from the filesystem, providing instant, deterministic classification:

| State           | Condition                                      |
| --------------- | ---------------------------------------------- |
| **OPEN**        | No `tests/` directory, or empty `tests/`       |
| **IN PROGRESS** | `tests/` directory has files, but no `DONE.md` |
| **DONE**        | `tests/DONE.md` exists                         |

This simple convention means status checks take milliseconds, not minutes.

## BSP Numbering

Work items use Binary Space Partitioning numbers for easy ordering and insertion:

```
21, 32, 43, 54, 65, 76, 87...
```

To insert between 21 and 32, use 27 (midpoint). This allows unlimited insertion without renumbering.

## Directory Structure

```
project/
├── specs/
│   ├── backlog/          # Future work
│   ├── doing/            # Active work
│   │   └── capability-21_core-cli/
│   │       ├── core-cli.capability.md
│   │       └── feature-21_pattern-matching/
│   │           ├── pattern-matching.feature.md
│   │           └── story-21_parse-names/
│   │               ├── parse-names.story.md
│   │               └── tests/
│   │                   └── DONE.md
│   └── done/             # Completed work
└── .spx/
    └── sessions/         # Handoff sessions
```

## Session Management

Sessions enable context preservation across work boundaries:

1. **Handoff**: Save current context with priority
2. **Pickup**: Resume the highest-priority session
3. **Release**: Return session to queue without completing

This creates a priority queue of work items that agents can pick up and continue.

## Integration with Claude Code

The SPX-Claude marketplace provides plugins that understand this structure:

- `/handoff` command creates sessions
- `/pickup` command resumes sessions
- Skills like `/coding-typescript` follow the spec structure
- `/writing-prd` and `/writing-trd` create specifications

Together, the CLI and plugins form a complete workflow for AI-assisted development.
