---
title: SPX
subtitle: Spec-Driven Development for AI Agents
author: Simon Heimlicher
date: 2025-01-01T00:00:00+0100
description: SPX - Fast, deterministic workflow management for spec-driven development with Claude Code
genre: Developer Tools
keywords:
  - spx
  - spec-driven development
  - claude code
  - ai agents
  - workflow management
lastmod: 2025-01-16
aliases:
  - /home/
build:
  publishResources: false
cascade:
  - build:
      publishResources: false
---

## What is SPX?

{{% lede-initial %}}SPX is a framework for **Spec-Driven Development** — a methodology that combines fast, deterministic CLI tooling with Claude Code plugins to streamline AI-assisted development workflows.{{% /lede-initial %}}

### The Problem

When working with AI coding assistants, checking the status of work items typically requires expensive LLM calls that take 1-2 minutes and consume tokens. This creates friction in the development loop.

### The Solution

SPX provides:

- **spx CLI**: Instant status checks in under 100ms with zero token cost
- **SPX-Claude Marketplace**: Pre-built Claude Code plugins for testing, coding, and documentation workflows

{{< panel page="/cli" float=left relativewidth=45 >}}

### Fast CLI Tooling

The `spx` command-line tool scans your `specs/` directory and provides instant, deterministic status analysis of capabilities, features, and stories.

```bash
spx status
spx next
spx session handoff
```

{{< /panel >}}

{{< panel page="/marketplace" float=right relativewidth=45 >}}

### Claude Code Plugins

The SPX-Claude marketplace provides skills and commands for TypeScript, Python, testing, specifications, and productivity workflows.

```bash
claude plugin marketplace add simonheimlicher/spx-claude
claude plugin install core@spx-claude
```

{{< /panel >}}

## Get Started

Install the CLI and marketplace to begin using Spec-Driven Development:

```bash
# Install spx CLI
git clone https://github.com/simonheimlicher/spx-cli.git
cd spx-cli && npm install && npm run build && npm link

# Add Claude Code marketplace
claude plugin marketplace add simonheimlicher/spx-claude
claude plugin install core@spx-claude
```
