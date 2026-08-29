# Four-host plugin packaging

Document Specialist ships as one directory that four clients can load.

| Client | Manifest | Skills path |
|--------|----------|-------------|
| Universal / Agent Plugins 1.0 | `plugin.json` | `skills/` plus repo-root `SKILL.md` (`"skills": "./"`) |
| Claude Code | `.claude-plugin/plugin.json` | repo root `SKILL.md` plus `skills/` |
| Grok Build | `.grok-plugin/plugin.json` | Claude layout, zero-config |
| Codex | `.codex-plugin/plugin.json` | `skills/` |
| Cursor | `.cursor-plugin/plugin.json` | `skills/` |

---

## Universal plugin.json

Root file. Schema `https://agent-plugins.org/schemas/1.0.0/plugin.schema.json`.

- `name`: `document-specialist`
- `skills`: `./`
- `extensions` point at host manifests so a client that understands reverse-domain extras can load hooks later

A client that only understands Agent Plugins 1.0 ignores `.claude-plugin/` and still loads `SKILL.md` (and `skills/documentation-specialist/SKILL.md` as a copy).

---

## Claude Code

`.claude-plugin/plugin.json` plus `.claude-plugin/marketplace.json` so the repo is its own marketplace.

```text
claude plugin marketplace add SpillwaveSolutions/document-specialist-skill
claude plugin install document-specialist
```

Grok Build also loads Claude plugins zero-config when `.claude-plugin/` exists.

---

## Grok Build

`.grok-plugin/plugin.json` and `.grok-plugin/marketplace.json`. Pin the marketplace, or rely on the Claude layout.

```text
skilz install SpillwaveSolutions_document-specialist-skill/documentation-specialist
```

---

## Codex

`.codex-plugin/plugin.json` sets `"skills": "./skills/"` (a single path string, not an array) and Codex `interface` metadata: display name, default prompts, category Productivity.

Default prompts:

- Write DESIGN_DOC.md for this repo using arc42.
- Create an architecture document with C4-style Mermaid.
- Reverse-engineer an SDD from this Spring Boot service.

---

## Cursor

`.cursor-plugin/plugin.json` mirrors the universal name and description. Optional `.cursor/rules` can point at `SKILL.md`.

---

## Design files in this repo

| Path | Role |
|------|------|
| `DESIGN_DOC.md` | arc42 SDD of Document Specialist itself |
| `references/templates/markdown/DESIGN_DOC.md` | arc42 SDD template |
| `references/templates/markdown/architecture.md` | Short C4 architecture template |
| `references/workflows/design-workflow.md` | Intent DESIGN |
| `references/examples/greenfield/ecommerce-sdd.md` | Greenfield few-shot |
| `references/examples/greenfield/architecture-doc.md` | Short-form few-shot |
| `references/examples/greenfield/ui-wireframes.md` | PlantUML Salt few-shot |
| `references/examples/brownfield/spring-boot-sdd.md` | Brownfield few-shot |
| `commands/write-sdd.md` | Slash command |
| `commands/write-architecture.md` | Slash command |
| `commands/write-wireframe.md` | Slash command |

---

## Install matrix

```text
# Skilz (30+ agents)
skilz install SpillwaveSolutions_document-specialist-skill/documentation-specialist

# Claude Code
claude plugin marketplace add SpillwaveSolutions/document-specialist-skill
claude plugin install document-specialist

# Codex
# enable the plugin from the Codex plugin UI, or copy into ~/.codex/plugins/

# Grok Build
# add the marketplace pin, or clone beside the project
```

After install, ask:

> Write DESIGN_DOC.md for this repository. Use Google docs style. Include Mermaid context, sequence, and ER figures. Add PlantUML Salt wireframes for every UI.

The agent should load `design-workflow.md`, the arc42 template, and one example, then emit `DESIGN_DOC.md`.
