# Exercise 4: Run agent skills in GitHub Copilot

In Exercise 3, you used GitHub MCP tools to repair a quiz issue and open a pull
request. In this exercise, choose one or more of the following activities to
explore project, installed, client-provided, and custom skills.

## Contents

- [Use a project skill](#use-a-project-skill)
- [Explore built-in Copilot skills](#explore-built-in-copilot-skills)
- [Install a third-party skill](#install-a-third-party-skill)
- [Create your own project skill](#create-your-own-project-skill)

## Use a project skill

This repository includes `.agents/skills/pr-summary-report/SKILL.md`.

1. Open the file and inspect its frontmatter and workflow.
   The skill provides instructions for a process that uses the GitHub MCP server.

2. In a fresh chat, either use the slash command to directly invoke the skill:

    ```text
    /pr-summary-report for pamelafox/github-copilot-mcp-skills-workshop
    ```

    Or use this prompt to test Copilot's ability to discover the right skill for the job:

    ```
    Summarize the open pull requests in
    pamelafox/github-copilot-mcp-skills-workshop
    ```

    You should see that the Copilot agent reads the `pr-summary-report` skill early on in the thought process.

3. Check that the report:

  * Includes every open pull request, with links.
  * Gives each pull request its own row when five or fewer are open.
  * Groups related work only when linked issues, goals, or changed files support the relationship.
  * Distinguishes explicit relationships from inferred ones.
  * Makes no changes on GitHub.


## Explore built-in Copilot skills

Each GitHub Copilot client comes with built-in skills.
Explore them using the instructions for your chosen Copilot client:

- **VS Code or Codespaces**: Type `/` to browse available skills, or type
  `/skills` to open **Configure Skills**. Inspect the source of a skill provided
  by VS Code or an extension, then invoke it on a small task.
- **Copilot CLI**: Run `/skills list`, then `/skills info SKILL-NAME` to inspect
  a preinstalled skill and its location. Invoke it with `/SKILL-NAME your task`.
- **GitHub Copilot app**: Select **Customize**, then **Skills**, to browse the
  available set. Try a GitHub-provided skill such as `/af` to find a skill for
  a task.

## Install a third-party skill

[Matt Pocock's skills repository](https://github.com/mattpocock/skills) contains
small, composable engineering workflows. 

1. If you have a recent version of the `gh` CLI installed, simply run:

  ```bash
  gh skill install mattpocock/skills --agent github-copilot --scope project --all
  ```

  Alternatively, if you have `npx` installed, run:
    
  ```bash
  npx skills@latest add mattpocock/skills --agent github-copilot --project --all
  ```

2. Your `.agents` folder should now contain many skills, including the
   `/codebase-design` skill. That skill evaluates module interfaces using deep
   module design principles. Open `.agents/skills/codebase-design/SKILL.md` and
   review the contents.

3. Start a fresh chat and try the installed skill:

  ```text
  /codebase-design evaluate whether src/quiz.py has a good interface for
  adding a timed mode and automated tests.
  ```

  You do not need to implement any new features, just observe the response.

4. Explore the other installed skills to find others that may be helpful for
   your software development flow. For example, you can use a sequence of skills like
   `/grill-me` → `/to-spec` → `/to-tickets` → `/tdd` or 
   `/implement` → `/code-review` → `/pr` → `/retro`.

## Create your own project skill

1. Create `.agents/skills/quiz-question-reviewer/SKILL.md`.
   Ask Copilot to create the skill using this prompt:

   ```text
   Create a project skill named quiz-question-reviewer. It should review a
   multiple-choice MCP quiz question, use Microsoft Learn MCP to verify the fact,
   check that exactly one of four options is correct, assess whether the
   distractors are plausible, and recommend precise revisions. It must not edit
   the quiz unless I explicitly ask.
   ```

2. Inspect the generated file. Confirm that the directory matches the skill
   name, the frontmatter includes a specific `name` and `description`, and the
   body defines a repeatable workflow rather than one fixed answer.

3. Start a fresh chat so Copilot discovers the new skill.
   In Copilot CLI, you can instead run `/skills reload`, followed by
   `/skills info quiz-question-reviewer`.
   Then try out the skill:

   ```text
   Use /quiz-question-reviewer to review this question:

   Which MCP primitive lets a server expose executable operations?
   A. Tools
   B. Resources
   C. Prompts
   D. Roots
   Correct answer: A
   ```

4. Watch for a Microsoft Learn MCP call and verify that the response separates
   factual evidence from editorial recommendations.
