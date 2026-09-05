# One Hire

An AI hiring tool that qualifies and classifies candidates the way an experienced operator would, in a fraction of the time it takes by hand. It captures a batch of candidates from a search, judges each one against a role rubric with reasoning and evidence, drafts a personalized outreach note, and stops at an approval queue. A person approves. The tool does the reading, the judgment call, and the draft.

Architecture: ./ARCHITECTURE.md
Playbook, live: https://yashasvishailly.com/kits

## The judgment layer

The core of One Hire is the qualification. For each candidate it decides fit as yes, no, or uncertain, attaches a confidence, and shows the evidence behind the call, the reason for an exclusion, and what evidence it's still missing. It surfaces its own uncertainty and flags when it might be hallucinating.

This is the part a recruiter does in their head over hours of reading. One Hire does it consistently across a whole batch in minutes, and it shows its work, so a person can trust a call or overturn it. The human stays the decision maker. The tool removes the hours.

## What it does

- **Capture.** A browser extension captures the visible batch of candidate results from a search page, on a user action. No auto login, no auto scroll, no bulk profile opening.
- **Qualify and classify.** Each profile is judged against the role rubric. The tool returns the fit call, a confidence, the evidence it used, an exclusion reason, missing evidence, and a hallucination flag.
- **Draft.** For a fit, it writes a short, personalized outreach note in a configured voice.
- **Review.** Every candidate lands in an approval queue. A person approves, edits, rejects, or marks the classification wrong and records why.
- **Ready to send.** Approval flips a candidate to ready, with a timestamped audit log. The tool never sends the outreach itself.

## Design principles

- **Human approval before anything leaves the queue.**
- **Evidence on every call.** Each fit decision carries the evidence it used and flags what it's missing.
- **No dark pattern automation.** No auto login, no auto navigation, no bulk sending, no scraping of contact details, and no gender inference from names or photos.
- **Auditable.** Every state change is logged with a timestamp.
- **Local first.** Profile data stays local during a run.

## Stack

- Browser extension for user triggered capture
- Local Node service, review dashboard, and JSON audit store
- A model called with a strict output schema for the qualification, plus an offline rule mode for development
- CSV and JSON evidence export

## What this repository is

A case study and the system architecture. See `ARCHITECTURE.md`. One Hire is a paid product, so the qualification rubric, the prompts, the scoring, and the outreach templates are not here. No candidate data and no client data appear in this repository.

## Who built it

Yashasvi Shailly. Designed and built solo.
