# Business Documentation

Business analysis for VegyScan - Product vision, user research, and requirements.

## Documents

- **[vision.md](./vision.md)** - Product vision, goals, problem statement, and strategic scope
- **[personas.md](./personas.md)** - User personas with demographics, needs, and behaviors
- **[constraints-assumptions.md](./constraints-assumptions.md)** - Project constraints and assumptions
- **[risks.md](./risks.md)** - Risk analysis and mitigation strategies
- **[use-cases/](./use-cases/)** - Detailed use case scenarios and workflows
- **[user-stories/](./user-stories/)** - Agile user stories grouped by epics
- **[requirements/](./requirements/)** - Functional and non-functional requirements

## Purpose

This directory contains all **WHAT** and **WHY** documentation from the user perspective:

- **WHAT** problems do users have?
- **WHY** are we building VegyScan?
- **WHAT** features must the product have?
- **WHAT** quality attributes are required?
- **HOW** do users interact with features? (workflows)

## Quick Navigation

### Understanding the Users
Start with [personas.md](./personas.md) to meet the 7 target user personas, each representing different dietary needs and use cases.

### Understanding the Vision
Read [vision.md](./vision.md) to understand:
- The problem VegyScan solves
- Product vision and strategic goals
- What's in scope and out of scope
- Success metrics

### Understanding User Interactions
Browse [use-cases/](./use-cases/) to see detailed workflows:
- How users scan and analyze menus
- Error handling and edge cases
- Integration points (camera, GPS, share extension)

### Understanding Requirements
Check [requirements/](./requirements/) for:
- [functional.md](./requirements/functional.md) - What features the app must have
- [non-functional.md](./requirements/non-functional.md) - Quality attributes (performance, UX, security, cost constraints)
- [error-handling.md](./requirements/error-handling.md) - Error message library

### Understanding User Stories
See [user-stories/stories.md](./user-stories/stories.md) for agile user stories that connect personas, use cases, and requirements.

## Single Source of Truth

This directory is the authoritative source for:
- User personas → `personas.md`
- Product vision → `vision.md`
- Functional requirements → `requirements/functional.md`
- Non-functional requirements → `requirements/non-functional.md`
- User workflows → `use-cases/UC-*.md`
- User value propositions → `user-stories/stories.md`

**Architecture and technical decisions belong in `/docs/architecture/`, not here.**

## For AI/Agents

See [`.claude.md`](./.claude.md) for detailed working instructions on:
- Single Source of Truth principles
- What belongs in each file
- Update workflows
- Domain separation (business vs. architecture)
