# Presenter notes - Builder session 3 · create_agent, properly

Student-facing page: courses/b3-create-agent.html. These notes are for the presenter only.

## Preflight (do the night before, not the morning)

- [ ] venv active, pins verified: `pip install "langchain>=1.3,<2" "langgraph>=1.2,<2" langchain-anthropic langchain-ollama` still resolves clean
- [ ] ANTHROPIC_API_KEY set + one warm-up invoke run in the demo shell
- [ ] Ollama warm: `ollama run llama3.1` executed once tonight so Demo 2's swap streams immediately instead of cold-loading
- [ ] Seeded demo CSVs: `data/orders.csv` (date + order_value columns) AND `data/signups.csv` (any second CSV) - list_datasets returns both paths and they must both exist
- [ ] datadesk_v1.py pre-typed in a hidden tab; live-type only the SYSTEM constitution and the two new tools
- [ ] Rehearse the two-tool question once: confirm the model actually chains list_datasets/csv_stats + column_mean on YOUR data - if it one-shots it, sharpen the question until it chains
- [ ] Rehearse the refusal test ("churn by region") - know what your model does before the room does
- [ ] Projector zoom tested; the harness SVG is the session's centerpiece slide

## Run of show

| Min | Beat | Notes |
|-----|------|-------|
| 0-3 | Recap + tonight's claim | "You have called create_agent twice on trust. Tonight we open it and find your b1 while-loop inside." |
| 3-9 | Part 1: the harness | Harness SVG on projector zoom; map each piece to their b1 loop line by line - this is the payoff of making them write it by hand |
| 9-14 | Part 1: the constitution | Role + tool guidance + refusal rules; tell the invented-column story - it lands hardest with DAs |
| 14-18 | Part 2: streaming modes | messages = watching the answer, updates = watching the agent; one table, keep it tight, the demo proves it |
| 18-32 | Demo 1: DataDesk v1 | Two new tools + constitution; the two-tool chain question is the wow beat - narrate "nobody sequenced this" while updates would show the steps; run the refusal test live |
| 32-42 | Demo 2: make it feel alive | Typing effect first (silence in the room helps - let it type), then updates mode, then the engine swap on Ollama |
| 42-45 | Q&A + homework pointer | Name the fourth-tool homework and the invoke-vs-stream timing exercise |

## Never-cut beats

1. The line-by-line mapping of the b1 scratch loop onto the harness SVG - it converts create_agent from magic to engineering, which is the session's entire job
2. The refusal test ("churn by region" → "not in the data") - the constitution beat that makes stakeholder-facing deployment thinkable
3. The two-tool chain with the narration "you never wrote this sequence - the model planned it"
4. The Demo 2 engine swap with streaming untouched - the course spine, every session, no exceptions

## Cuts if long

- The eject-to-LangGraph self-study card - one pointing gesture ("b5 is where the rails become yours") suffices
- The multi-tool routing self-study card - Demo 1's docstring troubleshooting tip covers the live need
- Demo 2 step 3 (narrating UI modes) - fold it into one sentence while the updates print
- The system-prompt attack Try-it-now - it is homework anyway

## Q&A landmines

- "If create_agent is just a loop, why not keep my own loop?" - Because the loop was never the expensive part. The rails are: checkpointing, streaming, interrupts, time travel arrive in b6-b7 with zero rewrite. Hand-rolled loops rebuild those badly - that was b1's closing story.
- "Can I force the tool order / make it always call list_datasets first?" - You can steer with the system prompt (we did) and route hard with graph edges in b5. If the order is truly fixed, you may want a workflow, not an agent - the b1 ladder applies.
- "The model picked the wrong tool" - First stop is always the docstrings: overlap or vagueness, not model quality. Sharpen the boundary, re-run, THEN consider a bigger model.
- "Does streaming cost more tokens?" - No, same tokens, delivered earlier. The cost is code complexity in your UI layer, which is why we showed both modes in six lines.
- "Why does Ollama streaming feel slower?" - It IS slower: local tokens arrive at your hardware's pace. That is the honest trade of the free private path - and exactly the degrade b4 makes graceful.
