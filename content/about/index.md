---
title: About SPX
subtitle: Spec-Driven Development Framework
description: About the SPX framework for spec-driven development with Claude Code
keywords:
  - spx
  - about
  - spec-driven development
  - open source
lastmod: 2025-01-16
section: About
weight: 10
---

## The Project

SPX is an open-source framework for **Spec-Driven Development** — a methodology designed to bring structure, speed, and determinism to AI-assisted development workflows.

The framework consists of two main components:

### spx CLI

A fast, deterministic command-line tool that:

- Scans `specs/` directories for work item status
- Provides instant (<100ms) status checks without LLM calls
- Manages work sessions for context handoffs between agents

**Repository**: [github.com/simonheimlicher/spx-cli](https://github.com/simonheimlicher/spx-cli)

### SPX-Claude Marketplace

A Claude Code plugin marketplace providing:

- Pre-built skills for TypeScript and Python development
- Commands for git workflows and context management
- Testing and specification writing guidance

**Repository**: [github.com/simonheimlicher/spx-claude](https://github.com/simonheimlicher/spx-claude)

## Why Spec-Driven Development?

When working with AI coding assistants, several challenges emerge:

1. **Status checks are slow**: Asking an LLM to check work status takes 1-2 minutes and consumes tokens
2. **Context is lost**: Work sessions don't naturally persist between conversations
3. **Workflow is ad-hoc**: Without structure, AI-assisted development can become chaotic

SPX addresses these challenges by:

- Making status determination instant and deterministic via filesystem conventions
- Providing session management for context continuity
- Establishing clear hierarchies (capabilities → features → stories)

## Contributing

SPX is open source under the MIT license. Contributions are welcome:

1. Report issues on GitHub
2. Submit pull requests
3. Share feedback and ideas

## Author

SPX is created and maintained by [Simon Heimlicher](https://simon.heimlicher.com/about).

## License

MIT License — see the repositories for full license text.
