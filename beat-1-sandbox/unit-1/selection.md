# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/57

**Verdict output**

````
## Summary

All three issues share the same repo-level facts (repo `codepath/pathreview-ai301-fa26-s3`, not archived, last push 2026-09-16 by a human collaborator, `docs/CONTRIBUTING.md` and PR template have no AI ban — both required repo-level checks pass for all three). The differentiator is `unclaimed`: issues #53 and #60 each already have an **open** PR that says "Fixes #NN," while #57 has none (the several claim *comments* on it don't count against it, per the Path Review house rule).

- **#53** (PII scrubber / parenthesized phone numbers) — well-scoped, well-signposted, but **PR #77 ("Fixes #53") is open** → fails `unclaimed` → **reject**.
- **#60** (Faithfulness checker `text: None` crash) — well-scoped, well-signposted, but **PR #80 ("Fixes #60") is open** → fails `unclaimed` → **reject**.
- **#57** (Tech detector counts vendored/build files) — one-line-cause bug in a single named file (`agent/tools/tech_detector.py`), two named tests, no assignee, no open/linked PR → **accept**.

**#57 is the one to take.** It's the only survivor, and it fits your profile well: a single, precisely-specified regex/path-matching bug in one file, verifiable in an hour with the two named unit tests, no environment/Docker setup needed (pure Python, per multiple repro reports in the thread).

```json
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/57",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "Last 5 default-branch commits all authored by Aburke225 (human collaborator), most recent 2026-09-16, within 180 days"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "Not archived; last push to main 2026-09-16, within 180 days"},
      {"name": "scope-bounded", "grade": "pass", "evidence": "Single bug: one exclusion-pattern fix in agent/tools/tech_detector.py, two named tests, no umbrella/repo-wide language"},
      {"name": "unclaimed", "grade": "pass", "evidence": "No assignee; no linked or cross-referenced PR in the timeline (only two 'referenced' commit events, not PRs); claim comments exist but house rule excludes classmate claims"},
      {"name": "policy-permits-ai", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and .github/PULL_REQUEST_TEMPLATE.md state no AI restriction; several contributors on other issues in this repo disclose AI-assisted workflows without pushback"},
      {"name": "newcomer-signposted", "grade": "pass", "evidence": "Carries the 'good first issue' label"},
      {"name": "starting-point-named", "grade": "pass", "evidence": "Issue names agent/tools/tech_detector.py and the two failing tests test_node_modules_excluded / test_build_directory_excluded"},
      {"name": "maintainer-responsive", "grade": "unclear", "evidence": "No maintainer (Owner/Member/Collaborator) comment appears anywhere in the thread to time a first response from"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/53",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "Last 5 default-branch commits authored by human collaborator Aburke225, most recent 2026-09-16"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "Not archived; last push 2026-09-16, within 180 days"},
      {"name": "scope-bounded", "grade": "pass", "evidence": "Single regex fix in safety/pii_scrubber.py, four/five named tests, no repo-wide or design-debate language"},
      {"name": "unclaimed", "grade": "fail", "evidence": "Open PR #77 'fix: redact parenthesized US phone numbers in PII scrubber' with body 'Fixes #53.' is still open"},
      {"name": "policy-permits-ai", "grade": "pass", "evidence": "CONTRIBUTING.md and PR template contain no AI restriction"},
      {"name": "newcomer-signposted", "grade": "pass", "evidence": "Carries the 'good first issue' label"},
      {"name": "starting-point-named", "grade": "pass", "evidence": "Issue names safety/pii_scrubber.py and its phone_us pattern, plus four specific tests"},
      {"name": "maintainer-responsive", "grade": "unclear", "evidence": "No maintainer comment appears in the thread"}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/60",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "Last 5 default-branch commits authored by human collaborator Aburke225, most recent 2026-09-16"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "Not archived; last push 2026-09-16, within 180 days"},
      {"name": "scope-bounded", "grade": "pass", "evidence": "Single one-line fix in rag/evaluator/faithfulness_checker.py's check(), one named test"},
      {"name": "unclaimed", "grade": "fail", "evidence": "Open PR #80 'fix: tolerate None text in faithfulness checker context chunks' with body 'Fixes #60.' is still open"},
      {"name": "policy-permits-ai", "grade": "pass", "evidence": "CONTRIBUTING.md and PR template contain no AI restriction"},
      {"name": "newcomer-signposted", "grade": "pass", "evidence": "Carries the 'good first issue' label"},
      {"name": "starting-point-named", "grade": "pass", "evidence": "Issue names rag/evaluator/faithfulness_checker.py line 38 and test_none_context_chunk_text"},
      {"name": "maintainer-responsive", "grade": "unclear", "evidence": "No maintainer comment appears in the thread"}
    ],
    "verdict": "reject"
  }
]
```
````

---

## Eval iterations

**Run history**

My runs, in order:

1. `--limit 3` smoke run — **0 graded**. Every issue returned `ERROR (claude exited 1)`
   because the `claude` CLI the harness shells out to had an expired OAuth session. No
   rubric was exercised; I re-authenticated and started over.
2. `--limit 3` smoke run — **2/3**. `issue-02` and `issue-03` agreed. `issue-01` was a
   false reject: my `scope-bounded` check failed a conda docs task whose gold label is
   `accept`.
3. `--only issue-01,issue-05,issue-10,issue-20` — **3/4**. After loosening
   `scope-bounded`, `issue-01` flipped to `accept` (correct) and the two umbrella
   canaries `issue-05` and `issue-10` still rejected (correct), but `issue-20` flipped
   to a false `accept`.
4. `--only issue-20,issue-09,issue-06,issue-14` — **4/4**. After adding the
   unendorsed-feature-request clause, `issue-20` rejected correctly and the three
   clear-accept canaries I was most worried about damaging all still accepted.
5. `--only issue-12` — **1/1**. A single-issue check that my `policy-permits-ai` check
   catches the one `policy` issue in the set, because the category floor fails the whole
   run if that category has no match.
6. Full run with `--save-run eval-run.txt` — **18/20, PASS**, category floor met
   (`claimed 4/4  clear-accept 7/8  dead-repo 3/3  policy 1/1  scope 3/4`). This is the
   run committed as `eval-run.txt`.

**Issue analysis**

`issue-19` (zxcalc/zxlive#517, "Selecting large subgraphs in proof mode freezes the UI").

My rubric decided **reject**; the gold label is **accept**. The harness reported the
cause as `failed: scope-bounded`.

My `scope-bounded` check fails an issue that "lists sub-items each meant to become its
own separate issue or PR." The body of `issue-19` opens with "There are two potential
causes which should be fixed:" followed by a numbered list, and then a second numbered
list headed "Additional suggestions:" containing three more items — five numbered items
in total. Read literally against my wording, that is a list of sub-items, so the check
failed and the single required failure rejected the issue.

The gold label reads the same text differently, and I think correctly. The two "potential
causes" are not two pieces of work; they are two hypotheses about the cause of *one*
symptom — a frozen UI — and fixing either one is a complete response to the issue. The
three "additional suggestions" are explicitly optional performance ideas, not required
deliverables. The issue was filed by a COLLABORATOR, carries `Type: bug` and
`Priority: High`, has no assignee and no comments. A maintainer diagnosing one bug and
naming the places to look is the *best* case for a newcomer, not a warning sign.

The distinction my wording misses is between a list of **work items** and a list of
**causes or suggestions for one symptom**. One symptom is one issue, however many
candidate explanations the reporter enumerates.

**Check rationale**

The check I am quoting is `scope-bounded`, from the `rubric.md` uploaded to
`tools/issue-select/`. Its pass condition currently reads, in full:

> Ask one question: **could one person land this in a single pull request?** Fails only if **any** of these is true: the issue calls itself an umbrella, tracking, meta, or epic issue, or lists sub-items each meant to become its **own separate issue or PR**; the work is described as applying **repo-wide** ("across the codebase", "every module", "all call sites"); the thread shows the design still being debated with no maintainer having settled it; a maintainer states the fix reaches core internals; the issue is a pure usage or support question ("how do I get this to work?") rather than a request for a change; or the issue is an **unendorsed feature request** — see the next sentence. **Unendorsed feature request** means *all* of: the issue proposes **new functionality** (not a bug fix or a docs task); its author is not a maintainer (author_association `NONE`, `CONTRIBUTOR`, or `FIRST_TIME_CONTRIBUTOR`); **no** maintainer comment in the thread supports building it; and it carries **no** maintainer-applied acceptance label (`good first issue`, `help wanted`, `accepted`, `approved`). When all four hold, an unmade product decision is hiding inside the request no matter how tidy its formatting, and the check fails. Any one of these rescues it: a maintainer opened it, a maintainer endorsed it in the thread, or a maintainer labelled it. This clause **never** applies to bug reports or documentation tasks. **Detail is scoping, not sprawl**: a long body, sub-headings, a bullet list of requirements, or edits to a handful of **named** files that ship together in one PR all **pass** — a precise specification of one deliverable is the best-scoped kind of issue, not an umbrella. A terse body, a missing reproduction, or a bare acceptance-criteria checklist likewise **pass**. Grade the size of the work asked for, not the length or polish of the writeup.

Almost all of that wording is scar tissue from a specific run. The check began as a
short list of disqualifiers, and the `--limit 3` smoke run immediately false-rejected
`issue-01`, a conda documentation task whose body has three sub-headings under "Proposed
changes" and edits three named files. My original wording treated that structure as an
umbrella. It is the opposite: someone scoped that work precisely. That produced the
governing question at the front of the check — "could one person land this in a single
pull request?" — and the explicit sentence that **"Detail is scoping, not sprawl"**, so
that length and formatting can never by themselves sink an issue.

Loosening it that far immediately cost me `issue-20`, a tidily formatted feature request
with success criteria and a named surface that my newly permissive check waved through.
Gold rejects it. The thing actually wrong with `issue-20` is not its scope but its
provenance: it was opened by `cursor[bot]` with `author_association: NONE`, carries no
labels, and has zero comments — nobody with authority has agreed the feature should
exist. Hence the four-part unendorsed-feature-request clause, deliberately narrowed so
it applies only to new functionality and never to bug reports or documentation tasks,
which is why `issue-01` and the maintainer-filed bugs are untouched by it.

**Trade-offs**

The permissiveness that rescued `issue-01` is what I still pay for, and I can name the
exact price: `issue-19`, analysed above, is a false reject, and `issue-15` ("years of
design debate and two abandoned PRs behind a friendly label") is a false accept — the
two disagreements in my committed run. `issue-15` is the sharper lesson. My check does
contain a clause for design debate, but it requires the thread to show the design "still
being debated with no maintainer having settled it," and on an issue where the debate
happened over several years and simply went quiet, there is no live argument for that
clause to catch. Silence after an exhausted debate reads to my rubric exactly like
consensus.

I re-ran canaries rather than trusting the loosening. After adding the
unendorsed-feature-request clause I re-ran `--only issue-20,issue-09,issue-06,issue-14`:
`issue-20` rejected correctly, and critically `issue-09` — "old but valid bounded
feature; the 2022 claim is stale and the maintainer invited takers" — still accepted.
That was the canary I cared about, because it is a *feature request* and would have been
the first casualty of a clause written any wider. All four agreed, which is how I know
the clause bought `issue-20` without costing me the clear-accepts.

The case I accept it will miss: a stalled-by-exhaustion issue like `issue-15`, where the
disagreement is in the archive rather than in the live thread. Detecting it needs a
signal my rubric does not currently read — issue age against abandoned linked PRs — and
I chose not to add it, because a check that rejects on abandoned attempts would also have
rejected `issue-09`, where a stale claim is exactly what made the issue available. At
18/20 with the category floor met, trading a clear-accept for an arguable scope call is
a bad deal.

---

## Selection rationale

**Selection rationale**

*Fit to my interests and the time available.* I can read and debug Python, C/C++, and
JavaScript/TypeScript, and what I care about is making a small change that genuinely
matters rather than a large change nobody runs. Issue #57 is a Python bug in one file,
`agent/tools/tech_detector.py`: the tech detector counts vendored and build-output
directories when it infers a repo's languages, which skews the result. It comes with two
named failing tests, `test_node_modules_excluded` and `test_build_directory_excluded`, so
I have an unambiguous definition of done and no environment or Docker setup to fight. I
have a few hours for this, and this is a one-sitting change I can actually verify.

*What the verdict identified correctly, and what I weighed that the rubric could not.*
The verdict did the claim archaeology better than I would have by hand. It found open PRs
saying "Fixes #53" and "Fixes #60" on my other two candidates and rejected both on
`unclaimed`, while correctly applying the Path Review house rule so that classmates'
claim *comments* on #57 did not count against it — an open pull request is a real claim
whoever opened it; a comment in a classroom repo is not. It also confirmed the repo is
alive (last push 2026-09-16 by a human collaborator) and that nothing in `CONTRIBUTING.md`
or the PR template restricts AI-assisted work. What I weighed that the rubric could not:
`maintainer-responsive` graded `unclear` on all three candidates because no maintainer has
commented anywhere in these threads, and my verdict rule would normally treat `unclear` as
a failure. It did not sink #57 only because that check is `preferred`. In a real
open-source repo that silence would worry me; in a course repo built for students to
practise on, I read it as normal rather than as neglect. That is a judgement about
context, and it lives outside anything my rubric can see.

*Anticipated difficulty in claiming it.* Low on the mechanics and moderate on the
competition. There is no assignee and no linked PR, so nothing procedural is in my way.
But #57 already carries several classmate claim comments, and the house rule is explicit
that a shared issue costs nobody anything, since credit attaches to the pull request I
open rather than to whether it merges. The real risk is not being blocked — it is that
the fix is small enough that several of us will converge on nearly the same diff. I am
not claiming it yet: that comment belongs in Unit 2, after the voice guide.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
