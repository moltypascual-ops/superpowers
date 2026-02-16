# OpenClaw-Adapted Skills

This directory contains skills from the [Superpowers](https://github.com/vissanum/superpowers) framework, adapted for use with [OpenClaw](https://github.com/openclaw/openclaw).

## Overview

These skills have been converted from Claude Code's format to OpenClaw's skill structure:
- Frontmatter adapted to OpenClaw format with `metadata.openclaw.emoji`
- Tool references mapped: `Bash` → `exec`, `Task` → `sessions_spawn`, `Skill` → file references
- Removed Claude Code-specific features (hooks, plugins, `@` syntax)
- Maintained all core methodology and content

## Skills Included (13 total)

### High Priority
| Skill | Emoji | Description |
|-------|-------|-------------|
| `systematic-debugging` | 🔍 | Debugging methodology with 4-phase approach |
| `test-driven-development` | 🧪 | Strict TDD with red-green-refactor cycle |
| `brainstorming` | 💡 | Design before implementation |
| `subagent-driven-development` | 🤖 | Execute plans with fresh subagent per task |
| `verification-before-completion` | ✅ | Evidence before claims |

### Medium Priority
| Skill | Emoji | Description |
|-------|-------|-------------|
| `writing-plans` | 📝 | Create comprehensive implementation plans |
| `finishing-a-development-branch` | 🔀 | Complete work with merge/PR options |
| `requesting-code-review` | 👀 | Request reviews at checkpoints |
| `writing-skills` | 🛠️ | Create new skills with TDD approach |

### Low Priority
| Skill | Emoji | Description |
|-------|-------|-------------|
| `executing-plans` | ▶️ | Execute plans in batches with checkpoints |
| `dispatching-parallel-agents` | ⚡ | Parallel investigation of independent issues |
| `using-git-worktrees` | 🌳 | Isolated workspaces with git worktrees |
| `using-skills` | 📚 | Meta-skill for skill discovery and usage |

## Tool Mapping Reference

| Claude Code | OpenClaw |
|-------------|----------|
| `Skill` tool | Read `skills/{name}/SKILL.md` |
| `TodoWrite` | No equivalent (use comments) |
| `Task` | `sessions_spawn` |
| `Bash` | `exec` |
| `Read` | `read` |
| `Write` | `write` |
| `Edit` | `edit` |

## Installation

Copy any skill directory to your OpenClaw skills folder:
```bash
cp -r openclaw-skills/{skill-name} /path/to/openclaw/skills/
```

## Skill Dependencies

Many skills reference each other. Recommended installation order:
1. `systematic-debugging` (core debugging)
2. `test-driven-development` (core development)
3. `verification-before-completion` (quality gate)
4. Remaining skills as needed

## Original Source

These skills are adapted from [Superpowers v4.3.0](https://github.com/vissanum/superpowers) by Jesse Dickey.

## License

MIT License (same as original Superpowers)
