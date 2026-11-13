# Workshop 3: getting the data

In a capstone, the client's data often arrives late, thin, or locked behind an
agreement. The same thing happens when you build a project for a job you're
applying to, because that company's data isn't yours to use. In both cases you
find data somewhere else and pull it yourself.

This workshop is a tour of four routes to data. A route is the way data gets
from where it lives to a file on your disk, and a pull is one trip along a
route. You'll make one small pull on each route and write down what you did,
so someone else could repeat it.

| Section | Route                             | The situation it fits                        |
| ------- | --------------------------------- | -------------------------------------------- |
| 2       | An API called from Python         | You know who publishes the data              |
| 3       | An MCP connector                  | You don't know yet which source has the data |
| 4       | Firecrawl                         | The data sits on a web page                  |
| 5       | A token for a system that's yours | The data belongs to you or your client       |

The workshop is self-paced. Work through the sections in order, and check
what each section asks you to check before you move on.

## What you'll have at the end

- Four data files, one from each route.
- Two Python scripts that can rerun their pulls.
- A source note for each pull.
- One paragraph of your own on which route you'd try first.

## 1. Set up

Open your `meridian-capstone` repo in VS Code. This workshop doesn't use the
Meridian case. You're using the repo because your Workshop 1 and 2 work is
already there.

These steps assume Claude Code. If you use another agent, ask it how to add an
MCP server by its address.

### Create two accounts

Both accounts are free, and you don't enter a card for either one.

1. Request a Census key at https://api.census.gov/data/key_signup.html.
2. Open the email from the Census Bureau and select the activation link.
3. Sign up for Firecrawl with your LMU email at
   https://www.firecrawl.dev/student-program.
4. In Firecrawl, open Settings, then Billing.
5. Enter the student code shown on that page.

Request the Census key first. The email can take a few minutes, and you can
finish the other steps while you wait.

### Add two connectors

An MCP server is a service that gives your agent a set of tools it can call.
Claude calls an MCP server a connector. You'll use two of them, and adding
both now means you won't have to restart your agent in the middle of the tour.

Run these two commands in the VS Code terminal, before you start Claude Code:

```text
claude mcp add --transport http usafacts https://data.mcp.usafacts.org/mcp
claude mcp add --transport http firecrawl https://mcp.firecrawl.dev/v2/mcp-oauth
```

1. Start Claude Code.
2. Enter `/mcp`.
3. Choose `firecrawl` and sign in through your browser.
4. Check that `usafacts` and `firecrawl` both show as connected.

USAFacts needs no account and no key.

### Set the rules for the tour

Your agent can get data several ways, and it won't always tell you which one
it used. If you don't know the route, you can't repeat the pull or explain it
to a client. The first rule below is there for that reason.

A key is a string that identifies your account to a service. Anyone who has
your key can act as you. Your repo is public, so a key in a committed file is
public too. The second rule and the `.env` file keep your keys out of the repo.

```text
We're doing BSAN 6088 Workshop 3, a tour of four routes to data.
Save the rules below as workshop-03/rules.md and follow them until I
say the tour is over.

1. I name the route for each pull. Use that route only. If it fails,
   stop and tell me. Don't switch to web search, your memory, or
   another tool.
2. Never open .env. Never print a key or put one in a command, a file,
   or the chat.
3. Save data under workshop-03/data/ and scripts under
   workshop-03/pulls/.
4. Never generate or fill in data. If a pull returns nothing, say so.
5. Do one step at a time, then stop.

Create workshop-03/data/, workshop-03/pulls/, and an empty
workshop-03/sources.md. Create an empty .env in the repo root if there
isn't one, and add .env to .gitignore. Show me that Git ignores .env.
Then stop.
```

You'll add keys to `.env` yourself in VS Code. Your agent doesn't need to see
them.

When you come back in a new session, start with this prompt:

```text
Read workshop-03/rules.md and follow it.
```

You're set up when all of these are true:

- `workshop-03/` holds `data/`, `pulls/`, `rules.md`, and `sources.md`.
- Git ignores `.env`.
- You've opened the activation link in the Census email.
- `/mcp` shows `usafacts` and `firecrawl` as connected.

### The source note

Every pull gets a source note in `workshop-03/sources.md`. The source note is
what lets a teammate or a client trust the file, and it's what you'll rely on
when you reopen the project in three months. Each source note answers the same
six questions:

1. Which route did the pull take?
2. What is the source, and what is its URL?
3. What date did you pull it?
4. What do the source's terms allow you to do with the data?
5. Does the file hold personal data, meaning anything about an identifiable
   person?
6. How did you check that the data is right?

Your agent can draft the first three answers. Write the last three yourself.

## 2. An API called from Python

Suppose a client gives you sales by county and nothing about the people who
live in each county. The Census Bureau publishes that, and it offers an API.

An API is an address that answers a request with data and not a web page. The
request names the dataset, the fields you want, and the places you want them
for. A key in the request tells the service who is asking.

1. Open `.env` in VS Code.
2. Add the line below with your own key.
3. Save the file.

```text
CENSUS_API_KEY=your-key-here
```

Then ask your agent:

```text
Route: the Census Data API, called from a Python script.

Read the user guide first:
https://www.census.gov/data/developers/guidance/api-user-guide.html

Write workshop-03/pulls/census_counties.py. It pulls total population
and median household income for every county in California from the
most recent ACS 5-year dataset. It loads CENSUS_API_KEY from .env and
saves workshop-03/data/census_counties.csv. Use a virtual environment.

Run it. Show me the request address with the key replaced by KEY.
Then stop.
```

In the request address, find:

- The year and the dataset.
- The field codes after `get=`.
- The places after `for=` and `in=`.
- Where the key goes.

Ask your agent what each field code means if the address doesn't tell you.

Open the CSV, which should have 58 rows, one for each California county. Look up
the median household income for Los Angeles County at https://data.census.gov,
using the same year and the ACS 5-year estimates. Does it match your file?

Read the terms at
https://www.census.gov/data/developers/about/terms-of-service.html. Find the
statement they ask you to include when you publish something built on the API.

Now ask for the source note:

```text
Add a source note for this pull to workshop-03/sources.md. Answer
questions 1 to 3. Leave questions 4, 5, and 6 blank for me.
```

Write answers 4, 5, and 6 yourself.

If your Census key hasn't arrived, use this prompt and say so in your source
note. The Bureau of Labor Statistics API answers without a key.

```text
Route: the Bureau of Labor Statistics public API, version 1, with no
key, called from a Python script.

Write workshop-03/pulls/bls_unemployment.py. It pulls series
LAUCN060370000000003, the unemployment rate for Los Angeles County,
and saves workshop-03/data/bls_unemployment.csv. Use a virtual
environment.

Run it. Show me the request address. Then stop.
```

## 3. An MCP connector

Suppose the client's sales dipped last year, and they want to know if the
economy explains it. You need an economic series, and you don't know which
agency publishes the right one.

The USAFacts connector reaches about two dozen government sources through one
set of tools. USAFacts is a nonprofit that organizes US government data.

Start by asking what the connector offers:

```text
Route: the USAFacts connector. Don't use web search or your memory.

List the sources the connector offers, with one line on what each
covers. Then stop.
```

Read the list, and decide which source would hold a monthly unemployment rate
before you go on.

```text
Route: the USAFacts connector only.

Get the monthly unemployment rate for California and for the United
States over the last 24 months. Save it as
workshop-03/data/usafacts_unemployment.csv.

Show me the citation the connector returned: the agency, the date, and
the exact API call. Tell me which connector tools you called. Then
stop.
```

Read the citation. The connector made an API request, the same kind of request
your script made in section 2. Two things differ, and both matter in a
capstone.

You have no script, so next month's refresh means asking again unless your
agent turns the citation's API call into a script.

The rows also went through the model on their way to your file. A script
writes rows to your disk, but a connector returns its rows to your agent. If a
client bars customer records from AI tools, a connector is the wrong route for
those records.

Open the agency page named in the citation. Check one month in your file
against it.

Ask for the source note with the same prompt as in section 2, then write
answers 4, 5, and 6 yourself. The citation carries any terms notice the agency
requires.

If `usafacts` won't connect, install it from
https://claude.ai/directory/connectors/usafacts-connector and restart Claude
Code. The connector is in open beta and can be down for a short time. If it
still fails later, record the error and what you tried in your source note,
then go on to section 4.

Other connectors search for datasets too, and each needs a free account:

- Kaggle, at https://www.kaggle.com/docs/mcp
- Hugging Face, at https://huggingface.co/settings/mcp
- Data Commons, at https://docs.datacommons.org/mcp/run_tools.html

You don't need them for this workshop. The full directory is at
https://claude.ai/directory.

## 4. Firecrawl

Suppose you want a list of the largest US companies with each one's industry,
revenue, employees, and headquarters. No agency publishes that list as a file,
and a web page has it in a table.

Firecrawl is a service that reads a web page and returns its content in a
clean form. It replaces most of the scraping code people used to write by
hand.

### Check the terms before you pull

A public page isn't always a page you may collect. The site's terms of use
say what you may do with its content. Its `robots.txt` file tells automated
visitors which pages they may request.

```text
Route: Firecrawl.

Don't collect any data in this step. Read Wikipedia's terms of use and
https://en.wikipedia.org/robots.txt. Tell me what they say about
automated collection and about reusing the content. Quote the lines
you rely on. Then stop.
```

Read the quoted lines yourself. Decide if this pull is allowed and what
conditions come with it. That decision is answer 4 in your source note.

### Pull the table

```text
Route: Firecrawl only.

Scrape
https://en.wikipedia.org/wiki/List_of_largest_companies_in_the_United_States_by_revenue
and save the first table, the largest public companies, as
workshop-03/data/largest_companies.csv. Keep the page's values as they
are. Tell me which Firecrawl tool you called and how many credits it
used. Then stop.
```

Open the page in your browser. Compare three rows in your file with the page,
and check that the row counts match.

Ask for the source note, then write answers 4, 5, and 6 yourself.

### Check one site of your own

Pick a company you'd apply to, or one that looks like a capstone client. Find
a page on its site with data you'd want, such as locations, products, prices,
or job listings.

```text
Route: Firecrawl.

Don't collect any data in this step. Read the terms of use and
robots.txt for [site]. Tell me what they say about automated
collection. Quote the lines you rely on. Then stop.
```

Add a heading called "A site I checked" to `workshop-03/sources.md`. Under it,
write the site, the data you wanted, what the terms say, and your decision. If
the terms don't allow collection, add one sentence on where else you'd look.

Don't pull anything from this site, because the decision is the work in this
step.

If the student code didn't apply, Firecrawl's free plan has enough credits for
this section.

## 5. A system that's yours

First-party data is data an organization already holds in its own systems,
such as its point of sale, its CRM, or its loyalty platform. Most of those
systems have an API. The client's IT team gives you a token, which works like
a key. They decide what the token can read and how long it lasts.

You don't have a client's system for this workshop. GitHub holds your own
records, so it stands in for one.

Create a token that can read one repo for one week:

1. On GitHub, open Settings, then Developer settings.
2. Open Personal access tokens, then Fine-grained tokens.
3. Select Generate new token.
4. Set the expiration to 7 days.
5. Under Repository access, choose Only select repositories.
6. Select `meridian-capstone`.
7. Under Permissions, set Contents to Read-only.
8. Generate the token and copy it.
9. Add the line below to `.env` with your own token, then save.

```text
GITHUB_TOKEN=your-token-here
```

GitHub changes these screens from time to time. If yours differ, aim for the
same result: a token that reads this one repo and expires in a week.

```text
Route: the GitHub REST API, called from a Python script with my token.

Read the docs first:
https://docs.github.com/en/rest/commits/commits

Write workshop-03/pulls/github_commits.py. It lists every commit in my
meridian-capstone repo with the SHA, the date, and the message. It
loads GITHUB_TOKEN from .env and follows pagination. Leave out author
names and email addresses. Save workshop-03/data/github_commits.csv.

Run it. Show me the request headers with the token replaced by TOKEN.
Then stop.
```

Find the header that carries the token. Compare the row count in your file
with the commit count on your repo's GitHub page.

Three things in this pull carry over to a client's system.

The token reads one repo and can't change it. Ask a client for the same thing:
read-only access to the tables you need.

The token also expires, so it's useless to anyone who finds it a year after
the project closes.

Commit records include names and email addresses, and your script left them
out before it wrote the file. Make that decision with customer records too.
Choose the fields you need before you pull.

You can also run the script yourself in the terminal. The rows then go to your
disk without passing through a model. Your agent can write a script from an
API's documentation without seeing the data. That's how you work with records
a client bars from AI tools.

Many systems also ship a command-line tool that wraps the same API. GitHub's
is `gh`, and this command returns the same records:

```text
gh api repos/[your-username]/meridian-capstone/commits
```

It's the same route with less code. Try it if you already have `gh` installed.

Ask for the source note, then write answers 4, 5, and 6 yourself.

## 6. Write your paragraph and turn it in

Add a heading called "Which route first" at the bottom of
`workshop-03/sources.md`.

Pick one real situation. It can be a capstone where the client's data is late,
or a project for a job you'd apply to. Name the data you'd need. Say which
route you'd try first and why, and what you'd check before you trusted the
data.

Write 100 to 150 words yourself. A paragraph your agent drafted doesn't meet
the standard in the syllabus.

Check for keys before you push:

```text
Check every tracked file and the full Git history for my Census key
and my GitHub token without printing either one. Confirm that Git
still ignores .env. Then stop.
```

If a key or token shows up anywhere except `.env`, replace it before you push.
Delete the token in GitHub's settings and make a new one. Request a new Census
key with the same form.

```text
Commit and push.
```

Open `workshop-03/sources.md` on GitHub. Paste its link in the Workshop 3
assignment in Brightspace. The due date is in that assignment.

This is what I check for Credit:

- Four data files in `workshop-03/data/`.
- Two scripts in `workshop-03/pulls/`.
- Four source notes, each with all six answers.
- The site you checked, with your decision.
- Your paragraph, in your own words.
- No key or token anywhere in the repo.

## If you get stuck

Paste the error to your agent and ask what it means before you ask for a fix.
Then try the fallback in that section.

If the fallback fails too, message me in Teams with the section number and
what you tried. Don't skip a route without a note. A source note that records
the error and what you tried still counts for that pull.
