# Presenter notes - Builder session 6 · State, memory, persistence

Student-facing page: courses/b6-state-memory-persistence.html. These notes are for the presenter only.

## Preflight (do the night before, not the morning)

- [ ] venv active with `langchain>=1.3,<2` and `langgraph>=1.2,<2` PLUS `langgraph-checkpoint-sqlite` installed (the room will need it mid-demo - put the pip line on the whiteboard before you start)
- [ ] Both engines tested: Claude key + one call, `ollama run llama3.1` warm
- [ ] Seeded data.csv present (amount + date columns) - the pronoun follow-up ("that same column") only lands if the first answer was real
- [ ] Everyone's datadesk_v2.py from b5 is the prerequisite - send a reminder the day before with your reference copy attached for anyone who missed b5
- [ ] Rehearse the kill: run act 2, Ctrl+C, rerun, follow-up question - THREE times, timed. The resurrection must look casual, not lucky
- [ ] Delete stale datadesk.db before the session (a leftover db from rehearsal makes the "fresh start" thread mysteriously knowledgeable - this WILL happen if you skip this line)
- [ ] Projector zoom tested; the checkpoint-timeline SVG is the anchor visual
- [ ] Have `graph.get_state(cfg)` pretty-print rehearsed - the raw snapshot is ugly; know which fields you will point at (values, next, config)

## Run of show

| Min | Beat | Notes |
|-----|------|-------|
| 0-3 | Welcome + the promise | "By minute 30 you will kill a process and the conversation will survive it." Say it exactly - it structures the whole hour |
| 3-9 | Part 1: checkpointers + thread_id | Timeline SVG on zoom; the ladder table gets 90 seconds - it is a deployment decision, not a code decision |
| 9-14 | Part 1: durable execution | The overnight-backfill story lands well with data crowds; the honest-cost bullet (state carries references not payloads) is the take-home |
| 14-18 | Part 2: two memories + Store API | Two-box SVG; the one-question test: "should a brand-new thread already know it?" If yes, Store |
| 18-30 | Demo 1: DataDesk remembers | Acts 1-2-3: pronoun resolves → fresh thread fails → SqliteSaver swap. Then THE KILL at ~min 26: Ctrl+C with theater, rerun, ask the follow-up. Hold the silence after it answers |
| 30-40 | Demo 2: DataDesk learns your taste | store.put a preference, NEW thread uses it, store.search to audit. "Memory you can audit is memory you can govern" - say it while search output is on screen |
| 40-42 | get_state_history peek | Print the photo stack; one sentence: "each of these is a valid restart point - that sentence is next week's entire session" |
| 42-45 | Q&A + homework pointer | The remember-tool homework + the thread_id-mapping sketch; b7 needs both |

## Never-cut beats

1. The resurrection moment - process dies, conversation survives. The emotional core of the session; if time collapses cut everything else first (yes, including Demo 2)
2. Why the kill test needs SqliteSaver, not InMemorySaver - the one-line ladder swap IS the persistence lesson; skipping it leaves people thinking InMemorySaver is broken
3. The two-memories test question ("should a new thread already know it?") - one sentence, prevents the most common memory design bug
4. store.search on screen - auditability is what separates memory from liability, and the governance-minded in the room need to see it exists

## Cuts if long

- Demo 2 step 5 (the search peek) can shrink to 15 seconds - but not to zero (see never-cut 4)
- Part 1 self-study card (what exactly gets saved) - never present it
- The analyst-bot example in Demo 2 - one line version: "the best long-term memory is the three facts users are tired of repeating"
- Act 1's fresh-thread contrast (Demo 1 step 2) - cut only if the room already visibly gets thread isolation

## Q&A landmines

- "Isn't this just chat history in a database? I could build that." - The checkpointer saves the FULL graph state every super-step mid-run, not transcripts after the fact - that is why a crash at step 3 of 5 resumes at step 3. Chat-history tables cannot pause, resume, or rewind; this can, and b7 is built on exactly that difference.
- "What about PII sitting in checkpoints forever?" - Real concern, right instinct. Answers: state carries references not payloads, per-thread deletion maps cleanly to user-deletion requests, Postgres checkpointers live in YOUR database under YOUR retention policy, and b4's PII middleware scrubs before state ever forms. Governance crowd: say "the checkpoint DB is a system of record - treat it like one."
- "Does the checkpoint slow everything down?" - A state write per super-step; with sane state sizes it is dwarfed by model latency. If someone pushes: measure, then trim state - do not drop persistence.
- "Can two users share one thread_id?" - Technically yes, and they will trample each other's conversation. thread_id maps to one conversational identity - user session, ticket, run. The homework sketch exists for this.
- "Ollama vs Claude - does memory differ?" - Persistence is engine-agnostic; only answer quality differs. Nice 10-second live proof if someone asks: swap the engine and continue the same thread.
