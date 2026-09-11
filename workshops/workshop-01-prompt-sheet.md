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

## 1. Brainstorm and save the spec

```text
Use Superpowers to brainstorm a small research wiki with me in this
meridian-capstone repository. Read raw/client-brief.md. The purpose is to
understand Southern California specialty grocery before interviewing
Meridian's leadership. This is a fictional client and a public repository.
Use the LLM wiki pattern at
https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f
as a reference. If you cannot read it, tell me and pause for a local copy.

Ask at most four clarifying questions, one at a time. Keep this first
design focused on raw/ for sources, wiki/ for cited pages, wiki/index.md,
wiki/log.md, and concise instructions in CLAUDE.md (or this agent's
equivalent project instructions file). Preserve the original sources. Use
the provided brief and public research; apply the brief's data boundaries.

Save our agreed design as a Markdown spec in docs/superpowers/specs/.
Show me its path and pause for my review. Do not write the implementation
plan or build the wiki until I approve the preceding stage.
```

Answer the clarifying questions from your understanding of the brief. In VS
Code, expand `docs/superpowers/specs/` and open the saved spec. Check the purpose,
source handling, data boundaries, and proposed result. Ask for corrections as
needed. If the design is only in chat, ask the agent to save the Markdown file.

## 2. Approve the spec and save the plan

Use this after reviewing the spec:

```text
I have reviewed the saved spec and approve it. Use Superpowers to write
an implementation plan and save it in docs/superpowers/plans/.
Include setting up the wiki, ingesting the first public source, adding a
second public source afterward, and checking answers against the evidence.
For each task, state what a completed result looks like and how to check it.
Include a Review notes section where I can record what I requested, what
came back, my actual check, and what I accepted, changed, or rejected and why.
Leave those notes unfilled until I report what I actually did.
Show me the saved plan's path and pause before building.
```

Open the saved file in `docs/superpowers/plans/`. Check that the tasks match
your spec and say how to verify the results. The Review notes section will
hold your actual checks and decisions as you work. Both files must exist
before you approve the build.

## 3. Build the initial wiki

After reviewing the plan:

```text
I have reviewed and approve the saved implementation plan. Carry out only
the initial wiki setup task now. Pause afterward and show me the changed
files for review. Wait for my approval before ingesting a source.
```

Open the project instructions, `wiki/index.md`, and `wiki/log.md`. Compare them
with the spec. Record your first task review using step 6 below.

## 4. Ingest and check the first source

Paste the instructor-provided source URL into the same message as this prompt:

```text
Continue with the first-source task in the approved plan. Retrieve the
public source at the URL I provide and save its readable content under
raw/, retaining its title and original URL. If retrieval is incomplete
or fails, report that and stop for my help. Ingest it following the project
instructions. Show me the pages you changed and pause for my review.
```

Open the original source beside the wiki summary. Find the passage supporting
one claim. Check the date, what any number measures, and any qualification.
Record the claim, source location, result of your check, and decision using
step 6. This is your second task review.

For homework, repeat this process with at least one more public source from
the list at
https://github.com/LMU-MSBA/bsan-6088-fa26/blob/main/workshops/workshop-01-sources.md.
Your wiki needs at least two public sources ingested. The client brief does not
count toward them.

## 5. Ask a question and judge the answer

```text
What does our source say about where specialty grocers are opening?
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
ask Dana based on what you learned. Record this answer-evaluation task using
step 6. This is your third task review.

## 6. Record your review after each task

Tell the agent what you requested, what came back, the check you actually
performed, what you found, and what you accepted, changed, or rejected and why.
Then use:

```text
Add the review I just described to the saved implementation plan under
Review notes, identifying the task. Use only the checks and decisions I
reported. If anything is missing, ask me. Update the task status to match
what we actually completed, and show me the saved entry for review.
```

Read the saved entry and correct anything inaccurate. A few bullets per task
are enough. Acceptance after checking is valid; do not invent a rejection.
Your spec and annotated plan serve as the work log. `wiki/log.md` separately
records wiki updates.

## 7. Review, commit, push, and check GitHub

Ask the agent to explain the changes and help you review them. After reviewing:

```text
Commit and push the changes I just reviewed to my meridian-capstone repo.
Include the saved spec, implementation plan and my review notes, project
instructions, source material, and wiki pages. Report any failure instead
of claiming the push succeeded. Give me the GitHub links to the spec and plan.
```

Open the actual spec and plan on GitHub and check that all three task reviews
are visible. Check your public repo in a signed-out browser window. You do not
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
