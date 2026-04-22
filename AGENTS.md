# AGENTS.md

This repository contains specialized AI agent personalities organized by domain. Each agent is a markdown file with YAML frontmatter.

## Repository Structure

```
agency-agents/
├── engineering/          # Software development specialists
├── design/              # UX/UI and creative specialists
├── marketing/           # Growth and marketing specialists
├── sales/               # Sales and revenue specialists
├── product/             # Product management specialists
├── project-management/  # PM and coordination specialists
├── testing/             # QA and testing specialists
├── support/             # Operations and support specialists
├── spatial-computing/   # AR/VR/XR specialists
├── specialized/         # Unique specialists
├── finance/             # Financial specialists
├── game-development/    # Game dev specialists (Unity, Unreal, Godot, etc.)
├── academic/            # Academic research specialists
├── scripts/             # Conversion and installation scripts
└── integrations/         # Tool-specific converted files (gitignored)
```

## Agent File Format

Every agent file must follow this structure:

```markdown
---
name: Agent Name
description: One-line description of specialty
color: colorname or "#hexcode"
emoji: 🎯
vibe: One-line personality hook
---

# Agent Name

## 🧠 Your Identity & Memory
- Role, personality, memory, experience

## 🎯 Your Core Mission
- Primary responsibilities with deliverables

## 🚨 Critical Rules You Must Follow
- Domain-specific rules and constraints

## 📋 Your Technical Deliverables
- Concrete code examples and templates

## 🔄 Your Workflow Process
- Step-by-step methodology

## 💭 Your Communication Style
- Tone, voice, approach

## 🎯 Your Success Metrics
- Measurable outcomes with numbers
```

### Required Frontmatter Fields
- `name` - Agent name
- `description` - One-line specialty description
- `color` - Color name or hex code

### Optional Frontmatter Fields
- `emoji` - Icon for the agent
- `vibe` - Short personality description
- `services` - External service dependencies (name, url, tier)

## Adding or Modifying Agents

1. Create or edit agent file in appropriate category directory
2. Ensure frontmatter has required fields (name, description, color)
3. Include recommended sections: Identity, Core Mission, Critical Rules
4. Test agent in real scenarios before committing

## Validation

The repository has automated linting that runs on PRs:

```bash
# Run linter locally
./scripts/lint-agents.sh

# Lint specific files
./scripts/lint-agents.sh engineering/*.md
```

**Required checks:**
- Frontmatter must exist with `---` delimiters
- Required fields: `name`, `description`, `color`
- Body must have at least 50 words

**Warnings (non-blocking):**
- Missing recommended sections (Identity, Core Mission, Critical Rules)
- No section headers mapping to tool formats

## Conversion and Installation

### Convert agents to tool formats

```bash
# Convert all tools
./scripts/convert.sh

# Convert specific tool
./scripts/convert.sh --tool opencode

# Parallel conversion (faster)
./scripts/convert.sh --parallel
```

### Install to local tools

```bash
# Interactive installer (auto-detects tools)
./scripts/install.sh

# Install specific tool
./scripts/install.sh --tool opencode

# Non-interactive (for scripts)
./scripts/install.sh --no-interactive --tool all
```

**Important:** Generated integration files in `integrations/` are gitignored. Users run `convert.sh` locally after cloning.

## Tool-Specific Notes

### OpenCode
- Agents copied to `.opencode/agents/` in current directory
- Project-scoped - run from project root
- Color names resolved to hex via `resolve_opencode_color()`

### Claude Code
- Agents copied to `~/.claude/agents/`
- No conversion needed - uses source .md files directly

### GitHub Copilot
- Agents copied to `~/.github/agents/` and `~/.copilot/agents/`
- No conversion needed - uses source .md files directly

### Antigravity (Gemini)
- Each agent becomes a skill in `~/.gemini/antigravity/skills/agency-<slug>/`
- Format: `SKILL.md` with extended frontmatter

### Cursor
- Agents converted to `.mdc` rule files in `.cursor/rules/`
- Format includes description, globs, alwaysApply frontmatter

### Aider
- All agents combined into single `CONVENTIONS.md`
- Project-scoped - run from project root

### Windsurf
- All agents combined into single `.windsurfrules`
- Project-scoped - run from project root

### OpenClaw
- Agents split into `SOUL.md` (persona) and `AGENTS.md` (operations)
- Plus `IDENTITY.md` with emoji + name + vibe
- Installed to `~/.openclaw/agency-agents/`

### Qwen Code
- Supports `${variable}` templating in agent body
- Minimal frontmatter: name and description only
- Installed to `~/.qwen/agents/` or `.qwen/agents/`

### Kimi Code
- YAML agent spec with separate `system.md` file
- Installed to `~/.config/kimi/agents/`

## Section Classification for OpenClaw

The `convert.sh` script classifies sections into two groups:

**SOUL.md (persona):**
- Identity & Memory
- Learning & Memory
- Communication Style
- Critical Rules / Rules You Must Follow

**AGENTS.md (operations):**
- Core Mission
- Technical Deliverables
- Workflow Process
- Success Metrics
- Advanced Capabilities

## Agent Design Principles

1. **Strong Personality** - Distinct voice, not generic "helpful assistant"
2. **Clear Deliverables** - Concrete code examples and templates
3. **Success Metrics** - Specific, measurable outcomes with numbers
4. **Proven Workflows** - Step-by-step processes tested in real scenarios
5. **Learning Memory** - Pattern recognition and continuous improvement

## External Services

Agents may depend on external services when essential to their function:

1. Declare dependencies in frontmatter `services` field
2. Agent must stand on its own without the service
3. Don't duplicate vendor docs - reference them instead
4. Prefer services with free tiers for testing

## Common Pitfalls

- **Missing frontmatter** - Always include `---` delimiters and required fields
- **Vague descriptions** - Be specific about specialty and deliverables
- **No code examples** - Include real, runnable code samples
- **Overly broad scope** - Narrow, deep specialization works better
- **Forgetting to convert** - Run `convert.sh` after adding/modifying agents
- **Committing generated files** - Integration files are gitignored

## Testing Your Changes

1. Run linter: `./scripts/lint-agents.sh`
2. Convert to target format: `./scripts/convert.sh --tool <name>`
3. Install locally: `./scripts/install.sh --tool <name>`
4. Test agent in real scenarios
5. Verify frontmatter and structure match template

## CI/CD

The `.github/workflows/lint-agents.yml` workflow runs on PRs that modify agent files. It validates frontmatter and structure before allowing merge.

## Resources

- [README.md](README.md) - Full agent catalog and use cases
- [CONTRIBUTING.md](CONTRIBUTING.md) - Detailed contribution guidelines
- [examples/](examples/) - Example workflows and multi-agent scenarios