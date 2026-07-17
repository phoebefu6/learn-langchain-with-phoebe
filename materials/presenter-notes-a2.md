# Presenter notes - Leader session a2 · Speaking agent: the vocabulary bridge

Student-facing page: courses/a2-speaking-agent.html. These notes are for the presenter only.

## Preflight (do the night before, not the morning)

- [ ] Re-verify the MCP one-liner ("USB for AI tools") still matches current MCP docs framing, and skim the LangSmith tracing page once - the trace SVG must match what a real trace actually shows
- [ ] Re-verify Gartner/MIT stats are still the latest before an exec room (they only appear in asides here, but an exec WILL ask "what's the failure rate" a session early - have a3's numbers ready and date-stamped)
- [ ] Rehearse the anatomy SVG walk-through out loud once: model → tools → state → guardrails → HITL gate, under 90 seconds
- [ ] Preload the decode-the-status-update paragraph on a slide or the projector zoom - the whole room must read it simultaneously
- [ ] Run the decoding-partner prompt yourself on the exercise paragraph so you know what a good AI translation looks like (and where it over-simplifies)
- [ ] Bring ONE real (sanitized) status update from your own org as a backup exercise text - a room that recognizes its own jargon works twice as hard
- [ ] Check who in the room has a live AI project - Exercise 2 needs each person to have one; have a generic "customer-service assistant" fallback for those who don't

## Run of show

| Min | Beat | Notes |
|-----|------|-------|
| 0-3 | Welcome + the premise | "The meeting where you nod along ends this week." Then the reframe: every term = a question you become able to ask - say it twice, it is the session |
| 3-8 | Part 1: anatomy SVG + identity words | Walk the picture first, words second; LLM/agent/workflow ties straight back to a1 - reward anyone who says "who chooses the steps" |
| 8-12 | Orchestration, tool calling, state | Land the state question hard: "what happens if it fails halfway?" - tell the ops-director story; pause after it |
| 12-16 | Part 2: the governance four | Frame as finance instincts they already have: approval limits, controls, audit trails, monitoring. HITL, evals, traces, observability in that order |
| 16-20 | The plumbing four + trace SVG | Trace SVG on projector zoom; "show me what it did last Tuesday" is the line they will remember - deliver it slowly |
| 20-32 | Exercise 1: decode the status update | Read the paragraph aloud badly-fast once (that is the nod experience), then decode line by line together; steps 4-5 individually |
| 32-40 | Exercise 2: your first three questions | Silent solo work, then pairs swap questions; collect two good ones for the room |
| 40-45 | Q&A + homework pointer | Point at the 22-term table: "menu, not checklist"; homework = decode one REAL update from your own inbox |

## Never-cut beats

1. Exercise 1 (decode the status update) - the session's promise is kept or broken here; cut concepts before touching it
2. Exercise 2 (your first three questions) - it converts vocabulary into a calendar entry; without it the session is a glossary
3. The state question ("what happens if it fails halfway?") with the story - the ten-second demonstration that questions beat definitions
4. The trace request ("show me exactly what it did last Tuesday") - it is the single most reusable sentence in the leader track

## Cuts if long

- The plumbing four card can compress to one line each (the table has the rest)
- The full 22-term table walkthrough - never present it; it is self-study by design, just hold it up and say "beside your calendar"
- The try-it-now prompt in Part 1 (it reappears in homework anyway)

## Q&A landmines

- "Do I really need to know all 22?" - No: six machine words + the governance four gets you through 90% of meetings. The table is a lookup, not a syllabus - that is why only ten terms get presented live.
- "Isn't asking for traces micromanaging my engineers?" - Reframe: it is the same as asking finance for an audit trail. Good teams are PROUD of their traces; discomfort with the request is itself information.
- "What's the difference between evals and testing?" - Evals are ongoing scoring of output QUALITY (which drifts), not one-time functional tests. "How do we know it's still good next month" is the distinguishing clause.
- "Our vendor says they support MCP - so we're fine?" - MCP standardizes the plug, not the judgment. Still ask what the tools are allowed to do and what guardrails wrap them - a4 covers exactly this.
- "What is the lethal trifecta? You skipped it." - Deliberately: it is the centerpiece of a4. One sentence (private data + untrusted content + external comms in one agent = exploitable) and promise the full hour.
