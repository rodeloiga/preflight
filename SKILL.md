---
name: preflight
description: A pre-ship consolidation discipline for AI agents and the humans they report to. Use whenever anything is about to be deployed, published, released, sent, or launched, even when the user never mentions gates, checks, or sign-off. Every applicable check still runs on its own; preflight translates all findings onto one scale and delivers ONE report in two classes, Blockers and Advisories, with a single human decision attached. Blockers are presented as rulings to make, never as approvals to grant; a report with no Blockers compresses to one Approve or Reject. Preflight never fixes anything, and it never ships anything by itself.
---

# Preflight: one report, two classes, one decision

Serious work accumulates checks. A security review, an
accessibility audit, a copy review, a link check, a design
review: each is worth running, and each tends to report in its
own format, on its own severity scale, in its own file. The
failure mode is volume. The person who has to decide whether
something ships receives five documents in five dialects, and
the one finding that should have stopped the ship sits unread
in the third. Work has shipped exactly that way: a blocker,
correctly found and correctly written up, buried in a pile of
reports nobody had the attention left to finish.

Preflight is the consolidation discipline that prevents it.
The checks still run individually, as working checks, in their
own terms. But nothing is presented for a ship decision until
every finding is translated onto one scale and gathered into
ONE report. The human reads one document and makes one
decision.

Verifying work while it is being built is a companion
discipline with its own practice. Preflight governs only the
moment of the ship decision.

## Setup: the gate inventory

Before preflight can run, the project declares its inventory.
Lines with defaults may use them silently, with one exception:
the Gates line's default is discovery, and a discovered gate
list is proposed to the human, not adopted silently.

- **Gates:** the checks this project runs before anything
  ships (default: discover them from the project itself, its
  review habits, its checklists, its tooling, and propose the
  list). A gate is any repeatable check with findings: a
  security review, an accessibility audit, a privacy review, a
  copy or content review, a link and asset verification, a
  design or quality review, a legal or compliance read. The
  list belongs to the project; preflight does not impose one.
- **Blocker classes:** fixed, and not the project's to widen
  or narrow casually. Blocker is reserved for seven classes:
  security; privacy and data leak; accessibility; agency and
  dignity (anything that removes a user's exit, refusal, or
  control, or silently discards their input); violations of
  the project's own standing rules; ship-breaking defects (the
  work fails its own purpose or its specification: a broken
  checkout, a wrong price, a factual error in a publication, a
  misaddressed send); and legal or compliance defects.
  Everything else is Advisory. Membership in this list changes
  only by a human's written decision, recorded in the
  inventory's change log; a finding's class is set by the class
  definitions and the human's rulings, never adjusted by a
  gate or a consolidator to make a report cleaner.
- **Gate states:** every gate in the inventory appears in
  every report in exactly one state: PASSED (ran in full, no
  findings in its scope), FINDINGS (ran in full, findings
  listed), PARTIAL (ran with reduced coverage, the coverage
  stated), NOT RUN (did not run, the reason stated), or
  SKIPPED (does not apply to this ship, the reason stated).
  A gate that errored is NOT RUN with the error as its reason;
  it is never silently PASSED. Silence is not a state.
- **Precedents and version:** the inventory carries a version
  number and a change log. Human rulings on findings are
  recorded in it as standing precedents, so the same finding
  is not re-litigated ship after ship; a ruling that accepts
  a risk records its owner and its expiry, and an expired
  acceptance returns as a fresh finding. Each report states
  the inventory version it ran under and what changed since
  the last report.

## The law of the report

- **Findings only.** Preflight never fixes, applies, or clears
  anything. It consolidates and triages. Fixes happen in the
  work, under their own process, and are then re-checked.
- **One report per ship.** The report is the only gate document
  the decision maker is asked to read for that ship. The
  individual gate outputs stay in the project as evidence;
  they are never separate asks.
- **One cause, one finding.** Findings are merged by root
  cause across gates. Five gates reporting one cause produce
  one entry tagged with all five gates, not five findings;
  counts in a report count causes, so volume never inflates
  the Blocker total or hides its shape.
- **Inputs are listed.** The report names what it was built
  from: the gate outputs, and any build-time verification logs.
  A verification log's Not verified entries are a required
  input and are carried into the report as coverage caveats,
  so a ship decision never rests on checks the build already
  admitted it skipped.
- **Read in full before saying "ready."** Whoever presents the
  ship must have read the entire consolidated report, including
  Advisory, before telling anyone the work is ready. A gate is
  not passed until its findings have actually been read. A
  clean-looking summary over an unread report is the exact
  failure this discipline exists to prevent. The read is
  demonstrated, not attested: the presenting message restates
  every Blocker in its own words, and its counts match the
  report's counts exactly.
- **Blocker present means BLOCKED.** Any Blocker item makes the
  report a blocked report. The ask is then "rule on these
  blockers," never "approve." Presenting a blocked report as
  an approval request, with the blockers in the small print,
  is a violation of this discipline, not a style choice.
- **Clean is a defined state, not an impression.** A report is
  clean only when it has zero Blockers AND every Blocker-class
  gate is PASSED or FINDINGS (ran in full). A Blocker-class
  gate in PARTIAL or NOT RUN state makes the report not clean,
  however quiet its findings are: unknown is not clean. Such
  gates are named in the report's first lines, and the
  decision then includes them (accept the coverage risk in
  writing, or wait for the gate). A clean report compresses
  the decision to a single Approve or Reject. The report itself
  never ships anything. Approval stays a human act, and this
  discipline grants no permission at any point.
- **No workarounds (the anti-workaround law).** When the work
  collides with a security policy, a schema rule, or a standing
  posture (a content security policy, a CORS rule, an auth
  boundary, a data-handling rule), the collision is itself a
  Blocker finding. A proposed fix that invents a runtime
  workaround, an ad-hoc per-route exception, or a monkey-patch
  to get past the policy is not a fix and is never presented
  as one. The remedies are systemic: change the design so the
  policy is satisfied, or bring the policy change itself to
  the human as the decision. This law exists because the
  workaround is always available and always tempting: a
  per-route exception to a security header policy, for
  instance, where shipping an external file under the existing
  policy satisfied it all along. The law has a one-line test,
  applied to every proposed remedy: does it satisfy the policy
  as written, or carve an exception to it? Only the first is
  a fix.
- **Scope stays decoupled.** Unbuilt features and future
  capability proposals never block a clean deliverable and
  never ride inside its report as findings. They are recorded
  as separate backlog items, specified on their own and ruled
  on their own. A report that mixes "this is broken" with
  "wouldn't it be nice" trains its reader to skim both. The
  line is exact: a deviation from the specification or the
  standing rules is a finding; a gap between the work and the
  ideal is backlog.

## Which gates apply

The inventory decides, per surface. As a starting shape:

- **A web page or site release:** every applicable gate in the
  inventory, and in particular any gate covering third-party
  content and tracking, security (for any surface with forms,
  sign-in, or data handling), accessibility, copy and content
  verification, and design quality.
- **An application or interactive release:** the same, plus the
  project's design and interaction reviews, and the copy gate
  over every user-visible string.
- **A document, publication, or send:** the copy and fact
  review, the privacy review, and any compliance read the
  project runs.

Whatever the surface, the rule of the inventory holds: a gate
that does not apply is listed as SKIPPED with its reason.

## Severity mapping

Each gate keeps its native scale while it runs. Consolidation
translates by class, not by label:

- **Security:** a confirmed exploitable finding, an exposed
  secret, broken access control, or a policy collision (see
  the anti-workaround law) is Blocker. Hardening gaps and
  defense-in-depth notes are Advisory.
- **Privacy and data leak:** personal data exposed, sent
  somewhere it was not approved to go, or collected beyond the
  project's stated purpose is Blocker. Documentation and
  retention hygiene is Advisory.
- **Accessibility:** a barrier (content unreachable, focus
  lost or trapped, a required announcement missing, contrast
  below the project's standard, motion that ignores a
  reduced-motion setting) is Blocker. Awkward but complete
  rendering is Advisory.
- **Agency and dignity:** any behavior that silently deletes
  user input, removes an exit or a refusal path, or forces an
  alert on someone is Blocker, whatever the gate that found it
  called it. Friction and tone findings are Advisory unless they
  cross that line.
- **Standing-rule violations:** a finding that breaks a rule
  the project has adopted in writing (a privacy commitment, a
  no-tracking rule, an approval requirement for public text,
  a naming or branding law) is Blocker. Ordinary consistency
  drift is Advisory.
- **Ship-breaking defects:** the work fails its own purpose or
  its specification (a checkout that errors, a wrong price, a
  factual error in a publication, a message sent to the wrong
  recipient) is Blocker, whatever gate or test surfaced it.
  Defects that degrade without breaking are Advisory.
- **Legal and compliance:** a missing required disclosure, a
  consent flow that does not match its policy, a licensing or
  regulatory defect is Blocker. Compliance polish and
  documentation hygiene are Advisory.
- **Everything else** (craft, taste, performance polish,
  design quality notes) is Advisory by design. Advisory is not a
  dismissal; it is the list the decision maker reads after the
  blockers, grouped by disposition (fix, backlog, accept) with
  counts per group, so its volume stays readable.

When a finding plausibly sits in both classes, it is classed
as a Blocker and the report says why. Blocker inflation is
corrected by the human's ruling, never by the consolidator's
optimism.

## Living-document reconciliation

Verification usually covers the artifact a job produced. It
rarely covers the project's living documents (decision logs,
READMEs, requirement sets, specs of record, plans), so those
drift silently: every check passes while the record of
record states facts the project has already moved past.

- **Trigger.** Any job that changes a fact of record (a
  decision lands, a deploy state changes, a feature ships,
  an external route or provider goes live) owes a
  reconciliation pass before it reports.
- **Method.** (1) Name the fact in one line. (2) Search the
  project's living documents for that fact's own terms.
  (3) Reconcile each hit in the same job, or name it as
  unreconciled. Search first; read only where the search
  lands.
- **Dated records are exempt.** Snapshots, dated reports,
  and historical logs are never edited. A living document
  that quotes a superseded claim only inside a dated
  correction note is reconciled, not stale.
- **Reporting.** The report carries a Reconciliation line
  (see the format below). Unreconciled items are named:
  Advisory for ordinary drift; Blocker, standing-law class,
  when the stale document misstates a privacy-relevant
  feature, a consent or access rule, or itself claims to
  be the record of record for the fact. Unreconciled items
  also seed the Not verified list.
- **The calendar half.** Drift also happens outside jobs.
  Pair this check with a scheduled freshness audit of the
  project's living documents (weekly is a workable
  cadence): the audit flags drift, it does not fix it.
  This section is the change-time half; the audit is the
  calendar half. A periodic check that both halves are
  actually running is part of the discipline, not an
  optional extra.
- **The change register.** Keep one register of
  fact-of-record changes. A job that changes such a fact
  files its entry in the same job: the fact, old form to
  new form, every surface touched, the source, and the
  check artifact (the search, extraction, report, or live
  check that proves the change landed). The report's
  Reconciliation line cites the entry. A change whose
  entry has no artifact, or whose artifact does not show
  the change on every named surface, is unreconciled:
  Advisory for ordinary facts; Blocker, standing-law
  class, when the fact is public-facing. The scheduled
  freshness audit reconciles register entries against the
  surfaces and flags missing, stale, or contradicted
  artifacts. A correction recorded from its edit list
  alone, with no post-change check across the whole
  surface set, is how a fixed error survives its own fix.

## Standard texts are diffed against canon

A file that claims to be a standard text (a license, a
legal notice, policy boilerplate) is verified by diffing
it against the canonical copy, never against a sibling
copy and never by its presence, filename, or copyright
line. Keep one canonical copy of each standard text in a
known place; packages copy from canon. A mismatch is a
Blocker, legal and compliance class. A scheduled audit
that diffs standard texts across the project's trees
against canon is the backstop for copies introduced
outside a ship.

## Floor integrity

Every check verifies the deliverable against the bar. This
check runs the other direction: it diffs the change itself
against the project's written floor and asks whether the bar
was quietly lowered to reach green. It runs on every ship, and
its result is a required section of the report.

A project's floor is its written quality bar: the standing
rules, budgets, thresholds, registries, and check configurations
the project has committed to, kept in one named place in the
project records. A project with no written floor runs this
check as NOT RUN until one exists.

Watch the diff for the five cheapest roads to green:

1. **The threshold moved.** A stated floor, budget, or severity
   edited down inside the same change it was failing.
2. **A test got easier.** A check skipped, deleted, or relaxed
   (an assertion removed from a test that stayed; a pinned
   expectation adapted) instead of the work fixed. Adaptations
   may be legitimate; they are listed either way, and the human
   rules.
3. **A checker got silenced.** A suppression added, a file
   excluded from a sweep, a verification scoped narrower than
   its report claims.
4. **Work is unfinished.** A stub, placeholder, or TODO standing
   where the implementation belongs, shipped undisclosed.
5. **An exception appeared.** A new exemption in any registry
   without a decision behind it.

Tightening is silent; only loosening surfaces. The check
reports the rule and the location, never a secret value. A
check that could not run is NOT RUN, never HELD; on a ship,
Floor integrity in NOT RUN means the report is not clean. A
WEAKENED item against a standing rule or a committed floor is
a Blocker, standing-law class; against a project-local target,
an Advisory, unless the project's own documents make it a
Blocker.

## Report format

Saved with the project's records as
`preflight-report-<YYYY-MM-DD>.md`:

```
# Pre-flight report: <project / surface>, <date>
Build or version: <id>
Report version: <n> (supersedes v<n-1> when a re-check)
Inventory version: <n> | Changes since last report: <summary>
Inputs: <gate outputs; verification logs, incl. their Not
  verified entries, carried below as coverage caveats>

## Gate states
- [gate]: PASSED / FINDINGS / PARTIAL (coverage: <what ran>) /
  NOT RUN (reason) / SKIPPED (reason)

## Coverage caveats
<Blocker-class gates not fully run, and Not verified items
  from the inputs. Present here, in the report's first lines,
  never buried. "None" is a claim the states above must back.>

## Reconciliation
<Facts of record this ship changed; living documents
  reconciled; unreconciled items named, or "none.">

## Floor integrity
HELD / WEAKENED (<items, each with the rule and its location>) /
  NOT RUN (<reason>)

## Blockers (<n causes>)
- [gates that found it] Finding, in one sentence, with its
  evidence and the proposed fix or the decision it needs.

## Advisories (<n>: fix <a> / backlog <b> / accept <c>)
- [gate] Finding, one sentence, proposed disposition.

## Sign-off
Read in full by: <presenter>, <date>
Decision: pending / approved / approved with rulings noted /
  rejected / blocked / accepted-risk (owner, expiry)
```

A re-check after fixes is a new version of the same ship's
report, superseding the previous one and stating what changed;
it is never a fresh report that quietly forgets the blocked
version existed.

The message that delivers a ship decision attaches or links
this report and states the Blocker count, and any Blocker-class
gate not fully run, in its first lines. No other gate document
is attached to the same ask.

## Presenting a blocked report

When the report carries Blocker items, the presenting message
uses this shape, one block per blocked ship, so the ruling
being asked for is unmistakable:

This block is kept identical in shape to the escalation block
in the companion verification-loop skill; the two are twin
copies and are kept in sync (see the README's provenance note).

```
### ESCALATION: HUMAN INPUT REQUIRED

**Blocked ship:** [the specific deliverable, release, or send]
**Blockers:** [<n> causes, by class]

For each Blocker:
1. The obstruction:
   [One or two sentences: the finding, its class, and its
   evidence.]

2. Evaluated options:
   - Option A: [systemic remedy]. Trade-off: [risk / downside]
   - Option B: [systemic remedy, or the policy change itself].
     Trade-off: [risk / downside]
   - Option C: [accept the risk and ship]. Owner: [name].
     Expiry: [date the acceptance lapses and the finding
     returns].
   (Remedies are systemic, per the anti-workaround law; no
   workarounds are listed as options, and no false binaries
   are built on self-imposed local constraints. Accept-risk
   appears only as itself, in writing, never disguised as a
   fix.)

   Recommendation: [the presenter's pick, with its reason in
   one line. The presenter read the whole report; they carry
   a pick.]

3. Required rulings:
   [ONE line per Blocker, each answerable in a word.]
```

A blocked report never ends in an approval ask. It ends in
the ruling lines.

## A worked example

A small site release, consolidated. Six gates in the
inventory. The security gate errors on a tool failure; the
accessibility gate runs fully and finds one barrier (a form
error that screen readers never announce); the copy gate and
the fact gate both flag the same wrong price, one root cause;
two gates pass; one does not apply and is SKIPPED with its
reason.

The report does not read clean, and not only because of the
price. Its first lines name the security gate as NOT RUN
(Blocker-class, error stated), so the decision cannot be a
bare Approve. Blockers: two causes (the unannounced form
error; the wrong price, tagged with both gates that found
it). The presenting message restates both in its own words,
recommends fixing the price and the announcement and re-running
security before any ship, and ends with one ruling line per
Blocker plus one for the coverage gap. The human rules: fix
both, re-run security, resubmit as report v2. Nothing shipped
on v1, and v2 supersedes it with the diff stated.

## What preflight is not

- It is not a fixer. It never edits the work, clears a
  finding, or grades a gate's homework leniently to reach a
  clean report.
- It is not a shipper. A clean report authorizes nothing by
  itself; the human's approval is the ship, every time.
- It is not a substitute for running the gates. Consolidating
  findings from checks that never ran produces a tidy,
  worthless report. The gates run first, in full; preflight
  is the last step, not the only one.
