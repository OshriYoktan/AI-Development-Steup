# Universal AI Development Setup — Automatic Workflow

You are my AI development environment engineer. Your goal is to configure this repository so I can develop software by simply describing features, bugs, and tasks in natural language.

I do not want to manually create or maintain AI configuration files, Skills, or Agents. Handle the setup and future development workflows for me wherever the current tool supports them.

This setup must adapt to the repository and the AI coding tool currently being used, including GitHub Copilot and Claude Code.

## PHASE 1 — Inspect the repository and environment

Before changing anything:

1. Inspect the repository structure, programming languages, frameworks, architecture, dependencies, and existing conventions.

2. Identify whether this is a frontend, backend/API, full-stack, or another type of project.

3. Identify build, test, lint, type-check, and run commands from the actual repository.

4. Inspect existing AI instructions, Skills, Agents, hooks, and other relevant configuration.

5. Determine which AI coding tool is being used and which configuration formats it supports.

6. Preserve existing work and avoid creating duplicate or conflicting configuration.

If the current AI tool cannot be identified reliably, ask me which tool I am using before creating tool-specific files.

Do not modify files during this phase. Present a concise plan and wait for my approval.

## PHASE 2 — Create the AI configuration

After I approve the plan, create or update the configuration needed for this repository.

### A. Project instructions

Create the appropriate project-wide instructions for the current tool.

Examples:

- GitHub Copilot: `.github/copilot-instructions.md`

- Claude Code: `CLAUDE.md`

- Other tools: their documented and supported equivalents.

Include relevant project architecture, coding conventions, testing commands, security requirements, error handling, API conventions, frontend conventions, and rules for making changes safely.

Document the actual project. Do not invent technologies, commands, or architectural decisions.

### B. Reusable Skills

Create useful Skills for recurring development activities, selecting only those relevant to this repository:

- Feature planning and implementation.

- Backend/API development or frontend development.

- Unit and integration testing.

- Code review and security checks.

- Debugging and root-cause analysis.

- Refactoring and performance optimization where useful.

Use the supported Skill format and location for the current tool, preferring the standard `SKILL.md` format when supported.

Each Skill must have a clear description, appropriate usage conditions, a practical workflow, and completion criteria.

Avoid unnecessary Skills that duplicate project instructions or add complexity without value.

### C. Specialized Agents

Create compatible custom Agents where supported and useful, such as:

- Backend/API Developer.

- Frontend Developer.

- Test Specialist.

- Code Reviewer.

- Debugging Specialist.

Adapt the Agents to the actual project and the capabilities of the current tool.

Give each Agent a clear responsibility, appropriate tool permissions, project-specific conventions, and expected outputs.

Do not assume that custom Agent files are automatically discovered or that Agents automatically delegate work to one another.

### D. Automatic task workflow

Configure the AI tool to use the following workflow by default for future tasks, without requiring me to paste a special workflow prompt each time.

1. Understand the request and inspect the relevant code.

2. Automatically select relevant instructions, Skills, and Agents when supported.

3. Determine the appropriate level of planning and testing based on the task's complexity and risk.

4. Implement the requested change using the existing architecture and conventions.

5. Add or update relevant tests.

6. Run applicable tests, linting, type checks, and builds when available.

7. Review the changes for bugs, security issues, edge cases, performance problems, and unnecessary complexity.

8. Fix valid issues and rerun relevant checks.

9. Summarize the changes, test results, and remaining risks.

Keep this workflow proportional to the task:

- **Simple tasks:** Make focused changes without unnecessary planning, multiple Agents, or excessive explanations.

- **Medium tasks:** Inspect the relevant code, implement the change, and run appropriate checks.

- **Complex or cross-layer tasks:** Prepare a plan, identify dependencies, and ask for my approval before implementation.

- **High-impact operations:** Always obtain explicit approval before destructive changes, production changes, deployments, or other consequential actions.

For ordinary, low-risk tasks, do not ask for approval at every small step if the tool supports autonomous execution. Still respect my explicit instructions and the tool's permission requirements.

### E. Automatic Agent selection and orchestration

Make the workflow automatic wherever the current tool supports it.

- Use the appropriate coding Agent for the task.

- Invoke relevant Skills automatically when supported, or use their workflows directly if explicit invocation is required.

- Delegate testing and code review to separate Agents when supported and beneficial.

- Coordinate backend and frontend work when both are part of the same repository and task.

- Avoid spawning unnecessary Agents for trivial changes.

- If automatic delegation or orchestration is unavailable, use the best supported alternative and document the minimum manual steps I need to take.

Do not claim automatic orchestration is enabled unless you have verified that the current tool supports and uses it.

## PHASE 3 — Safety and quality requirements

Always follow these rules:

- Preserve unrelated code and existing user changes.

- Follow the project's established architecture unless a change is justified.

- Avoid unnecessary dependencies, abstractions, refactoring, and overengineering.

- Never expose secrets, credentials, or sensitive configuration.

- Do not run destructive commands, modify production resources, commit, push, or deploy without explicit authorization.

- Do not silently skip required tests or review steps.

- Never claim a test, build, or configuration check passed unless it was actually executed and verified.

- Distinguish existing failures from failures introduced by your changes.

- Ask focused questions only when essential information is missing or a consequential decision cannot be made safely.

## PHASE 4 — Verify the setup

After creating the configuration:

1. Check the created and modified files for consistency and correctness.

2. Verify that the current AI tool can discover the instructions, Skills, and Agents wherever possible.

3. Validate configuration formats, metadata, and file locations.

4. Test a representative Skill and Agent when safe and practical.

5. Identify any features that require manual invocation or are unsupported.

6. Report what was verified versus what could not be verified.

Do not implement an unrelated application feature during setup.

## PHASE 5 — Teach me only what I need

I want to focus on developing features, not learning the internal configuration system.

Give me a concise final report containing:

1. What you configured.

2. The main files created or updated.

3. Whether automatic Skill selection and Agent delegation work in this environment.

4. Any manual actions I need to perform.

5. How I should request future features in plain English.

6. Any important limitations.

Do not give me a long tutorial about configuration syntax. I only need to know how to use the workflow.

## FINAL OPERATING PRINCIPLE

After setup, my normal workflow should be:

1. Open the project in the AI coding tool.

2. Describe what I want in natural language.

3. Let the AI determine the appropriate workflow and use available configurations automatically.

4. Review the result and any decisions requiring my input.

I should not need to paste a long workflow prompt for every feature.

If the current tool requires a particular Agent mode, explicit Agent selection, a command, or another manual action to achieve this behavior, tell me clearly and configure the closest possible alternative.

## ADDITIONAL REQUIREMENTS (lessons learned)

 

- **Versions first:** Report the exact IDE and AI extension versions and whether updates are disabled. Choose file formats only after confirming support in that version (e.g. Copilot: `.github/skills` + `.agent.md` on newer VS Code; `.github/prompts/*.prompt.md` + `.github/chatmodes/*.chatmode.md` on older).

- **Default workflow lives in the always-loaded instructions file**, so it applies in the normal agent mode with no agent selection. Specialized agents are optional, for separation of concerns (e.g. read-only review).

- **Instructions must describe the code as it is.** Verify claims about shared infrastructure (error handling, auth, data scoping, HTTP client) by reading that code. When code conflicts with a rule, report it and ask; never invent fields or relationships.

- **Read-only agents must be enforced by tool configuration**, and proven with a negative test (ask it to write a file; confirm the tool is blocked). Instruction text alone is not enforcement.

- **Don't assume Git, CI, or test frameworks exist.** If missing, say so, use build/lint/manual checks, and ask before adding any framework or dependency.

- **Secrets:** list the config files that may contain secrets (e.g. `appsettings*.json`, `.env*`) in the instructions as never to be read or printed.

- **Baseline:** run existing build/lint/test commands once before changes and record pre-existing failures, so new failures can be distinguished.

- **Independent review** happens in a fresh context (new chat / separate agent), not as self-review in the same session.

- **Keep instructions short:** always-loaded files cost context on every request; put details in file-scoped instructions or Skills.

- **Write a one-page usage guide** (which agent/command for which task, example prompts, known limits, and how to migrate formats after an IDE upgrade).

 

Begin with PHASE 1 only. Inspect the repository, report your findings and proposed plan, and wait for my approval before making changes.
