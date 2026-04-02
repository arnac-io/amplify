---
name: amplify
description:
  Run a discussion — create, explore, contribute, and refine structured
  proposals via conversation.
argument-hint: "content, topic, or repo URL"
---

# amplify

A discussion platform where dense documents become conversations. Authors create
structured proposals, contributors explore them via LLM dialogue, and feedback
flows as typed contributions (PRs) that authors ingest into the discussion.

Every discussion lives in its own GitHub repo. The skill abstracts all
git/GitHub operations — users never need to know they exist.

## Setup

Before first use, verify prerequisites. If any are missing, walk the user
through setup interactively:

1. `gh` CLI installed — check with `gh --version`
2. `gh` authenticated — check with `gh auth status`
3. If `gh` is missing: guide install via `brew install gh` (macOS) or
   [cli.github.com](https://cli.github.com)
4. If not authenticated: run `gh auth login`

Do NOT proceed with any command until setup is verified.

## Detecting Role

Determine context from the current repo:

- If cwd is an amplify discussion repo (has `discussion/meta.yaml`), check if
  user is author (has push access) or contributor
- If cwd is NOT a discussion repo, user is starting fresh — offer to create or
  find a discussion

## Author Commands

### Create a discussion

Trigger: user wants to start/create/propose a discussion

1. Ask for title and optional tags if not provided
2. Generate slug from title (lowercase, hyphens, no special chars)
3. Create repo from template:
   ```
   gh repo create {owner}/amplify-{slug} --template {template-repo} --public --clone
   ```
4. Populate `discussion/meta.yaml` with title, author (from `gh api user`),
   status: draft, created date, tags
5. Configure GitHub repo metadata:
   ```
   gh repo edit {owner}/amplify-{slug} \
     --description "Discussion: {title}" \
     --add-topic amplify-discussion \
     --add-topic amplify-draft \
     --add-topic {tag1} --add-topic {tag2} \
     --enable-discussions
   ```
6. Disable issues and wiki (not needed):
   ```
   gh repo edit {owner}/amplify-{slug} --enable-issues=false --enable-wiki=false
   ```
7. Overwrite `README.md` with the discussion content: title as H1, TL;DR, and
   auto-generated sections (table of contents, contribution guide) wrapped in
   `<!-- amplify:auto -->` markers
8. Commit and push

If user provides content (text, URL, or topic), use it to draft the initial
chapters. If a URL, fetch the content and convert to markdown chapters.

### Write / edit chapters

Trigger: user wants to add, edit, or restructure discussion content

- Chapters live in `discussion/chapters/` as numbered markdown files:
  `01-problem.md`, `02-approach.md`, etc.
- Create, edit, rename, reorder as needed
- After changes, commit and push

### Challenge with personas

Trigger: user says "challenge this", "stress test", "poke holes"

1. Read all chapters into context
2. For each persona in `personas/`:
   - Adopt the persona's perspective (read the persona's .md file for the system
     prompt)
   - Review the full discussion content through that lens
   - Produce a structured critique per the persona's format
3. Present all persona reviews to the author
4. Author decides what to address

Run personas sequentially (each one in full context). The author can also
request specific personas: "challenge this as the skeptic and cost analyst".

The template ships with 13 built-in personas across two categories:

**Technical/organizational:** skeptic, operator, cost-analyst, expander,
customer-advocate, security-auditor, historian, regulator

**Broader/human:** empathist, newcomer, devils-advocate, ethicist, storyteller

### Create a persona

Trigger: user says "add a persona", "create a persona for...", "I want a
reviewer that focuses on..."

1. Discuss with the user: what perspective should this persona take? What should
   it focus on? What kind of discussion is it useful for?
2. Create the persona file at `personas/{name}.md` following the standard
   format:
   ```yaml
   ---
   name: { name }
   display_name: { The Display Name }
   description: { one-line description }
   best_for: [{ use case 1 }, { use case 2 }]
   ---
   ```
   Followed by the system prompt with:
   - Clear perspective statement ("You are reviewing a proposal as...")
   - 5-6 focus areas as bullet points
   - Guidance on tone and specificity
   - Structured output format (4 sections)
   - Closing: "End with {the persona's key question}, stated in one sentence."
3. Commit and push

Custom personas are available immediately for challenge. They also propagate to
any discussion created from this repo if it's used as a template.

### Publish

Trigger: user says "publish", "make it active", "open for contributions"

1. Update `discussion/meta.yaml`: status → active
2. Update GitHub topics: remove `amplify-draft`, add `amplify-active`
3. Update repo description with current TL;DR from README
4. Sync README auto-generated sections (TOC from chapters, contribution count)
5. Create GitHub Release (tag: `v1`, title: "Published", body: TL;DR from
   README)
6. Commit and push

### Review contributions

Trigger: user says "show contributions", "any feedback?", "what's pending?"

1. List open PRs: `gh pr list --state open`
2. For each PR, summarize: contributor, type (from PR body/branch name), content
   preview, comment count
3. Present as a numbered list

### Ingest a contribution

Trigger: user says "ingest #N", "incorporate that feedback", "work in
contribution #N"

1. Fetch the PR content: `gh pr view {N} --json body,title,headRefName`
2. Fetch the PR diff to see the contribution file content
3. Read the contribution and the current chapters
4. Work the contribution's substance into the relevant chapters — rewrite,
   extend, or restructure as the content requires
5. Add attribution in a commit message: "Ingest contribution from @{user}:
   {summary}"
6. Close the PR with a comment explaining how it was incorporated:
   `gh pr close {N} --comment "Ingested into chapters — {details}"`
7. Commit and push

The author can also choose to merge as-is if the contribution is ready:
`gh pr merge {N} --squash`

### Update

Trigger: user says "update the discussion", "push changes"

1. Commit current changes with descriptive message
2. Push
3. Optionally create a new GitHub Release for significant updates
4. GitHub notifications reach all watchers automatically

### Close

Trigger: user says "close", "wrap up", "conclude"

1. Update `discussion/meta.yaml`: status → closed
2. Update GitHub topics: remove `amplify-active`, add `amplify-closed`
3. Create final GitHub Release with summary of outcomes
4. Update README with conclusion
5. Commit and push

## Contributor Commands

### Find discussions

Trigger: user says "find discussions", "what's open?", "any discussions about
X?"

Search GitHub for amplify discussions:

```
gh search repos --topic amplify-discussion --topic amplify-active --sort updated
```

For topic search:

```
gh search repos --topic amplify-discussion "query terms" --sort stars
```

For org-scoped:

```
gh search repos --topic amplify-discussion --owner {org}
```

Present results with: title, author, stars, last updated, link.

### Enter a discussion

Trigger: user says "enter", "open", "read the X discussion"

1. Clone the repo if not already local: `gh repo clone {owner}/amplify-{slug}`
2. Read all content: README.md, meta.yaml, all chapters, questions.yaml
3. Read existing contributions: `gh pr list --state all`
4. Load everything into context
5. Tell the user what the discussion is about and invite them to explore

### Explore

No special trigger — once entered, the user just talks. They ask questions about
the content, the LLM responds from the loaded context. This is the core of
amplify: dense documents become conversations.

### Contribute

Trigger: user expresses an opinion, disagreement, idea, question, or data point
about the discussion content. Also: "I want to contribute", "I disagree
with...", "what about...", "here's data that..."

1. Identify the contribution type from context:
   - **question** — asks something the discussion should address
   - **insight** — offers a perspective or observation
   - **dissent** — disagrees with a claim or approach
   - **enhancement** — suggests an addition or improvement
   - **data** — provides evidence, numbers, or references
2. Draft the contribution content with the user conversationally — refine until
   they're happy
3. Create a branch: `git checkout -b contribution/{type}-{short-desc}`
4. Write contribution file to `contributions/{date}-{user}-{type}.md`
5. Commit and push the branch
6. Open a PR:
   ```
   gh pr create --title "{type}: {summary}" --body "{contribution content}"
   ```
7. Share the PR link with the user

### Revise a contribution

Trigger: user says "update my contribution", "revise based on feedback"

1. Check PR review comments: `gh pr view {N} --json reviews,comments`
2. Show the feedback to the user
3. Discuss revisions conversationally
4. Update the contribution file on the branch
5. Commit, push — PR updates automatically
