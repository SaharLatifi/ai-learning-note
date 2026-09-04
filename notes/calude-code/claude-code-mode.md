## 🔄 Claude Code Modes



# Claude Code Permission Modes

| Mode | Config Value | What It Does | Best For |
|------|--------------|---------------|----------|
| **Manual** (default) | `default` | Prompts before every tool use; reads are auto-allowed | General development, learning Claude Code, sensitive code |
| **Plan** | `plan` | Read-only — Claude explores and proposes a plan, but writes/edits/shell commands are blocked outright | Understanding a new codebase, code review without risk |
| **Accept Edits** | `acceptEdits` | Auto-allows file edits and common filesystem commands (mkdir, mv, cp, etc.); shell commands like `npm test` or `git push` still prompt | Trusted projects, fast iteration without approving every file change |
| **Auto** | `auto` (needs `--enable-auto-mode` flag, Team+ plan, Sonnet 4.6/Opus 4.6) | A background classifier checks each action and auto-approves lower-risk ones, blocking risky/injected ones | Long refactoring sessions, reducing approval fatigue while keeping some safety net |
| **Bypass Permissions** ("YOLO mode") | `bypassPermissions` | Skips all prompts entirely — everything auto-approved | Isolated sandboxes only (Docker, VM), CI/CD pipelines — never on a main machine |

## Notes
- Cycle through modes with **Shift+Tab** during a session (Bypass Permissions may need an explicit flag/confirmation; orgs can disable it entirely).
- Even in Bypass mode, some actions are never auto-approved — e.g. tools requiring direct user interaction, or destructive `rm`/`rmdir` on critical paths.
- For day-to-day work (status line setup, dbt, etc.), **Manual** or **Accept Edits** are the sensible choices. Avoid Bypass Permissions on a main machine.


Use **Plan Mode** for:

- Complex or multi-step changes
- Safe code reviews
- Reviewing the approach before execution
