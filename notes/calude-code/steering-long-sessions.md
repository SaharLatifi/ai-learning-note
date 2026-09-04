# 🕒 Managing Long Claude Code Sessions

**Date:** 2026-08-17

Short tasks are simple — ask, Claude does it, you check the result. But longer tasks (big refactors, new features) are harder because Claude can drift off track the more turns it takes. The fix comes down to two habits: **plan before it starts**, and **steer while it's running**.

## 📋 Step 1: Plan before starting

Before Claude touches any code, have it explore and research first (read-only, no edits), then hand you a plan. Actually read it carefully instead of skimming — catching an issue in the plan is much cheaper than cleaning up a mess after Claude has already written code.

## 🎛️ Step 2: Choose how you steer while it runs

Once Claude is working, you pick one of two styles — **stay hands-on** or **hand off more control**. These aren't steps you do one after another, they're two different approaches to the same problem.

### Option A — Stay hands-on (you actively steer)

**Keep context under control**
Long conversations eventually fill up Claude's context window (its working memory). `/compact` solves this by summarizing the conversation and freeing up space — but it can accidentally drop something important if you just run it blind. Better to guide it:

`/compact Focus on the --version flag implementation`

**Recover when things go wrong**
Instead of trying to talk Claude back onto the right path, you can just roll back. Every prompt you send creates a checkpoint. Double-tap escape on an empty prompt to open the rewind menu, where you can restore code, restore the conversation, or both — or summarize everything before/after a checkpoint to compress it.

### Option B — Hand off more control (Claude runs more independently)

**Let it run on its own toward a goal**
If you can describe what "done" looks like better than the exact steps to get there, use `/goal`:

`/goal all tests in src/billing pass, and the type checker reports zero errors`

Claude keeps working across turns until that condition is actually verified — not just until it thinks it's finished. The check only looks at what Claude actually outputs (like test results), so the condition has to be something visible in the transcript.

**Watch and react automatically**
`/loop` reruns a prompt on an interval, useful for watching something external — like checking if a CI run finished or a deploy went out — and reacting when the state changes.

## 🌳 Separate concern: running multiple sessions safely

This one isn't about steering a single session — it's about running several sessions at once. Running two Claude sessions on the same codebase at the same time is risky since they can overwrite each other's changes. Worktrees solve this by giving each session its own separate copy of the files, so they can't clash. A `.worktreeinclude` file lets you specify git-ignored files (like an `.env`) that should still get copied into every worktree.

## 💡 Takeaway

1. Plan first.
2. Then pick your steering style — hands-on (compact + rewind) or hands-off (goal + loop).
3. If running multiple sessions in parallel, use worktrees regardless of which steering style you chose.
