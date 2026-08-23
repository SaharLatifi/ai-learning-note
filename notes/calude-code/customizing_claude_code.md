# 🛠️ Customizing Claude Code

## 🧠 The `CLAUDE.md` File

The `CLAUDE.md` file provides Claude Code with persistent information about your project.

Claude automatically reads it at the beginning of each session and adds its contents to the context.

---

### The Problem It Solves

Without a `CLAUDE.md` file, Claude must repeatedly:

- Explore the codebase
- Identify dependencies
- Understand existing features
- Discover project conventions
- Make assumptions about how the project works

The `CLAUDE.md` file acts as an **onboarding guide** that helps Claude understand the project immediately.

---

### File Location

Place the file in the root directory of the project:

```text
project-root/
├── CLAUDE.md
├── README.md
└── src/
```

---

### Example

```markdown
# Project

This is a dbt analytics project using Snowflake.

Raw data is transformed through three layers:

- `staging`: Cleans and standardizes source data
- `intermediate`: Applies reusable business logic
- `marts`: Creates final dimensions, facts and reporting models

# Commands

- Install packages: `dbtf deps`
- Run all models: `dbtf run`
- Run tests: `dbtf test`
- Build the project: `dbtf build`
- Generate documentation: `dbtf docs generate`

# SQL Style

- Use lowercase SQL keywords.
- Use CTEs instead of deeply nested queries.
- Give CTEs descriptive names.
- Use `ref()` to reference dbt models.
- Use `source()` to reference source tables.
- Do not use `SELECT *` in final models.

# Modeling Conventions

- Prefix staging models with `stg_`.
- Prefix dimensions with `dim_`.
- Prefix facts with `fct_`.
- Define primary keys and tests in YAML files.
- Add descriptions to final models and important columns.

# Important Rules

- Do not include database credentials in the repository.
- Use environment variables for sensitive values.
- Run `dbtf build` before creating a pull request.
```

With this information, Claude already understands the project structure, dbt commands, SQL style, naming conventions and testing requirements.

---

### Project-Level and User-Level Files

- **Project-level `CLAUDE.md`:** Stored in the project root and shared with the team through version control.
- **User-level `CLAUDE.md`:** Stored in the user configuration folder and contains personal preferences that apply across projects.

Commit the project-level file to Git so everyone uses the same project instructions.

---

### Reference Project Documentation

Use `@` followed by a file path to tell Claude to read other project documentation:

```markdown
## Project Documentation

Read this file when you need more information: @README.md
```

---

### Save Repeated Corrections

If you repeatedly give Claude the same correction, ask it to save the rule in `CLAUDE.md`.

This prevents Claude from making the same mistake in future sessions.

---

### Create the File with `/init`

Consider starting without a `CLAUDE.md` file to identify which instructions and corrections Claude repeatedly needs.

When you are ready, run:

```text
/init
```

Claude will generate an initial `CLAUDE.md` file that you can review and improve.

---

### Summary

- `CLAUDE.md` gives Claude persistent project context.
- Keep it concise and focused on necessary information.
- Include the project stack, commands and coding conventions.
- Commit the project-level file so the team can use it.
- Store personal preferences in the user-level file.
- Add repeated corrections as new rules.
- Use `/init` to generate the initial file.

---
## 🤖 Subagents

Subagents allow Claude to delegate specific tasks to separate agents.

Each subagent:

- Has its own isolated context window.
- Focuses on a specific task.
- Can work in parallel with other agents.
- Returns a summary of its findings to the main agent.

---

### How Subagents Help

Tasks such as exploring a codebase, searching documentation or investigating an error can consume a large amount of context.

A subagent performs this work in a separate context window and returns only the relevant results. This keeps the main conversation focused on the current task.

For example, the main agent could ask a subagent to:

- Find where a dbt model is referenced.
- Explore the project folder structure.
- Research a Snowflake error.
- Review SQL transformations.
- Locate tests related to a particular model.

---

### Create a Subagent

Run:

```text
/agents
```

Then select:

```text
Create new agent
```

Claude will guide you through:

1. Choosing the agent’s scope
2. Defining its purpose
3. Selecting its available tools
4. Choosing its colour
5. Reviewing its generated name, description and instructions

The description also helps Claude determine when it should use the subagent.

---

### Subagent Configuration

Subagents are defined in Markdown files with YAML frontmatter.

A subagent can be configured with:

- A name and description
- Detailed instructions
- Specific tools
- Read-only or editing permissions
- Persistent memory
- Preloaded skills

> Give each subagent only the tools it needs. For example, a code-review subagent should normally use read-only tools.

---

### Persistent Memory

Persistent memory allows a subagent to retain useful information across conversations.

This can be helpful when the same subagent regularly works on the same project or type of task.

---

### Preload Skills

Add the `skills` key to the subagent configuration to preload specific skills.

Unlike skills used in the main conversation, a preloaded skill is added entirely to the subagent’s context.

Only preload skills that the subagent regularly needs.

---

### Summary

- Subagents handle focused tasks in separate context windows.
- They keep unnecessary exploration out of the main context.
- They can work in parallel and return summarized findings.
- Use `/agents` to create and manage them.
- Limit their tools and skills to what their assigned tasks require.

---

## 🧩 Skills

A **skill** teaches Claude how to perform a specific type of task. It prevents you from repeatedly explaining the same standards, preferences or processes.

Agent skills are folders containing:

- Instructions
- Scripts
- Examples
- Supporting resources
- A `SKILL.md` file

---

### How Skills Work

The `SKILL.md` file contains the skill’s instructions and description.

Claude uses the **description** to decide when the skill is relevant:

1. Claude reads your request.
2. It compares the request with available skill descriptions.
3. It activates matching skills.
4. It loads and follows their instructions.

For example, when you ask Claude to review a dbt pull request, it could automatically activate a skill containing your team’s SQL and dbt review standards.

---

### Skill Locations

#### Personal Skills

Personal skills are stored in:

```text
~/.claude/skills/
```

They are available across all your projects.

Use personal skills for your own preferences, such as:

- Commit-message style
- Documentation format
- Preferred explanation style
- SQL formatting preferences

#### Project Skills

Project skills are stored in the repository:

```text
project-root/
└── .claude/
    └── skills/
```

Anyone who clones the repository receives the project skills.

Use project skills for shared team standards, such as:

- SQL code-review guidelines
- dbt modeling conventions
- Data-quality requirements
- Pull-request review checklists
- Documentation standards

---

### Skills vs. `CLAUDE.md`

| Feature | `CLAUDE.md` | Skills |
|---|---|---|
| Loading | Loaded into every conversation | Loaded only when relevant |
| Purpose | General project instructions | Task-specific instructions |
| Context usage | Always consumes context | Loads on demand |
| Example | Always use lowercase SQL | Apply the team’s SQL review checklist |

Use `CLAUDE.md` for instructions Claude should always follow.

Use a skill for specialized instructions needed only for particular tasks.

---

### Skills vs. Slash Commands

- **Slash commands:** You must run them manually.
- **Skills:** Claude activates them automatically when your request matches their description.

---

### When to Create a Skill

Create a skill when you repeatedly explain how Claude should perform the same task.

Good examples for a data project include:

- Reviewing SQL and dbt models
- Writing commit messages
- Creating schema documentation
- Checking data-quality rules
- Reviewing dimensional models
- Formatting pull-request feedback

---

### Summary

- Skills provide reusable, task-specific instructions.
- Claude activates them automatically when their descriptions match a request.
- Personal skills apply across your projects.
- Project skills store shared team standards in the repository.
- Skills load only when needed, helping preserve the context window.
- Repeated instructions are often good candidates for new skills.

---
## 🔌 Model Context Protocol (MCP)

**Model Context Protocol (MCP)** is an open standard that connects Claude Code to external tools and data sources.

MCP gives Claude access to information outside the codebase, such as:

- Databases
- Project-management applications
- Documentation services
- Cloud platforms
- Public repositories

Claude can automatically select the appropriate MCP tool based on your request.

---

### Tools in Agentic AI

Tools allow Claude to perform actions instead of returning only a text response.

For a data project, MCP tools could help Claude:

- Retrieve information from a project-management ticket.
- Search current dbt or Snowflake documentation.
- Query database metadata.
- Inspect GitHub issues and pull requests.
- Access approved files from external systems.

---

### MCP Server Types

Add an MCP server with:

```bash
claude mcp add
```

There are two main server types:

- **HTTP server:** A remote service hosted by a provider and accessed over the network.
- **Stdio server:** A local process or script that runs on your computer.

---

### Manage MCP Servers

Inside a Claude Code session, run:

```text
/mcp
```

Use this command to:

- View connected servers
- Check their status
- Inspect available tools
- Reconnect a server
- Disable servers you do not need

---

### MCP Server Scopes

MCP servers can have three scopes:

| Scope | Availability |
|---|---|
| **Local** | Current project and current user only |
| **User** | All your projects |
| **Project** | Shared with the team through the repository |

Project-level MCP configuration is stored in:

```text
.mcp.json
```

Commit this file to version control when the team needs the same MCP server configuration.

> Do not store passwords, API keys or other credentials directly in `.mcp.json`.

---

### Context Cost

MCP servers add their tool definitions to Claude’s context window, even when the tools are not being used.

To preserve context:

- Enable only the servers needed for the current project.
- Use `/mcp` to disable unused servers.
- Prefer an existing CLI when it provides the same capability.
- Consider using a Skill when only reusable instructions are needed.

For example, using `gh` for GitHub may consume less context than keeping a GitHub MCP server loaded.

If MCP tools consume more than 10% of the context window, Claude Code may switch to **tool search mode** and discover tools only when needed.

---

### MCP vs. Skills

| Feature | MCP | Skills |
|---|---|---|
| Purpose | Connect to external tools and data | Provide reusable instructions |
| Capability | Retrieve information or perform actions | Teach Claude how to complete a task |
| Loading | Tool definitions may remain in context | Full instructions load only when relevant |
| Example | Query database metadata | Apply SQL review standards |

Use MCP when Claude needs access to an external system.

Use a Skill when Claude needs specialized instructions but no external connection.

---

### Summary

- MCP connects Claude Code to external tools and data.
- Add servers using `claude mcp add`.
- Manage connections using `/mcp`.
- Use `.mcp.json` to share project-level configuration.
- Disable unused servers to preserve context space.
- Prefer a CLI or Skill when an MCP connection is unnecessary.

---

## 🪝 Hooks

Hooks run commands at specific points in the Claude Code lifecycle.

Unlike prompts and instructions, hooks are **deterministic**. When their conditions are met, they always run.

> If something must happen every time, enforce it with a hook instead of relying only on a prompt.

---

### Why Use Hooks?

Instructions in `CLAUDE.md` guide Claude’s behaviour, but Claude may not follow them every time.

Hooks enforce required actions, such as:

- Formatting SQL files after edits
- Running SQLFluff or other validation tools
- Logging executed commands for auditing
- Blocking changes to production configuration
- Preventing commits directly to `main`
- Blocking destructive commands
- Sending a notification when Claude finishes

---

### Hook Events

| Event | When It Runs |
|---|---|
| `PreToolUse` | Before Claude calls a tool |
| `PostToolUse` | After a tool call completes |
| `UserPromptSubmit` | After you submit a prompt but before Claude processes it |
| `Stop` | When Claude finishes responding |
| `Notification` | When Claude sends a notification |

---

### Configure Hooks

Hooks are configured in:

```text
.claude/settings.json
```

You can configure them by running:

```text
/hooks
```

You can also edit `settings.json` directly.

A hook configuration includes:

- An event
- An optional tool matcher
- A command or script to run

---

### Example: Format Files After Editing

Use a `PostToolUse` hook to run a formatter whenever Claude changes a file.

A matcher could target file-editing tools:

```json
"Edit|MultiEdit|Write"
```

For a data project, the hook could inspect the file type and run:

- SQLFluff for `.sql` files
- A YAML formatter for `.yml` files
- A Python formatter for `.py` files

---

### Block Actions with `PreToolUse`

A `PreToolUse` hook runs before the requested action and can prevent it from executing.

The hook receives the tool name and input as JSON through standard input.

| Exit Code | Result |
|---|---|
| `0` | Allow the action |
| `2` | Block the action and return feedback to Claude |
| Any other code | Report an error without blocking the action |

The error message written to `stderr` explains why the action was blocked and helps Claude adjust its approach.

---

### Examples of Blocking Rules

A `PreToolUse` hook could block:

- Writes to a production configuration directory
- Commands containing `rm -rf`
- Commits directly to the `main` branch
- Files containing credentials or secrets
- Changes to protected data-model files
- SQL commands that modify production tables

---

### Share Hooks with the Team

Project-level hooks are stored in:

```text
.claude/settings.json
```

Commit this file to the repository so the entire team uses the same hooks.

Use the following environment variable to reference scripts stored inside the project:

```text
CLAUDE_PROJECT_DIR
```

This ensures the scripts work regardless of Claude’s current working directory.

---

### Hooks vs. `CLAUDE.md`

| Feature | `CLAUDE.md` | Hooks |
|---|---|---|
| Purpose | Provides instructions and context | Enforces actions |
| Behaviour | Guidance Claude should follow | Runs deterministically |
| Example | Ask Claude to run SQLFluff | Automatically run SQLFluff after every SQL edit |

---

### Summary

- Hooks run commands at specific Claude Code events.
- Use `PostToolUse` for formatting, validation and logging.
- Use `PreToolUse` to block unsafe operations.
- Configure hooks with `/hooks` or `.claude/settings.json`.
- Use exit code `2` to block an action.
- Commit project hooks so the entire team follows the same rules.
