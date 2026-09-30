# Rubric: is this a good first issue?

Five required checks, one per surface that actually kills a first
contribution: the maintainer is alive, the repo is in use, the scope fits a
newcomer, nobody else is already on it, and the project's rules permit the way
I work. Three preferred checks rank the issues that survive.

Every recency threshold is measured against the capture date stamped on the
bundle in eval mode, and against today in live mode.

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| `maintainer-alive` | Repo facts: the "last 5 default-branch commits" list (dates and author names), and the "maintainer first-response sample" | Passes if **either** holds: (a) at least one of the last 5 default-branch commits lands within **180 days** of the capture date and is authored by a human or by a bot merging a human's pull request; or (b) the first-response sample shows a commenter with author_association Owner, Member, or Collaborator replying within **90 days**. A list made only of standalone bot commits (author ends in `[bot]`, not merging a human PR) does not satisfy (a). | required |
| `repo-in-use` | Repo facts: the `archived:` flag on the repo line, "latest release", "last push to any branch" | Passes if the repo is **not archived** AND **either** the latest release is within **365 days** of the capture date **or** the last push to any branch is within **180 days**. An archived repo fails outright regardless of dates. | required |
| `scope-bounded` | The issue body and the full comment thread | Ask one question: **could one person land this in a single pull request?** Fails only if **any** of these is true: the issue calls itself an umbrella, tracking, meta, or epic issue, or lists sub-items each meant to become its **own separate issue or PR**; the work is described as applying **repo-wide** ("across the codebase", "every module", "all call sites"); the thread shows the design still being debated with no maintainer having settled it; a maintainer states the fix reaches core internals; the issue is a pure usage or support question ("how do I get this to work?") rather than a request for a change; or the issue is an **unendorsed feature request** — see the next sentence. **Unendorsed feature request** means *all* of: the issue proposes **new functionality** (not a bug fix or a docs task); its author is not a maintainer (author_association `NONE`, `CONTRIBUTOR`, or `FIRST_TIME_CONTRIBUTOR`); **no** maintainer comment in the thread supports building it; and it carries **no** maintainer-applied acceptance label (`good first issue`, `help wanted`, `accepted`, `approved`). When all four hold, an unmade product decision is hiding inside the request no matter how tidy its formatting, and the check fails. Any one of these rescues it: a maintainer opened it, a maintainer endorsed it in the thread, or a maintainer labelled it. This clause **never** applies to bug reports or documentation tasks. **Detail is scoping, not sprawl**: a long body, sub-headings, a bullet list of requirements, or edits to a handful of **named** files that ship together in one PR all **pass** — a precise specification of one deliverable is the best-scoped kind of issue, not an umbrella. A terse body, a missing reproduction, or a bare acceptance-criteria checklist likewise **pass**. Grade the size of the work asked for, not the length or polish of the writeup. | required |
| `unclaimed` | Repo facts: "this issue: assignees:" and "linked PRs:" (with state per PR); plus the Comments section | Passes if **all** hold: no assignee; no **open** linked PR; and no unretracted claim comment ("I'll take this", "can I work on this", "working on this", "started on this") posted within **90 days** of the capture date. A **closed, unmerged** linked PR is an abandoned attempt, not a claim, and does not fail this check on its own. Absent or empty assignee and linked-PR fields mean none, and pass. | required |
| `policy-permits-ai` | Repo facts: the "contribution policy" line, including any `AI_POLICY.md` / `AI_USAGE_POLICY.md` / PR-template disclosure it quotes or summarizes | Fails **only** on an outright ban on AI-generated or AI-assisted contributions ("we do not accept AI-generated code"). Conditions are not bans: disclosure, personal understanding, testing, and human-review requirements all **pass**, as terms to follow. Silence **passes** — a repo that states no policy is not restricting anything. An `AGENTS.md` file is a positive signal and passes. | required |
| `newcomer-signposted` | The issue's labels and body | Carries a `good first issue`, `good-first-issue`, `beginner`, or `help wanted` label, or the body names where to start. | preferred |
| `starting-point-named` | The issue body and comment thread | A maintainer names a specific file, function, or directory to change, or states the expected shape of the fix. | preferred |
| `maintainer-responsive` | Repo facts: "maintainer first-response sample" | The sample's typical first response is within **14 days**. | preferred |

## Verdict rule

**Accept if and only if every `required` check grades `pass`.** Any single
required `fail` rejects the issue.

`unclear` counts as **fail** — a first issue I cannot verify is not one I
should take. The exception is where a pass condition states that absent
evidence passes: an empty assignee or linked-PR field grades `pass` on
`unclaimed`, and a silent contribution policy grades `pass` on
`policy-permits-ai`. Those are answers, not gaps.

`preferred` checks never change the verdict. They rank the accepted issues:
more preferred passes means a better first issue, and they are reported in the
summary as reasons to choose one accepted candidate over another.
