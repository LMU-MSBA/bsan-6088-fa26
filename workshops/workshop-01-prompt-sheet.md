# Workshop 01: Working with AI, prompt sheet

Use these prompts one at a time. Read the agent's response, answer its questions,
and check the saved files before moving on. The prompts that approve work are
for after you have reviewed it.

## Before you begin

Create your own public `meridian-capstone` repository on GitHub, with a README.
Clone it using VS Code's **Git: Clone** action and open it. Check the repo name
in VS Code's Explorer and your account and repo name on GitHub.

Save the client brief as `raw/client-brief.md`. The Markdown file is at
https://raw.githubusercontent.com/LMU-MSBA/bsan-6088-fa26/main/workshops/client-brief.md
and the readable version is at
https://github.com/LMU-MSBA/bsan-6088-fa26/blob/main/workshops/client-brief.md.
Open your saved copy to check the contents.

Start your agent in this project and confirm Superpowers is available, using
the tutorial's instructions for your agent at
https://github.com/LMU-ISBA/ai-dev-workflow-tutorial. Keep the dashboard
tutorial in its separate `ai-dev-workflow-tutorial` repo.

For every task, ask yourself:

1. What are you asking the AI to do?
2. How will you check its work?
3. What will you accept, change, or reject, and why?

## 1. Brainstorm the design

```text
Help me design a research wiki to prepare for the Meridian stakeholder interview.
Interview me one question at a time with multiple-choice options.
Do not write the spec until I approve the design.
Read @raw/client-brief.md.
Follow the LLM wiki pattern at https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f.
```

Answer the questions from your understanding of the brief. When the agent
summarizes the design, ask for changes until it matches what you want.

## 2. Approve the design and write the spec

```text
I approve the design. Write the spec.
Do not write the implementation plan until I approve the spec.
```

In VS Code, expand `docs/superpowers/specs/` and open the saved spec. Read the
purpose, source handling, data boundaries, and proposed result, and push back
on anything to change. Approve it only when the file says what you decided. If
the spec is only in chat, ask the agent to save the Markdown file.

## 3. Approve the spec and write the plan

```text
I approve the spec. Write the implementation plan.
For each task, say what done looks like and how I check it.
If the spec leaves a choice open, ask me before deciding.
Do not build until I approve the plan.
```

Open the saved file in `docs/superpowers/plans/`. Check that the tasks match
your spec and say how to verify the results. The first task should set up the
wiki and ingest the client brief already in `raw/`; if it doesn't, ask for that
change. Later tasks should cover ingesting public sources and checking answers
against them. The spec
and plan are your work log, so ask for corrections until the saved files say
what you decided. Both files must exist before you approve the build.

## 4. Approve the plan and build the initial wiki

After you approve, the agent asks for an execution mode: subagent-driven or
inline. Choose inline so every change happens in front of you. This prompt
answers that question:

```text
I approve the plan. Execute inline.
Do only the first task.
Show me the changed files and stop.
```

Open the project instructions, `wiki/index.md`, `wiki/log.md`, and the page
built from the brief. Compare them with the spec and ask for corrections as
needed.

## 5. Ingest and check the first public source

Put the instructor-provided source URL on the last line:

```text
Do the next task in the plan: ingest the source at the URL below.
Keep the original in raw/ with its title and URL.
If the fetch fails, stop and tell me.
Show me the changed pages and stop.
<paste the source URL>
```

Open the original source beside the wiki summary. Find the passage supporting
one claim. Check the date, what any number measures, and any qualification.
If the wiki page misstates the source, ask the agent to correct it.

## 6. Start your second source

Choose a public source yourself, based on the one thing you wrote down to
research before meeting Dana. If you're stuck for one, or the fetch fails, pick
from the fallback list at
https://github.com/LMU-MSBA/bsan-6088-fa26/blob/main/workshops/workshop-01-sources.md.

Use the step 5 prompt again, with your URL on the last line.

When it pauses, glance at the changed pages and move on to step 7. Checking
this source closely is homework: open the original beside the wiki summary,
find the passage behind one claim, and ask for a correction if the page
misstates it. Then add
at least one more source you choose, so your wiki has at least three public
sources ingested. The client brief does not count toward them.

## 7. Ask a question and judge the answer

```text
What do our sources say about where specialty grocers are opening?
Cite the evidence and distinguish the source's claims from inference.
```

Follow a citation through the wiki page to the original source. Then ask:

```text
Which of Meridian's fourteen stores is underperforming, and why?
Explain what the available sources establish, what they do not establish,
and what additional information would be needed.
```

Check whether the answer stays within the evidence. An honest statement that
information is missing can be a good answer. Identify one useful question to
ask Dana based on what you learned and keep it for Workshop 2.

## 8. Review, commit, push, and check GitHub

Ask the agent to explain the changes and help you review them. After reviewing:

```text
Update the task statuses in the plan to match what we completed.
Commit and push everything to GitHub.
Tell me if anything fails.
Give me the GitHub links to the spec and plan.
```

Open the actual spec and plan on GitHub and check that they are the versions
you reviewed. Check your public repo in a signed-out browser window. You do not
need to memorize Git commands; you do need to verify that the files reached
GitHub.

If a step fails, keep the error and what you tried and ask for help on Teams.
If you evaluated the instructor's output while your setup was blocked, label
those notes accordingly and finish your own workflow afterward.

## Submission reminder

Follow the Brightspace assignment: paste six links (capstone repo, reading
notes, spec, plan, deployed dashboard, tutorial repo) and type the
confidentiality paragraph in the Brightspace text submission box by
**September 20 at 11:59 PM Pacific**. No attachment is needed. Share the
reading-notes Google Doc with **greg@lontok.com**.
