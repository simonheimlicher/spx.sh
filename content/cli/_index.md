---
title: spx CLI
subtitle: Fast, Deterministic Workflow Management
description: The spx command-line tool for instant status checks and session management
date: 2025-01-01T00:00:00+0100
lastmod: 2025-01-16
keywords:
  - spx
  - cli
  - command line
  - workflow management
---

## Overview

**spx** scans your project's `specs/` directory and provides instant status analysis of work items (capabilities, features, stories). It replaces slow, token-expensive LLM-based status checks with deterministic filesystem operations completing in under 100ms.

### Key Benefits

- **Fast**: Scan entire spec tree in <100ms vs 1-2 minutes with LLM
- **Deterministic**: Reliable DONE/IN PROGRESS/OPEN classification
- **Zero token cost**: No LLM calls for status checks
- **Multiple formats**: Text, JSON, Markdown, Table output

## Installation

### From GitHub

```bash
git clone https://github.com/simonheimlicher/spx-cli.git
cd spx-cli
npm install
npm run build
npm link  # Makes 'spx' available globally
```

### From npm (Coming Soon)

```bash
npm install -g spx
```

## Commands

### Status

Display project status with hierarchical tree view:

```bash
spx status              # Text output
spx status --json       # JSON for scripts/agents
spx status --format markdown
spx status --format table
```

Example output:

```
capability-21_core-cli [IN PROGRESS]
├── feature-21_pattern-matching [DONE]
│   ├── story-21_parse-capability-names [DONE]
│   ├── story-32_parse-feature-names [DONE]
│   └── story-43_parse-story-names [DONE]
├── feature-32_directory-walking [IN PROGRESS]
│   ├── story-21_recursive-walk [DONE]
│   └── story-32_pattern-filter [OPEN]
└── feature-43_status-determination [OPEN]
```

### Next

Find the next work item to tackle:

```bash
spx next
```

### Session Management

Manage work sessions for agent handoffs and task queuing:

```bash
# Create a handoff session
echo "# Implement feature X" | spx session handoff --priority high

# List all sessions
spx session list

# Claim the highest priority session
spx session pickup --auto

# Release session back to queue
spx session release

# Show session content
spx session show <session-id>

# Delete a session
spx session delete <session-id>
```

Sessions are stored in `.spx/sessions/` with priority-based ordering (high → medium → low) and FIFO within the same priority.

## Status Determination

Status is computed deterministically from the `tests/` directory:

| Condition                           | Status          |
| ----------------------------------- | --------------- |
| No `tests/` directory or empty      | **OPEN**        |
| `tests/` has files but no `DONE.md` | **IN PROGRESS** |
| `tests/DONE.md` exists              | **DONE**        |

## Work Item Structure

spx expects work items in `specs/doing/` following this pattern:

```
specs/doing/
└── capability-NN_{slug}/
    ├── {slug}.capability.md
    └── feature-NN_{slug}/
        ├── {slug}.feature.md
        └── story-NN_{slug}/
            ├── {slug}.story.md
            └── tests/
                └── DONE.md  # Present when complete
```

Numbers use BSP (Binary Space Partitioning) for easy insertion: start with 21, 32, 43... and insert between existing items.
