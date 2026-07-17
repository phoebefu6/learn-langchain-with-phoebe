# Presenter notes - Builder session 7 · Human-in-the-loop and time travel

Student-facing page: courses/b7-hitl-time-travel.html. These notes are for the presenter only.

## Preflight (do the night before, not the morning)

- [ ] venv active with `langchain>=1.3,<2` and `langgraph>=1.2,<2`; both engines tested (Claude key + one call, `ollama run llama3.1` warm)
- [ ] Seeded data.csv present, plus a SCRATCH `reports/` directory created in the project - empty it before the session; the demo's drama depends on the room watching files appear (and NOT appear) in it
- [ ] Keep a Finder/file-explorer window on the reports/ folder on the projector during Demo 1 - the file appearing on approve is the visual payoff, do not narrate it from a terminal ls
- [ ] datadesk_v4.py (the gated-write demo file) pre-written and rehearsed END TO END: approve run, reject run, edit-then-approve run - all three, timed
- [ ] A b6 thread with 4-5 turns already in a SqliteSaver db for Demo 2's rewind (rehearsal leftovers are perfect here - for once, do NOT delete the db; this is the opposite of b6's preflight)
- [ ] Rehearse the reject beat: run, pause, then conspicuously close the laptop lid or walk away for 3 seconds - "no resume, no write" plays better performed than explained
- [ ] Projector zoom tested; the interrupt-flow SVG (agent lane / human lane) is the anchor visual
- [ ] If presenting to a mixed room, skim leader session a4 beforehand - tonight is its exact implementation and someone will ask

## Run of show

| Min | Beat | Notes |
|-----|------|-------|
| 0-3 | Welcome + the reveal | "Last week's memory feature was secretly a control feature." One sentence on the arc: b6 built the checkpoint, tonight we refuse to resume it |
| 3-8 | Part 1: why gates | The mistake-cost vs delay-cost rule + the Replit story. Do NOT let this become a doom segment - land it as "the pause is one compile argument" and move |
| 8-14 | Part 1: interrupts + the three verbs | The gate/peek/verbs prompt-box on zoom; invoke(None, cfg) as "no new input, just continue" - say it twice, it is the idiom people forget |
| 14-18 | Part 2: time travel | Fork SVG; the "git for conversations" rename does more work than any formal definition - lead with it |
| 18-32 | Demo 1: DataDesk asks permission | Approve first (file appears in the Finder window - pause on it), reject second (walk-away theater, then show the empty folder), edit-then-approve third (update_state the path, file lands at YOUR name). Full triangle, in that order |
| 32-40 | Demo 2: rewind Tuesday | List history, replay from checkpoint 3, fork with a different question, read both endings aloud side by side |
| 40-42 | Two-altitudes recap | HumanInTheLoopMiddleware (b4) vs graph interrupts - same checkpoint machinery, pick your altitude. One breath |
| 42-45 | Q&A + homework pointer | Flag the dynamic-gate homework (interrupt only on overwrite) - it is the bridge from policy gates to judgment gates |

## Never-cut beats

1. The reject-then-edit gate sequence in Demo 1 - approve alone looks like a confirm dialog; reject proves the no-op is safe, and EDIT proves the human is a real node in the graph. The triangle needs all three sides; if time collapses cut Demo 2 entirely before trimming this
2. The pending state made visible BEFORE approval - print s.next and s.values["path"] and point: "you are approving the actual write, not a vibe"
3. "The gate is a checkpoint nobody resumed yet" - the sentence that fuses b6 and b7 into one mental model
4. The fork comparison (even 60 seconds) - two futures from one past is the debugging superpower; without it time travel sounds like a party trick

## Cuts if long

- Demo 2 steps 1-2 (history listing + replay) can compress to a pre-run screenshot; keep the fork live
- Part 2 self-study card (the incident workflow) - never present it, point at it during Q&A instead
- The flaky-Friday example - one line: "time travel makes agent failures sit still"
- The two-altitudes recap - can shrink to one sentence during the homework pointer

## Q&A landmines

- "Won't humans just rubber-stamp everything?" - Yes, if you gate everything - that is why the rule is economic (mistake cost vs delay cost), and why the gate shows the exact pending action. Selective gates with real payloads keep reviewers awake; blanket gates put them to sleep.
- "What if nobody ever approves - does it leak?" - The pause is a parked checkpoint row in your database, not a hanging process. It costs a row, not a thread. Production adds expiry/escalation policy on top - that is app plumbing, not graph code.
- "Replay gave a slightly different answer than the original run." - Correct and important: replay re-executes LIVE model and tool calls; determinism grows with how much state you pin. For exact forensics you also want traces - which is b10's LangSmith session. Park it visibly.
- "Is this the same as b4's HumanInTheLoopMiddleware?" - Same concept, two altitudes: middleware gates tool calls at the create_agent level by configuration; interrupts gate ANY node at graph level. Same checkpointer underneath - which is why both needed b6 to exist.
- "Can the human change the DRAFT, not just the path?" - Yes - update_state can rewrite any state key, text included. Great instinct; it is exactly how editorial-review flows get built on this machinery.
- "Who is allowed to approve?" - The graph only sees "resumed"; WHO may resume is your app's authz problem. In regulated settings, log the approver identity next to the thread_id - the governance folks upstairs (leader a4) are being taught to ask for exactly that audit trail.
