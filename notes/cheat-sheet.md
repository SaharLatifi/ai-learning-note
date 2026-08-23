# 🤖 Claude Code Cheat Sheet

## 🔄 Modes

Press `Shift + Tab` to switch modes.

- **Approval:** Approve file edits and commands.
- **Auto-Accept:** File edits are automatic; commands require approval.
- **Plan:** Claude explores and creates a plan without editing files.

---

## 🔁 Workflow

**Explore → Plan → Code → Commit**

1. Understand the codebase.
2. Review the implementation plan.
3. Implement and test the changes.
4. Review, commit and push.

---

## ⌨️ Commands

| Command | Purpose |
|---|---|
| `/context` | Check context usage |
| `/compact` | Summarize the session and free context |
| `/clear` | Start a fresh session |
| `/init` | Create `CLAUDE.md` |
| `/agents` | Manage subagents |
| `/mcp` | Manage MCP servers |
| `/hooks` | Configure hooks |
| `/commit-push-pr` | Commit, push and create a PR |
| `claude --from-pr <PR_NUMBER>` | Resume a PR session |

---

## 🛠️ Customization

| Feature | Purpose |
|---|---|
| `CLAUDE.md` | Persistent project instructions |
| **Subagents** | Handle focused tasks in separate contexts |
| **Skills** | Load reusable instructions when relevant |
| **MCP** | Connect Claude to external tools and data |
| **Hooks** | Automatically enforce required actions |

---

## 🔍 Quick Rules

- Use **Plan Mode** before complex changes.
- Use `/compact` for the same feature and `/clear` for a new one.
- Store general project rules in `CLAUDE.md`.
- Use subagents for exploration and unbiased reviews.
- Use Skills for repeated task-specific instructions.
- Disable unused MCP servers to preserve context.
- Use Hooks for actions that must always happen.
