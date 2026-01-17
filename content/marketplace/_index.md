---
title: SPX-Claude Marketplace
subtitle: Claude Code Plugins for Development Workflows
description: Pre-built skills and commands for testing, TypeScript, Python, and productivity
date: 2025-01-01T00:00:00+0100
lastmod: 2025-01-16
keywords:
  - claude code
  - plugins
  - marketplace
  - skills
  - commands
---

## Overview

The SPX-Claude marketplace is a collection of Claude Code plugins providing skills and commands for testing, Python and TypeScript development, specifications, and productivity.

## Quick Install

Add this marketplace and install plugins directly from GitHub:

```bash
# Add the marketplace
claude plugin marketplace add simonheimlicher/spx-claude

# Install plugins you want
claude plugin install core@spx-claude
claude plugin install test@spx-claude
claude plugin install typescript@spx-claude
claude plugin install python@spx-claude
claude plugin install specs@spx-claude
```

Now slash commands like `/commit`, `/handoff`, `/pickup` and skills like `/testing-typescript` are available in all your projects.

### Update Plugins

```bash
# Update this marketplace
claude plugin marketplace update spx-claude

# Or update all marketplaces
claude plugin marketplace update
```

## Available Plugins

### core

Productivity commands and skills.

| Type    | Name                  | Purpose                                 |
| ------- | --------------------- | --------------------------------------- |
| Skill   | `/committing-changes` | Commit message guidance                 |
| Command | `/commit`             | Git commit with Conventional Commits    |
| Command | `/handoff`            | Create timestamped context handoff      |
| Command | `/pickup`             | Load and continue from previous handoff |

### test

BDD testing methodology with three-tier testing (Unit, Integration, E2E).

| Type  | Name       | Purpose                         |
| ----- | ---------- | ------------------------------- |
| Skill | `/testing` | Foundational testing principles |

### typescript

Complete TypeScript development workflow.

| Type  | Name                                 | Purpose                            |
| ----- | ------------------------------------ | ---------------------------------- |
| Agent | `typescript-simplifier`              | Simplify code for maintainability  |
| Skill | `/testing-typescript`                | TypeScript-specific testing        |
| Skill | `/coding-typescript`                 | Implementation with remediation    |
| Skill | `/reviewing-typescript`              | Strict code review                 |
| Skill | `/architecting-typescript`           | ADR producer with testing strategy |
| Skill | `/reviewing-typescript-architecture` | ADR validator                      |

### python

Complete Python development workflow.

| Type    | Name                             | Purpose                            |
| ------- | -------------------------------- | ---------------------------------- |
| Command | `/autopython`                    | Autonomous implementation          |
| Skill   | `/testing-python`                | Python-specific testing patterns   |
| Skill   | `/coding-python`                 | Implementation with remediation    |
| Skill   | `/reviewing-python`              | Strict code review                 |
| Skill   | `/architecting-python`           | ADR producer with testing strategy |
| Skill   | `/reviewing-python-architecture` | ADR validator                      |

### specs

Requirements documentation and specification skills.

| Type  | Name                   | Purpose                            |
| ----- | ---------------------- | ---------------------------------- |
| Skill | `/writing-prd`         | Write product requirements         |
| Skill | `/writing-trd`         | Write technical requirements       |
| Skill | `/managing-specs`      | Set up specs directory structure   |
| Skill | `/understanding-specs` | Load context before implementation |

### frontend

Frontend design and styling.

| Type  | Name                  | Purpose                                |
| ----- | --------------------- | -------------------------------------- |
| Skill | `/designing-frontend` | Create distinctive frontend interfaces |

### code

Autonomous coding orchestration.

| Type  | Name                   | Purpose                            |
| ----- | ---------------------- | ---------------------------------- |
| Skill | `/coding-autonomously` | Autonomous implementation patterns |

### claude

Meta-skills for Claude Code plugin development.

| Type  | Name               | Purpose                    |
| ----- | ------------------ | -------------------------- |
| Skill | `/creating-skills` | Create maintainable skills |

## Build Your Own Marketplace

Want to create your own plugin marketplace? Fork the [spx-claude repository](https://github.com/simonheimlicher/spx-claude) as a starting point.

### Repository Structure

```
my-claude-plugins/
├── .claude-plugin/
│   └── marketplace.json          # Marketplace catalog
└── plugins/
    └── my-plugin/
        ├── .claude-plugin/
        │   └── plugin.json       # Plugin metadata and version
        ├── commands/
        │   └── my-command.md     # Slash commands
        └── skills/
            └── my-skill/
                └── SKILL.md      # Agent skills
```

| Concept         | What it is                                 |
| --------------- | ------------------------------------------ |
| **Skill**       | Agent guidance (SKILL.md files)            |
| **Command**     | Slash command (`/build` → `build.md`)      |
| **Plugin**      | Namespace grouping related skills/commands |
| **Marketplace** | Index pointing to plugins                  |
