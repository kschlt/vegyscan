# VegyScan Documentation

Central documentation for VegyScan - Business Analysis, Architecture, and Decisions.

## Structure

- **[business-case/](./business-case/)** - Market analysis, competitive landscape, business model, feasibility studies
- **[business/](./business/)** - Product vision, use cases, requirements, user stories, and personas
- **[architecture/](./architecture/)** - Technical decisions (ADRs), system diagrams, and tech stack
- **[decisions/](./decisions/)** - Chronological decision log

## Quick Start

1. **Business Foundation** → [business-case/](./business-case/) - Market validation, competitor analysis, business model
2. **Product Vision** → [business/vision.md](./business/vision.md) - Understand the product vision and goals
3. **User Research** → [business/personas.md](./business/personas.md) - Meet the target users
4. **Use Cases** → [business/use-cases/](./business/use-cases/) - See how users interact with features
5. **Requirements** → [business/requirements/](./business/requirements/) - Functional and non-functional requirements
6. **Architecture** → [architecture/adr/](./architecture/adr/) - Technical decisions
7. **Tech Stack** → [architecture/overview.md](./architecture/overview.md) - Technology choices

## For AI/Agents

See `.claude.md` files in each directory for specific working instructions and Single Source of Truth principles.

## Documentation Layers

```
STRATEGIC LAYER (Pre-Project)
/docs/business-case/
├─ Market validation and sizing
├─ Competitive positioning
├─ Business model and monetization
└─ Feasibility assessment
         ↓ Informs & Validates

PRODUCT LAYER
/docs/business/
├─ User needs and personas
├─ Product vision and goals
├─ Requirements and features
└─ Use cases and user stories
         ↓ Defines WHAT to build

SOLUTION LAYER
/docs/architecture/
├─ Technical decisions (ADRs)
├─ System design and diagrams
└─ Technology choices
         ↓ Defines HOW to build

DECISION TRACKING
/docs/decisions/
└─ Chronological record of all decisions
```

## Principles

### Single Source of Truth (SoT)

Each piece of information has exactly ONE authoritative location. Other documents reference the SoT, never duplicate it.

**Key Sources of Truth:**
- **Market & Strategy** → `business-case/`
- **User needs** → `business/personas.md`
- **Product vision** → `business/vision.md`
- **Features** → `business/requirements/functional.md`
- **Quality attributes** → `business/requirements/non-functional.md`
- **User workflows** → `business/use-cases/`
- **Technical decisions** → `architecture/adr/`
- **System design** → `architecture/diagrams/`

### Update Workflow

1. Identify the Single Source of Truth for the information
2. Update only that document
3. Other documents link to it (never copy)
4. Verify consistency across references

See [`.claude.md`](./.claude.md) for detailed AI working instructions.
