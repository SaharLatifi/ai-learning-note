## 🔄 Explore → Plan → Code → Commit Workflow

This workflow helps Claude understand the project before writing code and reduces unnecessary corrections.

---

### 🔍 Explore

Claude reads the relevant files to understand the codebase and gather context.

Use an **Explore subagent** when you only want a general codebase summary without making changes.

---

### 📋 Plan

Press `Shift + Tab` to enter **Plan Mode**.

In Plan Mode, Claude:

- Uses read-only tools
- Explores the codebase
- Researches the implementation
- Creates a detailed plan
- Cannot edit files

Review the plan and ask Claude to revise anything that does not meet your requirements.

> The planning stage is the best time to correct the approach because no code has been written yet.

---

### 💻 Code

Approve the plan and allow Claude to implement it.

To improve the coding process:

- Define clear success criteria.
- Provide the necessary tools.
- Include a reliable test suite.
- Test and verify the final changes yourself.

> If Claude repeatedly encounters the same problem, ask it to document the solution in `CLAUDE.md`.

---

### ✅ Commit

Before committing:

1. Test the changes yourself.
2. Ask a code-review subagent to review the work with fresh context.
3. Fix any identified issues.
4. Ask Claude to generate a commit message in your preferred style.
5. Commit and push the changes.

---

### 🔹 Summary

- **Explore:** Understand the codebase and gather context.
- **Plan:** Create and review the implementation approach.
- **Code:** Implement, troubleshoot and test the solution.
- **Commit:** Review, commit and push the completed work.

---

## 🧠 Context Management

Context is Claude’s working memory. Messages, files, commands, tool calls and their results all use space in the **context window.**

---

### 🔹 Context Window

The **context window** is the limited amount of information Claude can hold during a session.

As Claude reads files, runs commands and receives messages, the available context space decreases.

---

### 📦 Context Compaction

When the context window approaches its limit, Claude automatically **compacts** it.

Compaction:

- Summarizes important information
- Removes unnecessary tool results
- Frees up context space
- May lose some details

---

### 🛠️ Context Commands

| Command | Purpose |
|---|---|
| `/context` | Shows the current context usage and its breakdown |
| `/compact` | Summarizes the current session and frees up space |
| `/clear` | Removes the current context and starts a fresh session |

---

### 🔄 When to Use Each Command

Use `/compact` when:

- You are continuing the same feature.
- The context window is becoming full.
- You still need Claude to remember the main details.

Use `/clear` when:

- You are starting a different feature.
- Previous work is no longer relevant.
- You want to prevent old context from influencing the new task.

> Add information Claude should remember across sessions to `CLAUDE.md`.

---

### 💡 Saving Context Space

- **Write specific prompts:** Clear instructions reduce unnecessary exploration and reasoning.
- **Manage MCP servers:** Disable servers unrelated to the current project because their tools may consume context.
- **Use Skills:** Skills load information only when needed instead of loading everything upfront.
- **Use subagents:** They work with separate context windows and return only their findings to the main agent.
- **Check context usage:** Run `/context` to identify what is consuming space.

---

### 🔹 Summary

- Context is Claude’s limited working memory.
- Use `/context` to inspect context usage.
- Use `/compact` to continue the same work with a summarized context.
- Use `/clear` before starting unrelated work.
- Store important long-term project information in `CLAUDE.md`.

---

## 🔍 Code Review

Claude Code provides built-in features that make the Git and pull-request workflow faster.

---

### 👀 Review with a Subagent

Before pushing a pull request, ask Claude to use a **subagent** to review the changes.

The subagent:

- Uses a separate context window.
- Reviews the code with fresh eyes.
- Avoids the bias of the main agent that wrote the code.
- Flags issues without editing files.

Restrict the code-reviewer subagent to **read-only tools**. Store its configuration in the repository so the entire team can use the same reviewer.

---

### 🚀 The `/commit-push-pr` Skill

Run the following skill to complete the entire pull-request workflow:

```text
/commit-push-pr
  
