# Presenter notes - Builder session 9 · Multi-agent and subgraphs

Student-facing page: courses/b9-multi-agent.html. These notes are for the presenter only.

## Preflight (do the night before, not the morning)

- [ ] supervisor.py pre-written and run end to end on BOTH engines; know that llama3.1's routing is flakier and have the tightened routing prompt ready
- [ ] march.csv seeded (synthetic, with a revenue column) AND march_bad.csv prepared: same file, one revenue figure corrupted by 100x - obvious enough that the checker can catch it
- [ ] The checker node (~20 lines) pre-written for Demo 2 step 4 - you add it live but keep the working copy one tab away
- [ ] Run the cascade once at home: confirm the writer actually polishes the wrong number (models occasionally get suspicious; know your seed request wording)
- [ ] b8 DataDesk with search_docs working - the analyst inherits those tools
- [ ] Count and note the model-call totals: single-agent b3 answer vs tonight's team answer for the same request (Demo 1 step 5 needs the real ratio)
- [ ] Projector zoom tested; the supervisor org-chart SVG is the zoom candidate
- [ ] This is the hardest session - rehearse the graph wiring narration once out loud

## Run of show

| Min | Beat | Notes |
|-----|------|-------|
| 0-3 | Where DataDesk stands | "One agent, many tools. Tonight we ask when one agent is not enough - and what splitting costs" |
| 3-10 | Part 1: the honest gate + supervisor | Gate FIRST, pattern second - never reverse. Org-chart SVG on zoom; point at the arrows: "every arrow is a handoff that can carry a confident mistake" |
| 10-16 | Part 2: Send() + Deep Agents | Fan-out SVG. Send = same job, many items, workers cannot cascade. Deep Agents = one honest overview card: planning + filesystem + subagents prebuilt, a harness ON these primitives, not magic |
| 16-30 | Demo 1: DataDesk hires an analyst | Everyone builds. Narrate the stream: supervisor → analyst → supervisor → writer → END. Step 5's model-call count is the price tag - say the number |
| 30-40 | Demo 2: the cascade experiment | The room must SEE the writer polish the wrong number before you name it. Then the checker node, then the re-run that bounces. "Verify at the handoff, not at the end" |
| 40-42 | The a3 bridge | "Your leaders learned this as a slide; you just reproduced it in 20 lines" - the two tracks meeting is a course-design payoff, spend one minute on it |
| 42-45 | Q&A + homework pointer | Homework: third specialist + Send() fan-out + argue-against-the-split on a real backlog item |

## Never-cut beats

1. The cascade experiment (Demo 2) - the entire session exists so the room watches fluent, formatted fiction flow downstream; if time collapses, cut Part 2, cut Demo 1's third run, never this
2. The honest gate before any pattern - multi-agent multiplies cost AND failure modes; teaching the pattern without the gate is malpractice
3. The checker-node fix and its re-run - the lesson is incomplete at "it breaks"; it completes at "verify at the handoff"
4. The model-call count in Demo 1 step 5 - the price tag makes the gate concrete

## Cuts if long

- Part 1 self-study card (subgraphs/swarm/hierarchical) - namechecks live happily on the page
- Deep Agents card compresses to two sentences: "prebuilt harness for long-horizon work; not for DataDesk-shaped jobs"
- Demo 1 step 5 discussion can shrink to just saying the ratio
- The McKinsey/real-world callout - reference, do not retell

## Q&A landmines

- "Should we split all our agents into teams now?" - Reverse the question: can you write each agent's job in one sentence without overlap? If not, one well-prompted agent with all the tools is cheaper, faster, and easier to debug. Most jobs fail the gate - that is the finding, not the failure.
- "The supervisor keeps looping / misroutes on my machine." - Usually the local engine: llama3.1 routes less reliably than Claude. Tighten the routing prompt to forbid anything but the three words, or mix engines - strong supervisor, free workers. One line per node.
- "Why a checker node instead of a better writer prompt?" - The writer WAS told not to invent numbers - and did not; it summarized what it was given. Prompts cannot verify, only topology can: a node that re-checks claims against the raw data.
- "Is this the same as CrewAI's crews?" - Same idea (role-based specialists), different altitude: CrewAI hands you the pattern fast, LangGraph makes you wire it but gives you checkpointing, interrupts, and custom checker nodes on every edge. b1's alternatives card still applies.
- "When would we actually use Deep Agents?" - Long-horizon, open-ended work: research-and-report, multi-hour tasks needing planning and scratch space. If you can enumerate the tools and the run takes minutes, tonight's supervisor is the right altitude.
- "Do subgraphs share memory with the parent?" - Shared state keys pass through; otherwise you translate at the boundary. That boundary is a feature: it is what makes a team testable alone.
