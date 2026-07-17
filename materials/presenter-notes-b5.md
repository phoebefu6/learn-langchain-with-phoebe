# Presenter notes - Builder session 5 · The LangGraph mental model

Student-facing page: courses/b5-langgraph-mental-model.html. These notes are for the presenter only.

## Preflight (do the night before, not the morning)

- [ ] venv active with `langchain>=1.3,<2` and `langgraph>=1.2,<2` pinned AND imported once (first import compiles caches - never on venue time)
- [ ] Both engines tested: `ANTHROPIC_API_KEY` set + one Claude call, `ollama pull llama3.1` done + one local call
- [ ] Seeded data.csv in the project root (a few hundred rows, an `amount` column and a date column) - the same file the room used in b1-b4
- [ ] Your own datadesk_v1.py (the b3 create_agent file) importable as `from datadesk_v1 import agent` - run it once tonight
- [ ] datadesk_v2.py pre-written and RUN END TO END on both engines; keep it open in a second editor tab as the safety net if live typing goes sideways
- [ ] Mermaid renderer tab open (mermaid.live or any) for Demo 2's draw_mermaid paste
- [ ] Projector zoom tested (toolbar button); the three-shapes SVG is the anchor visual - check it reads from the back row
- [ ] Rehearse the misroute recovery: force the classifier to say "Stats." with a capital and punctuation, show pick_route absorbing it

## Run of show

| Min | Beat | Notes |
|-----|------|-------|
| 0-3 | Welcome + the hinge framing | "Tonight you stop renting create_agent's shape and start drawing your own." Everything after b5 is features of tonight's machine - say that upfront |
| 3-10 | Part 1: why graphs + three shapes | SVG on projector zoom; spend the time on the router shape - it is tonight's demo. create_agent = shape 3 prebuilt is the aha |
| 10-15 | Part 1: the four primitives | Table on screen; hammer the two bug-savers: partial updates, routing functions return STRINGS |
| 15-20 | Part 2: the five-call build sequence | Say the sentence: declare state, register nodes, wire edges, compile. Make the room repeat it - it works |
| 20-32 | Demo 1: DataDesk gets a spine | Everyone builds; type the state and classify node live, paste the rest from the page. The three-question run with visibly different routes is the payoff - read the route column out loud |
| 32-40 | Demo 2: draw what you built | draw_mermaid into the renderer on the projector; finger-trace the haiku question's path; then the engine swap - one line, rerun, same diagram |
| 40-42 | Eject checklist recap | When to come down to LangGraph vs stay at create_agent - one sentence per bullet |
| 42-45 | Q&A + homework pointer | Flag the sql_guard homework - it is their first deterministic node and b7 builds on the idea of nodes the model cannot skip |

## Never-cut beats

1. The router divergence in Demo 1 - three questions, three visibly different routes through the same graph. If time collapses, cut everything else first; this is the session
2. "create_agent IS a LangGraph graph" - the stack becomes one thing instead of two; without this beat b6-b9 feel like a new framework
3. Partial updates + routes-are-strings - the two rules that prevent every office-hours bug this week
4. The printed diagram (even 30 seconds of print_ascii) - "the diagram is the code" is the promise the whole session makes

## Cuts if long

- Demo 2 steps 2 and 4 (finger-trace + keep-the-diagram) - keep the print itself and the engine swap
- The Command/functional-API self-study card - never present it, it is marked self-study for a reason
- Part 2's naming-discipline callout - one sentence in passing is enough
- The whiteboard-that-compiled example - compress to one line if needed

## Q&A landmines

- "Why not just if/else in plain Python?" - You can, until you need to pause mid-flow, resume after a crash, or show an auditor the shape. The graph is plain functions PLUS a runtime that checkpoints between them - b6 makes this concrete, ask them to hold the question one week.
- "Is create_agent deprecated now that we know LangGraph?" - No. It is the right altitude for the tool-loop shape and it runs ON LangGraph. Eject when the shape no longer fits, not as a rite of passage.
- "My classifier routes everything to other / misroutes" - Small local models are sloppy formatters; that is why the code lowercases, strips, and defaults unknowns to other. Show the defensive pick_route line; with Ollama suggest the stricter one-word prompt or a bigger model.
- "Can a node call another graph?" - Yes - subgraphs, session b9. Park it visibly on the whiteboard.
- "What does compile() actually do?" - Validates the wiring (dangling edges, unknown node names) and returns a runnable with invoke/stream. Cheap, safe to call often; the expensive things only start at invoke.
