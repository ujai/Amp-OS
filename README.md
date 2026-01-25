# Amp-OS

> Spec-driven development workflows for AI coding assistants.

## The Problem

AI coding assistants are powerful, but they have issues:

1. **They jump straight to code.** No planning, no spec, just code. This leads to rework and missed requirements.

2. **Context gets messy.** Long sessions fill up with noise. The AI forgets what you decided earlier.

3. **No structure.** Every project is chaos. No consistent way to plan features, track tasks, or verify work.

4. **Different tools, different workflows.** Amp CLI works one way. OpenCode works another. You have to learn each from scratch.

## The Solution

Amp-OS gives you a **repeatable workflow** that works across tools:

```
Brainstorm → Plan → Spec → Tasks → Implement → Verify
```

Each phase has a dedicated skill/command that:
- Asks the right questions
- Produces standard documents
- Keeps context clean
- Enforces quality checks

**Result:** You get working code that matches what you actually wanted.

---

## Supported Platforms

| Platform | How it works |
|----------|--------------|
| **[Amp CLI](https://ampcode.com)** (Sourcegraph) | Skills loaded on demand |
| **[OpenCode](https://opencode.ai)** (SST) | Slash commands via oh-my-opencode |

---

## Installation

### One-line install

```bash
curl -fsSL https://raw.githubusercontent.com/ujai/Amp-OS/main/install.sh | bash
```

You'll pick your platform (Amp CLI or OpenCode).

### Manual install

```bash
git clone https://github.com/ujai/Amp-OS.git ~/Amp-OS
chmod +x ~/Amp-OS/scripts/*.sh
```

---

## Quick Start

### Amp CLI

```bash
# Add to your project
~/Amp-OS/scripts/amp-project-install.sh /path/to/your-project

# In Amp, load a skill:
"Load amp-os-plan-product to create a roadmap"
```

### OpenCode

```bash
# Requires oh-my-opencode first (see OpenCode Setup below)
~/Amp-OS/scripts/opencode-project-install.sh /path/to/your-project

# In OpenCode, use slash commands:
/plan-product
```

---

## The Workflow

Both platforms use the same phases:

| Phase | What it does | Amp CLI | OpenCode |
|-------|--------------|---------|----------|
| **Brainstorm** | Refine vague ideas into clear designs | `amp-os-brainstorm` | - |
| **Plan** | Create roadmap with milestones | `amp-os-plan-product` | `/plan-product` |
| **Shape** | Research requirements | `amp-os-shape-spec` | `/shape-spec` |
| **Write** | Write detailed specification | `amp-os-write-spec` | `/write-spec` |
| **Tasks** | Break spec into task groups | `amp-os-create-tasks` | `/create-tasks` |
| **Implement** | Build with tests first (TDD) | `amp-os-implement-tasks` | `/implement` |
| **Verify** | Check everything works | `amp-os-verify-implementation` | `/verify` |

---

## Examples

### New Project

Building something from scratch? Use the full workflow.

**Example: SaaS invoicing app**

```
1. Plan the product     → Creates roadmap.md with milestones
2. Shape "user-auth"    → Researches auth patterns, creates requirements
3. Write spec           → Detailed spec with API contracts, data models
4. Create tasks         → Breaks into implementable chunks
5. Implement            → TDD: tests first, then code
6. Verify               → Runs tests, generates report
```

### Existing Project

Adding a feature to existing code? Skip planning, start with shaping.

```
1. Shape "stripe-billing"  → Analyzes existing patterns
2. Write spec              → References current code
3. Create tasks            → Small, non-breaking changes
4. Implement               → Follows existing conventions
5. Verify                  → No regressions
```

### Quick Reference

| Scenario | Start at |
|----------|----------|
| New product | `plan-product` |
| New feature | `shape-spec` |
| Bug fix | Just fix it (load standards first) |
| Refactoring | `shape-spec` |
| Research only | `shape-spec` |

---

## What Gets Installed

After running the installer, your project gets:

```
your-project/
├── AGENTS.md              # Project context for AI
├── amp-os/                # (or opencode-os/)
│   ├── config.yml         # Project settings
│   ├── product/
│   │   └── roadmap.md     # Your product roadmap
│   ├── specs/             # Feature specs go here
│   │   └── [feature]/
│   │       ├── spec.md
│   │       └── tasks.md
│   └── templates/         # Document templates
└── .claude/
    └── skills/            # Symlinked skills (Amp CLI)
```

---

## Available Skills (Amp CLI)

| Category | Skills |
|----------|--------|
| **Workflow** | `brainstorm`, `plan-product`, `shape-spec`, `write-spec`, `create-tasks`, `implement-tasks`, `verify-implementation` |
| **Quality** | `spec-verifier`, `implementation-verifier` |
| **Standards** | `standards-global`, `standards-backend`, `standards-frontend`, `standards-testing` |
| **Utility** | `architecture-diagrams`, `code-analysis`, `handoff`, `workflow-orchestrator` |

Load any skill by asking Amp:
```
"Load amp-os-write-spec for the payment feature"
```

---

## OpenCode Setup

OpenCode requires **oh-my-opencode** plugin first:

```bash
# Add to ~/.config/opencode/opencode.json:
{ "plugin": ["oh-my-opencode"] }

# Then run opencode to initialize
opencode
```

See: [oh-my-opencode documentation](https://github.com/code-yeongyu/oh-my-opencode)

### Available Commands

| Command | Purpose |
|---------|---------|
| `/plan-product` | Create product roadmap |
| `/shape-spec` | Research requirements |
| `/write-spec` | Write specification |
| `/create-tasks` | Break into tasks |
| `/implement` | TDD implementation |
| `/verify` | Final verification |
| `/verify-spec` | Check spec quality |
| `/task-status` | Show progress |

---

## Thread Management (Amp CLI)

Long sessions get messy. Keep things clean:

1. **One task per thread.** Start a new thread for each task group.
2. **Use handoffs.** The `handoff` skill creates a summary to pass to the next thread.
3. **Reference, don't repeat.** Use `@@thread-name` to pull context from other threads.

**Hub-and-Spokes Pattern:**
```
       [Planning Thread]
              │
    ┌─────────┼─────────┐
    ▼         ▼         ▼
[Backend]  [Frontend]  [Tests]
```

---

## Updating

### Symlinked installs (default)

Skills update automatically when you pull:
```bash
cd ~/Amp-OS && git pull
```

### Copied installs

Re-run the installer:
```bash
~/Amp-OS/scripts/amp-project-update.sh /path/to/project
```

---

## Configuration

### Master config (`~/Amp-OS/config.yml`)

```yaml
version: 2.0.0
profile: default
use_symlinks: true        # false = copy files instead
```

### Project config (`amp-os/config.yml`)

```yaml
project_name: "My Project"
tech_stack: ["node", "react", "postgres"]
standards:
  global: true
  backend: true
  frontend: true
  testing: true
```

---

## Credits

- [Amp CLI](https://ampcode.com) by Sourcegraph
- [OpenCode](https://opencode.ai) by SST
- [oh-my-opencode](https://github.com/code-yeongyu/oh-my-opencode) by code-yeongyu

## License

MIT
