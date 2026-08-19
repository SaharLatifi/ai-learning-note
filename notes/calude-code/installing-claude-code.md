# 💻 Installing Claude Code on Windows

Claude Code can be used on Windows through the **terminal** or directly inside **Visual Studio Code**.

## 🖥️ Install Using PowerShell

Open PowerShell and run the official Claude Code installation command:

```powershell
irm https://claude.ai/install.ps1 | iex
```

After installation, restart your terminal if necessary and verify the installation:

```powershell
claude
```

## 🚀 Start Claude Code

Navigate to your project directory:

```powershell
cd path/to/your/project
```

Then run:

```powershell
claude
```

Claude Code will have access to the directory where you started it and its subdirectories.

During the initial setup, you may be asked to:

* Choose a theme
* Sign in to your Claude account
* Select your organization/account if applicable
* Configure initial permissions

## 🧩 Visual Studio Code

Claude Code can also be used directly from VS Code.

1. Open **Extensions**.
2. Search for **Claude Code**.
3. Select the extension published by **Anthropic**.
4. Install it.
5. Restart VS Code if required.

You can then open Claude Code from its sidebar icon or use:

```text
Ctrl + Shift + P
```

and search for:

```text
Claude Code: Open in New Tab
```

## 📌 Terminal vs. VS Code

Both use Claude Code's agentic capabilities.

* **Terminal** → direct CLI experience and typically receives new features first.
* **VS Code** → convenient when you want Claude alongside your files and editor.

You can also use Claude Code from VS Code's integrated terminal by navigating to your project and running `claude`.
