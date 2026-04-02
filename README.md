# amplify

**Dense documents become conversations.**

Write a proposal. Challenge it with AI personas. Publish it. Let others explore
it conversationally and contribute feedback — all through natural language.

amplify is a discussion platform that runs entirely on GitHub. No server, no
database, no accounts to create. Every discussion is a repo. Every contribution
is a PR. The built-in skill handles everything — you just talk.

---

## 30-second demo

**Author** opens [Claude Code](https://claude.ai/code) and says:

> "Start a discussion about why we should migrate to event sourcing"

amplify creates a repo, sets up the structure. The author writes chapters, then:

> "Challenge this as the skeptic and the operator"

Two AI personas tear the proposal apart. The author strengthens weak points,
then:

> "Publish it"

The discussion goes live. Anyone can find it, read it, and contribute.

**Contributor** says:

> "Enter the event-sourcing discussion"

The full discussion loads into their session. They explore it conversationally —
asking questions, probing arguments. Then:

> "I think the migration cost estimate in chapter 3 is way too optimistic"

amplify opens a contribution PR. The author reviews it, discusses via comments,
and eventually weaves it into the discussion.

---

## Why amplify

**Documents are static. Conversations aren't.**

A 20-page proposal sits in a doc. Some people read it, most skim it, few engage
deeply. Feedback comes as scattered comments or doesn't come at all.

amplify makes dense content interactive. Contributors explore proposals through
dialogue with an LLM that has the full content in context. They contribute
structured feedback that flows through GitHub's review system. Authors ingest
what's valuable and the discussion evolves.

**What you get from GitHub for free:**

- Authentication and permissions (public or private repos)
- Notifications (watchers get updates on new content and contributions)
- Review flow (PR comments for author-contributor dialogue)
- Version history (every change tracked, attributed, reversible)
- Discoverability (topics, stars, fork network, search)
- Hosting (README renders the discussion — no tooling needed to read)

---

## Getting started

### Prerequisites

- [Claude Code](https://claude.ai/code) or [Cursor](https://cursor.com)
- [GitHub CLI](https://cli.github.com) (`brew install gh` / `gh auth login`)

### Start a discussion

Open your AI coding tool and say:

> "Start a discussion about [your topic]"

### Find and join a discussion

> "Find active amplify discussions"

Or clone any discussion repo — the skill activates automatically when it detects
the amplify structure.

---

## How it works

### Author workflow

| You say                           | What happens                                                      |
| --------------------------------- | ----------------------------------------------------------------- |
| "start a discussion about X"      | Repo created from this template with full structure               |
| "add a chapter about Y"           | Markdown chapter added to `discussion/chapters/`                  |
| "challenge this"                  | AI personas review your draft from multiple perspectives          |
| "add a persona that focuses on Z" | Custom persona created for this discussion                        |
| "publish it"                      | Status set to active, repo metadata configured, watchers notified |
| "show me contributions"           | Open contribution PRs listed with summaries                       |
| "ingest contribution #3"          | Feedback woven into your chapters, PR closed with attribution     |

### Contributor workflow

| You say                             | What happens                                    |
| ----------------------------------- | ----------------------------------------------- |
| "find discussions about X"          | GitHub searched for matching active discussions |
| "enter the X discussion"            | Repo cloned, full content loaded into session   |
| "what does chapter 2 argue?"        | Conversational exploration of the content       |
| "I disagree with the cost estimate" | Contribution PR opened with your feedback       |
| "update my contribution"            | PR updated based on author's review comments    |

### Contributions as PRs

Contributions are pull requests — one per contribution, freeform.

The author reviews via normal GitHub flow and decides how to handle each:

- **Ingest** — agent weaves the substance into the discussion chapters
- **Iterate** — back and forth via PR comments until ready to merge as-is
- **Decline** — close with explanation

Every contribution is attributed through git history and PR links.

---

## Challenge personas

Before publishing, stress-test your discussion with built-in AI personas — or
create your own for your specific topic.

### Technical / organizational

| Persona               | Focus                                            |
| --------------------- | ------------------------------------------------ |
| **Skeptic**           | Weaknesses, hidden assumptions, overlooked risks |
| **Operator**          | Day-to-day reality, scaling, maintenance burden  |
| **Cost Analyst**      | Direct, hidden, and opportunity costs            |
| **Expander**          | Missing dimensions, adjacent opportunities       |
| **Customer Advocate** | User perspective and impact                      |
| **Security Auditor**  | Attack surface, worst-case scenarios             |
| **Historian**         | Precedent — when has this been tried before      |
| **Regulator**         | Compliance, legal, and policy risks              |

### Broader / human

| Persona              | Focus                                                       |
| -------------------- | ----------------------------------------------------------- |
| **Empathist**        | Emotional and human impact, who is affected and how         |
| **Newcomer**         | Fresh eyes — what's confusing, what assumes too much        |
| **Devil's Advocate** | The strongest case against, testing conviction              |
| **Ethicist**         | Moral implications, fairness, unintended consequences       |
| **Storyteller**      | Narrative clarity — is the argument compelling and coherent |

> "Add a persona that reviews from an investor's perspective"

Custom personas follow the same format and are available immediately.

---

## Discussion structure

In each discussion repo:

```
README.md                 The discussion — overview, chapters TOC, how to contribute
discussion/
  meta.yaml               Title, author, status (draft/active/closed), tags
  chapters/               Numbered markdown files — the substance
  questions.yaml           Open questions for contributors to address
contributions/            Ingested contributions (from merged PRs)
templates/personas/       Challenge personas (13 built-in + custom)
```

The README is the discussion's landing page — auto-synced from content so anyone
can read it directly on GitHub without any tooling.

---

## Discovery

Every discussion repo is configured with GitHub's discoverability features:

- **`amplify-discussion` topic** on every repo + status topics + custom tags
- **Stars** signal interest — "12 stars and 3 open contributions"
- **Watch** to get notified on new chapters, contributions, and updates
- **Releases** mark milestones — "v2: incorporated cost analysis feedback"
- **Fork network** — browse all discussions created from this template
- **README** renders the full discussion — readable without any tools

---

## License

MIT. The template, skill, and personas are open source. Discussion content
belongs to its authors.
