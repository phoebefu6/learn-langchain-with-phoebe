# Presenter notes - Builder session 8 · RAG the 1.x way

Student-facing page: courses/b8-rag.html. These notes are for the presenter only.

## Preflight (do the night before, not the morning)

- [ ] `pip install langchain-chroma langchain-ollama langchain-text-splitters` tested in the course venv
- [ ] `ollama pull nomic-embed-text` done on home wifi and one embedding call tested
- [ ] The synthetic `wiki/` folder written: metrics.md, data_dictionary.md, oncall.md - definitions with real opinions in them ("active user = 3 events in 7 days", not vague filler)
- [ ] `metrics_v2.md` (the deliberately wrong "EVER logged in" definition) pre-written but kept OUTSIDE wiki/ until Demo 2 - do not ingest it early
- [ ] ingest.py run once end to end; confirm `./wiki_db` exists and search_docs returns sane chunks for "active user"
- [ ] Working DataDesk from b7 (graph + persistence + gates) confirmed running - this session bolts onto it
- [ ] Test the "not in the docs" refusal once: if your model improvises, tighten rule 3 wording before class, not during
- [ ] Projector zoom tested; the two-phase SVG is the one you will zoom

## Run of show

| Min | Beat | Notes |
|-----|------|-------|
| 0-3 | Where DataDesk stands | "It computes anything, but ask how WE define active user and it guesses." That gap is tonight |
| 3-11 | Part 1: retrieval as a tool | Two-phase SVG on zoom. Land the era point hard: fixed retrieve-then-answer chains = 0.x history in langchain-classic; the agent DECIDES to retrieve. The three routing examples sell it |
| 11-16 | Part 2: grounding discipline | Grounded vs ungrounded SVG. Read the three rules out loud; rule 3 ("Not in the docs") is the trust-builder |
| 16-28 | Demo 1: DataDesk reads the wiki | Everyone builds. Ingest live, add the tool, ask the active-user question, point at the citation. Then the pure-CSV question that does NOT retrieve - the routing is the lesson |
| 28-38 | Demo 2: prove the grounding | The refusal first, then poison the well with metrics_v2.md. Let the wrong citation land in silence before you name it: retrieval is grounding, not truth |
| 38-40 | Governance close | Fixes are curation, provenance, one source of truth - and "cites the RIGHT doc" goes into the b10 eval set |
| 40-45 | Q&A + homework pointer | Homework: real docs in, five real questions, chunk-size experiment |

## Never-cut beats

1. The wrong-doc citation moment in Demo 2 - the emotional core of the session; a room that sees a faithful citation of a lie never trusts RAG naively again
2. The routing contrast in Demo 1 (retrieves for wiki questions, does NOT retrieve for CSV questions) - this IS agentic retrieval
3. The era check: pipe-chain/RetrievalQA tutorials are 0.x history - half the room will hit those tutorials this week
4. Rule 3, "Not in the docs" - the single sentence that makes stakeholders trust the tool

## Cuts if long

- Part 1 self-study card (chunking judgment + LlamaIndex honesty) - it is written to be read at home
- The RAG-vs-long-context discussion - one sentence ("small stable corpus: just paste it; big changing corpus: RAG") and move on
- Demo 2 step 5 (governance fixes) can compress to the b10 pointer
- The stale-runbook real-world callout - reference it, do not retell it

## Q&A landmines

- "Why not just paste the whole wiki into the context window?" - For five stable pages, honestly, do. RAG wins when the corpus outgrows the window, changes often, needs per-question cost control, or needs citations. Choose per corpus, not per fashion.
- "Which embeddings model should we use in production?" - Course uses nomic-embed-text because it is free, local, and keeps documents private. Hosted embeddings score higher; swap one line if docs are not sensitive. Hard rule either way: query and index must share the model, or you re-ingest.
- "Is Chroma production-grade?" - It is honest for a team wiki. At real scale you move to pgvector/Pinecone/OpenSearch - same interface shape, different ops. Tonight's code ports.
- "Why not LlamaIndex? I heard it is better at RAG." - For retrieval-first products over messy documents, its ingestion IS deeper - the page says so. The 2026 hybrid (LlamaIndex ingestion + LangGraph orchestration) is a legitimate design-review answer.
- "How do we stop wrong docs getting cited?" - You cannot, at the model layer - that is the Demo 2 lesson. Fixes are governance: curate ingestion, date-stamp, one source of truth per definition, and eval "cites the right doc" in b10.
- "What chunk size is correct?" - There is no constant. 800/120 is a sane default for wiki-ish markdown; the homework makes them feel 400 vs 1500 move retrieval quality; b10 makes it measurable.
