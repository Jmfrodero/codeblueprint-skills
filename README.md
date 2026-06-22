# CodeBlueprint — AI Agent Skills

Premium skill packs for AI coding agents: Hermes Agent, Claude Code, Cursor, Windsurf, and more.

## Available Skills

### 🏗️ DevOps Architecture Kit
**10 ADRs, 5 RFCs, 5 Runbooks, 4 Team Templates, 3 Guides, 7 AI Prompts**

Generate Architecture Decision Records, RFCs, production runbooks, and team documentation from context.

→ [Buy on Gumroad — €29](https://codeblueprint.gumroad.com/l/devops-architecture-documentation-kit)

**Install:**
```bash
# Hermes Agent
mkdir -p ~/.hermes/skills && curl -fsSL https://raw.githubusercontent.com/Jmfrodero/codeblueprint-skills/main/devops-architecture-kit.md -o ~/.hermes/skills/devops-architecture-kit.md

# Claude Code
# Copy the SKILL.md content to your .claude/skills/ directory
```

---

### 🎯 System Design Interview Kit
**20 Case Studies, 4S Framework, Capacity Formulas, 10+ AI Simulation Prompts**

A complete toolkit for acing system design interviews at top tech companies.

→ [Buy on Gumroad — €29](https://codeblueprint.gumroad.com/l/system-design-interview-kit)

**Install:**
```bash
# Hermes Agent
curl -fsSL https://raw.githubusercontent.com/Jmfrodero/codeblueprint-skills/main/system-design-interview.md -o ~/.hermes/skills/system-design-interview.md

# Claude Code
# Copy the SKILL.md content to your .claude/skills/ directory
```

---

### 💰 Freelancer Finance Spain
**Income tracking, IVA/IRPF, Modelo 303, Spanish tax calendar**

Manage your freelancer finances in Spain with AI-powered templates and prompts.

→ [Buy on Gumroad — €19](https://codeblueprint.gumroad.com/l/freelancer-finance-toolkit-spain-eu)

**Install:**
```bash
# Hermes Agent
curl -fsSL https://raw.githubusercontent.com/Jmfrodero/codeblueprint-skills/main/freelancer-finance-spain.md -o ~/.hermes/skills/freelancer-finance-spain.md
```

---

## Skill Format

Each skill is a self-contained `SKILL.md` file with:
- YAML frontmatter (metadata)
- Trigger conditions (when to use)
- Full templates and frameworks
- AI prompts for generation
- Usage examples

Compatible with any LLM-based agent that reads markdown files.

## License

MIT License — Free for personal and commercial use.
