# Requirements

Functional and non-functional requirements for VegyScan.

## Documents

- **[functional.md](./functional.md)** - What the app must do (features and capabilities)
- **[non-functional.md](./non-functional.md)** - How well it must do it (performance, UX, security, cost constraints)
- **[error-handling.md](./error-handling.md)** - Error message library and handling patterns

## Purpose

Requirements are the **Single Source of Truth** for:
- **WHAT** features the system must have
- **WHAT** quality attributes it must meet
- **WHAT** constraints it must respect

## Functional vs. Non-Functional

### Functional Requirements (`functional.md`)

Define **WHAT** the system must do:
- Feature capabilities
- User interactions
- Data processing
- System behaviors
- Integration points

**Example:** "REQ-F-032: System shall support uploading photos from device library"

### Non-Functional Requirements (`non-functional.md`)

Define **HOW WELL** the system must perform:
- Performance (speed, latency, throughput)
- Usability (UX patterns, accessibility)
- Security (data protection, privacy)
- Cost constraints (API budgets, infrastructure limits)
- Compliance (GDPR, accessibility standards)
- Reliability (uptime, error rates)

**Example:** "REQ-NF-005: OCR processing shall complete within 3 seconds for standard menus"

## Relationship to Other Documents

Requirements are **complementary** to:

- **User Stories** ([`../user-stories/`](../user-stories/)): WHY users need features (value)
- **Requirements** (this directory): WHAT features and quality attributes
- **Use Cases** ([`../use-cases/`](../use-cases/)): HOW users interact (workflows)
- **ADRs** ([`../../architecture/adr/`](../../architecture/adr/)): WHY we chose technologies (technical decisions)

### Single Source of Truth Principle

**Requirements are the SoT for all feature specifications.**

- ✅ Requirements define WHAT features exist
- ✅ Use cases describe HOW users use those features
- ✅ User stories explain WHY those features matter
- ❌ DO NOT duplicate feature lists in vision.md or elsewhere

**Update workflow:**
1. New feature needed? → Add to `functional.md` first
2. Quality attribute needed? → Add to `non-functional.md`
3. Other docs reference requirements (link, don't copy)

## Naming Convention

Requirements use a hierarchical ID system:

- **REQ-F-XXX**: Functional requirements
- **REQ-NF-XXX**: Non-functional requirements

IDs are sequential within each category and must be unique.

## For AI/Agents

See [`../.claude.md`](../.claude.md) for detailed working instructions on:
- Single Source of Truth principles
- When to update requirements vs. other docs
- Domain separation (business vs. architecture)
