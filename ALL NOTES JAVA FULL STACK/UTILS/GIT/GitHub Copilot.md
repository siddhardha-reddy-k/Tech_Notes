**Topic 18: GitHub Copilot** *(awareness-level)*

**What it is**

An AI-powered code completion tool that plugs into your code editor (VS Code, PyCharm, JetBrains IDEs, etc.) and suggests code as you type — trained on public code, documentation, and other resources.

**Core capabilities:**

- Auto-completes lines, whole functions, or entire code structures based on context (function names, variable names, surrounding code)

- Real-time suggestions as you type — accept with Tab or by selecting

- Supports most major languages: Python, JavaScript, Java, C++, etc.

**Important limitation to remember:** Copilot does **not** debug your code — it assists with writing, but testing/debugging remains entirely on the developer. It's an assist tool, not a replacement for understanding what you're writing (worth remembering given you're specifically trying to build real understanding, not just pass code through).

**Typical Workflow**

1. Install the Copilot extension in your editor (e.g., VS Code marketplace)

1. Sign in with GitHub account, grant permissions

1. Open/create a project — Copilot works contextually within whatever language/framework you're using

1. Start typing — Copilot suggests completions inline

1. Accept suggestions (Tab) or ignore them and keep typing your own

1. **Review the generated code** — don't blindly accept; check it matches your intent and standards

1. Test the code yourself — Copilot doesn't do this for you

1. Commit and push through normal Git workflow, same as any other code

**Interview-relevant framing if asked "have you used AI coding tools":** *"Yes — tools like Copilot speed up writing repetitive/boilerplate code, but I still review and test everything it suggests, since it doesn't guarantee correctness or handle debugging."* This shows you use the tool without being dependent on it — a good signal to an interviewer.
