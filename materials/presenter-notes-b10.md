# Presenter notes - Builder session 10 · LangSmith: trace, eval, ship

Student-facing page: courses/b10-langsmith.html. These notes are for the presenter only.

## Preflight (do the night before, not the morning)

- [ ] LangSmith account created at smith.langchain.com AND API key generated beforehand - never do signup flows on stage or venue wifi
- [ ] Both env vars exported on the presenter machine and one traced run confirmed visible in the project view
- [ ] Seed dataset JSON ready: the 15 golden questions with expected answers pre-written (8 factual, 4 "not in the docs" probes, 3 prose) - students curate their own, you demo from yours
- [ ] `pip install langsmith openevals` tested in the course venv
- [ ] evals.py run once end to end at home; know your baseline scores so you can narrate them ("we got 12/15 on exact match - let us find the 3")
- [ ] Re-verify free-tier numbers on the pricing page the morning of ($0 / 5k traces/mo / 14-day retention as of 2026-07) - pricing pages move, this course promises current truth
- [ ] The b9 cascade run re-traced so Demo 1 step 5 has a checker span to point at; know where it is in the tree
- [ ] Ask attendees BEFORE the session to create their free LangSmith account + API key - put it in the reminder email; a room doing signups burns 10 minutes
- [ ] Projector zoom tested; the eval-loop SVG and shipping-lanes SVG both get zoomed

## Run of show

| Min | Beat | Notes |
|-----|------|-------|
| 0-3 | Where DataDesk stands | "It is a team with gates and citations - and zero proof. Tonight: x-ray vision, then numbers, then shipping" |
| 3-8 | Part 1: tracing + free tier | The two env vars ARE the slide. Say the privacy note plainly - traces go to LangSmith's cloud; the local-data path decides deliberately |
| 8-14 | Part 2: from vibes to numbers | Eval-loop SVG on zoom. Datasets as unit tests for behavior; judge choice + spot-check-the-judge; the regression-gate habit is the take-home |
| 14-18 | Part 3: shipping lanes | Lanes SVG. Both names out loud: "LangGraph Platform" = old name, "LangSmith Deployment" = current - search results still use the old one. Enterprise = hybrid/self-hosted |
| 18-28 | Demo 1: turn the lights on | Env vars, three queries, open the tree. Find the slowest step and the b9 token cost - say the dollar number out loud. Find the checker span catching the bad number |
| 28-40 | Demo 2: DataDesk graduates | Dataset in, both evaluators, evaluate(), read the experiment. Then the b1 sentence rewrite - give the room 60 quiet seconds to actually write it |
| 40-43 | Graduation checklist | Out loud, call-and-response: persistence ✓ gates ✓ RAG ✓ team+checker ✓ evals ✓. Land the arc: b1's question finally has a unit |
| 43-45 | Q&A + next steps | Homework: run the suite on BOTH engines and compare honestly; Academy observability/monitoring courses as the road ahead |

## Never-cut beats

1. The b1 sentence revisited with numbers - the entire track was built to close this loop; if time collapses, cut Part 3 to two sentences, never this
2. The first trace opening on screen - nine sessions of blindness ending in one page load is the session's emotional core
3. The regression-gate habit ("no merge without an eval run") - the one behavior change that outlives the course
4. The privacy note on tracing - cloud traces + the local-data path must be said plainly once, this course does not hide trade-offs

## Cuts if long

- Part 1 self-study card (@traceable + business model) - written for home reading
- The free-tier table - one sentence ("$0, 5k traces a month, 14 days - plenty for a pilot") and move on
- Part 3 self-study (what production needs beyond deploy) - point at it as the road ahead
- Demo 1 step 5 (finding the checker span) if the b9 re-run misbehaves - the token-cost find already lands the point

## Q&A landmines

- "Do our prompts and data really go to LangSmith's cloud?" - Yes, that is what tracing is. Options: synthetic data for traced projects, self-hosted LangSmith at Enterprise, or tracing off for sensitive workloads. Deliberate choice, not default.
- "Is the free tier a trap?" - The numbers are real: $0, 5k traces, 14 days. The gravity is also real - the business model is frameworks free, trust layer paid, and the page says so in those words. Walk in with open eyes.
- "Can we self-host instead of using their cloud?" - The OSS lane always exists for RUNNING agents (your infra, free). LangSmith itself (tracing/evals) and hybrid or fully self-hosted deployment live at the Enterprise tier. Know which of the two things is being asked about.
- "Why trust an LLM to judge an LLM?" - You do not, blindly: strong judge model always, spot-check 5 verdicts before trusting 500, exact match for anything factual. The judge scales your review, it does not replace it.
- "15 questions seems tiny." - It is - and it beats zero, which is what most teams run. The dataset grows forever: every production miss becomes a row. Small suite on every change beats grand suite never.
- "My tutorial says LangGraph Platform / LangGraph Studio - is that different?" - Same products, pre-rename (late 2025): now LangSmith Deployment and LangSmith Studio. Read old posts with the substitution running.
- "Ollama runs show no cost in traces." - Correct: ChatOllama reports no token-usage metadata, so cost columns stay empty on the local path. Latency and structure still trace in full.
