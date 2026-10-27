# preflight

A pre-ship consolidation discipline for AI agents and the
humans they report to, written as a portable skill. Every
check a project runs still runs. Their findings are translated
onto one severity scale and delivered as ONE report, so
the person deciding whether something ships reads one document
and makes one decision.

## Why it exists

It was specified by a practitioner whose projects had grown a
full bench of review gates: security, accessibility, privacy,
copy, design. Each gate did its job, and each reported in its
own format, on its own scale, in its own file. The volume
outgrew the attention available to rule on it. The breaking
incident was quiet: a build shipped while a gate's blocker sat
unread inside a complete, correct report that nobody had
finished reading. The finding existed. The process failed.

Preflight is the discipline he set in response. Gates keep
running individually, as working checks. But no ship is
presented on piecemeal reports ever again: one consolidated
report, two classes, one decision, and a presenter who has read
every line of it before using the word "ready."

## What it does

- Consolidates every applicable gate's findings into one
  report, translated onto a single severity scale.
- Reserves Blocker for seven classes only: security, privacy
  and data leak, accessibility, agency and dignity, violations
  of the project's own standing rules, ship-breaking defects,
  and legal or compliance defects. Everything else is Advisory,
  with a proposed disposition.
- Gives every gate a state in every report: PASSED, FINDINGS,
  PARTIAL, NOT RUN, or SKIPPED, with coverage and reasons.
  Clean is defined against those states, so a gate that never
  ran can never read as a pass.
- Merges findings by root cause across gates and counts
  causes, so one problem reported five times cannot bury or
  inflate the report.
- Makes a Blocker report a blocked report: it is presented as
  rulings to make, in a fixed escalation format, never as an
  approval request with blockers in the small print.
- Compresses a clean report to a single Approve or Reject, and
  ships nothing by itself. Approval stays a human act.
- Treats a collision with a security policy as a finding in
  its own right. Workarounds and ad-hoc exceptions are never
  presented as fixes; the remedies are a design that satisfies
  the policy, or a ruling on the policy itself.
- Keeps scope decoupled: unbuilt features never block a clean
  deliverable and never ride inside its report.

## Use it with any AI

The skill is a single Markdown file, `SKILL.md`, in the agent
skills format. An `evals.md` ships alongside it: five
adversarial scenarios (a buried blocker, a silently errored
gate, one cause reported by five gates, a policy-exception
temptation, a "just ship it") for testing whether the
discipline is actually being followed. To use it:

- **Claude, and other agents with a skills system:** drop the
  `preflight` folder into your skills directory.
- **Any other assistant:** paste `SKILL.md` into the project's
  instruction file, system prompt, or chat, and declare the
  gate inventory for your project: the checks you actually run
  before a ship. The Blocker classes and the report format work
  as written.

The inventory is the point. Preflight is only as honest as the
gates feeding it, and only as useful as the rule that the
presenter reads the whole report.

## Provenance and license

Specified by Rodel Oiga; practiced in his studio's release
process, then extracted into portable form. Two of its laws,
the anti-workaround rule and the scope decoupling rule, were
adopted from a protocol draft he submitted for review during
the same project, after both proved themselves against a real
ship decision. The draft was then hardened through two outside
audits whose findings were sorted against the studio's record
and adopted on their merits. A companion skill by the same
author, verification-loop, covers the build-time half of the
same discipline; each stands on its own. The escalation block
in this skill and the one in verification-loop are twin
copies, kept identical on purpose; if you adopt both, keep
them in sync. Licensed under MIT (see `LICENSE`); change the
license if you publish a fork.
