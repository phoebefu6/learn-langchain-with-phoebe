# Presenter notes - Builder session 2 · Models, messages, tools

Student-facing page: courses/b2-models-messages-tools.html. These notes are for the presenter only.

## Preflight (do the night before, not the morning)

- [ ] venv active with pins installed: `pip install "langchain>=1.3,<2" "langgraph>=1.2,<2" langchain-anthropic langchain-ollama pydantic` - run `pip list` and screenshot it
- [ ] ANTHROPIC_API_KEY set in the demo shell AND one warm-up `model.invoke("hi")` already run (first-call auth failures on stage are unrecoverable time)
- [ ] Ollama running and warm: `ollama run llama3.1` once so the model is loaded in memory - a cold load mid-demo is 30+ dead seconds
- [ ] Seeded demo CSV at `data/orders.csv`: a date column spanning a real range + an `order_value` numeric column, ~200 rows, synthetic - `csv_stats` and Demo 2 both hit it
- [ ] DataDesk v0.1 from b1 runs clean in this venv (it is the base both demos edit)
- [ ] `xray.py` and the v0.2 file pre-typed in a second editor tab as the escape hatch if live typing goes sideways
- [ ] Projector zoom tested (toolbar button); the two SVGs on this page read well at 125%
- [ ] Confirm llama3.1 is the pulled tag - a non-tool-tuned model silently breaks the bind_tools beat

## Run of show

| Min | Beat | Notes |
|-----|------|-------|
| 0-3 | Recap + tonight's claim | "You used create_agent twice without knowing what a message even is. Tonight we X-ray everything." |
| 3-8 | Part 1: the swap contract | Land the plug-vs-appliance line; the interface is standardized, capability is not - say it twice |
| 8-13 | Part 1: message stack + content_blocks | Message-stack SVG on projector zoom; "the list IS the conversation, models are stateless" is the take-home |
| 13-18 | Part 2: @tool + structured output | "The docstring IS prompt engineering" - show the bad docstring box; structured output happens in the MAIN loop, no second call |
| 18-30 | Demo 1: X-ray a conversation | Everyone runs xray.py; step 4 engine swap is the never-cut moment - narrate the diff slowly: same block shapes, different vocabulary |
| 30-40 | Demo 2: DataRequest form | The messy stakeholder sentence gets typed live; print structured_response, then feed req.dataset into csv_stats to close the loop |
| 40-42 | v0.2 checkpoint | One sentence: DataDesk now speaks form. Point at the cheat sheet |
| 42-45 | Q&A + homework pointer | Docstring-rewrite homework is the one to name out loud |

## Never-cut beats

1. The Demo 1 engine-swap diff (step 4) - the whole course rests on students believing the one-line swap; they must SEE identical block shapes on both engines
2. The tool_call block appearing in the X-ray - it demystifies every agent they will ever debug
3. "Structured output runs in the main loop, no second LLM call" - the 1.x fact that separates this course from stale tutorials
4. Feeding `req.dataset` straight into `csv_stats` in Demo 2 - the handoff is the whole argument for structured output

## Cuts if long

- The capability-envelope table (self-study card - point at it, never present it)
- The "when structured output beats free text" card - the one-sentence rule from the lede is enough live
- Demo 2 step 5 (Ollama re-run of structured output) - assign it as the first homework bullet instead
- The Try-it-now prompt in Part 1 - it works fine as homework

## Q&A landmines

- "So Claude and llama3.1 are interchangeable?" - No: the INTERFACE is interchangeable. Capability differs (thinking, caching, PDFs, tool quality, usage metadata). The swap changes the appliance, not the plug - that is a feature, and b4's fallback middleware is built on it.
- "Why not just use JSON mode / a regex parser?" - response_format gives Pydantic validation at the boundary, in the main loop, with no drift between the answer and its structure. Regex parsers are how teams end up debugging prompts at 2am.
- "My Ollama run shows no tool_call block" - almost always the model tag: bind_tools works only on tool-tuned models. llama3.1 works; many pulls do not. That is the capability envelope, live.
- "Is content_blocks slower or lossy?" - It is a view over the same response, not a copy of less. You lose nothing; you gain a schema that survives provider swaps.
- "Can I see token usage on Ollama?" - No, and that is a real operational gap: no usage metadata on the local path. Budget dashboards need the Claude path or request counting.
