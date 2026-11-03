# Phase gate

Read when participants request completion, review, locking, or advancement. Do not
perform a full gate after every conversational turn.

## Review decision completeness

Review current-phase material only. Mark each item complete, explicitly unresolved,
or blocking, with a short reason. Check:

1. Material stakeholder concerns and the actual decision are understood or deferred.
2. Consequential assumptions, conflicting accounts, and unknowns are explicit.
3. Credible alternatives and conditions favoring them were considered.
4. Resources, skills, operating responsibilities, and delivery dependencies fit the
   proposal, or the gap has an explicit negotiation/escalation/risk disposition.
5. Contextual numbers, cost basis, incurred/committed costs, and second-order effects
   are recorded without unsupported precision or double-counting.
6. Affected promises/SLOs, trade-offs, risk owners, debt, and revisit triggers are visible.
7. The chosen artifact explains the decision to its intended audience and cites evidence.
8. Negotiations are resolved or explicitly pending; no draft is treated as consent.
9. Accepted history is intact and current totals/artifact versions are consistent.
10. The participant has reviewed the proposed checkpoint and explicitly accepted it.

Do not require a particular architecture, discovering every nuance, flawless predictions,
all metrics being green, or meeting every promise. Allow justified uncertainty and known
SLO failure when disposition and consequences are explicit. Do not fabricate authority
to waive an obligation. Apply any additional current package exit requirements; challenge
ones that assume a canonical design rather than evidence of reasoning.

## Propose a checkpoint

1. Summarize established decisions and their evidence, costs, promises, risks/debt, pending
   issues, active architecture/artifact versions, and current scenario time.
2. Identify only material blockers. Propose the smallest repair; do not assign extra work
   to make a different but defensible architecture match an answer key.
3. Save a proposed snapshot at the designated path, distinctly marked unaccepted.
4. Ask: "Accept this phase checkpoint, or revise a specific item?" Acceptance must refer
   to the checkpoint, not a casual earlier approval of a diagram or recommendation.

Do not load next-phase metadata while waiting. Do not treat silence as acceptance.

## Lock after acceptance

Append the acceptance event, checkpoint ID/path, package version, scenario time, source
release list, decision/cost IDs, exact artifact versions, open obligations, and integrity
status. Store a frozen snapshot containing the accepted records or exact immutable
versions, so later comparison does not rely on mutable links. No database, permission
system, signature, or complex enforcement infrastructure is required.

Leave accepted sources, records, and artifact versions unchanged. Update the mutable
current-state view to point at the checkpoint. New facts and revised decisions will be
append-only additions. Do not retroactively change costs because an option now looks poor.

## Request the next package

Use the exact drop location and neutral ID assigned in session control. If absent, ask
the trainer for those two items without requesting story details. Example wording:

> Phase [ID] is closed; checkpoint [ID/path] is accepted. Place the next released
> package's entry file and its resources at [exact drop location]. I will wait for
> confirmation before reading its entry. Accepted history and incurred costs remain.

Record `awaiting-package`. Stop scenario advancement. Do not scan or poll the filesystem
for future files, use an archive, request the whole course, or invent the next package.
Answer process questions and inspect already released history when useful.

On explicit delivery confirmation, load Package contract from the core skill, inspect
the entry metadata, verify compatibility with the locked checkpoint, and admit the new
phase. Never rewrite the checkpoint to accommodate a conflicting package.
