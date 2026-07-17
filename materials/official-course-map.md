# Official Course Map - learn-langchain-with-phoebe

Research date: 2026-07-17. LangChain ships weekly - re-verify docs.langchain.com changelog + PyPI versions before each delivery.

## Scope decisions (grilled + locked)

- Topic: LangChain 1.x + LangGraph 1.x (Python); LangSmith gets one builder session; Deep Agents overview only
- Two-track (Phoebe's standing directive): Leader track a1-a6 (thinking mode) + Builder track b1-b10 (practitioners)
- Audience: dual - org data team AND public/KOL followers
- LLM paths taught: BOTH - Claude API (langchain-anthropic) primary + local Ollama (langchain-ollama) free fallback; `init_chat_model` provider swap is itself a teaching point
- Repo: public + GitHub Pages from day one
- Design: LangChain brand-mimic (forest green x periwinkle, lilac paper, Manrope-adjacent type)

## Source universe (fetched, not guessed)

| # | Source | URL | Status |
|---|--------|-----|--------|
| S1 | docs.langchain.com (LangChain OSS 1.x structure, migrate guide, middleware, releases) | docs.langchain.com | fetched |
| S2 | LangGraph docs (graph-api, persistence, HITL, streaming, subgraphs) | docs.langchain.com/oss/python/langgraph | fetched |
| S3 | LangChain Academy - 12 courses, curricula public (lessons login-walled) | academy.langchain.com | fetched, syllabi captured |
| S4 | Integration docs: langchain-anthropic + langchain-ollama | docs.langchain.com/oss/python/integrations | fetched, code patterns verified |
| S5 | LangSmith docs (observability + evaluation quickstarts) + pricing | docs.langchain.com/langsmith | fetched |
| S6 | 1.0 announcement + changelog + PyPI versions | langchain.com/blog, pypi.org | fetched |
| S7 | Anthropic "Building effective agents" (leader track) | anthropic.com/engineering | fetched |
| S8 | McKinsey agentic lessons, Gartner cancellation forecast, MIT GenAI Divide (leader track) | various | fetched |
| S9 | Case studies: Klarna, Uber, LinkedIn, Replit incident, Willison lethal trifecta | various | fetched |
| S10 | Community curriculum (DeepLearning.AI, YouTube/Udemy corpus) + criticisms discourse | various | surveyed |

## Verified facts (teaching backbone)

### Versions + ecosystem state (2026-07-17)

- langchain 1.3.14 · langgraph 1.2.9 · langchain-core 1.4.9 · langchain-classic 1.0.8 · Python >=3.10
- Pin advice for materials: `langchain>=1.3,<2` and `langgraph>=1.2,<2`; 1.3.5/1.2.5 were YANKED (SummarizationMiddleware regression) - teachable "pin your versions" moment
- 1.0 GA Oct 20, 2025 for both; explicit no-breaking-changes-until-2.0 promise
- NAMING: "LangGraph Platform" renamed "LangSmith Deployment"; "LangGraph Studio" now "LangSmith Studio" (Oct 2025) - teach current names
- Stack roles: langchain (`create_agent`, high-level) is BUILT ON langgraph (low-level runtime) → checkpointing/streaming/HITL come free, eject downward without rewrite; Deep Agents = batteries-included harness on top; LangSmith = commercial trace/eval/deploy layer
- 1.0 changes: `create_agent` replaces create_react_agent/AgentExecutor (`system_prompt` param); middleware system (Summarization / HumanInTheLoop / PII / retry / fallback + before_model/after_model/wrap hooks); `message.content_blocks` provider-agnostic; LCEL chains + retrievers + hub → `pip install langchain-classic` (no published sunset date - flag)

### Code patterns (verified from docs)

- `from langchain.chat_models import init_chat_model; model = init_chat_model("claude-haiku-4-5-20251001")` - one line to swap providers
- `from langchain_anthropic import ChatAnthropic` - tools strict mode, extended thinking, prompt caching, PDFs/images
- `from langchain_ollama import ChatOllama; ChatOllama(model="llama3.1")` - bind_tools works ONLY with tool-tuned models; no token-usage metadata; free + private
- LangGraph: `StateGraph(State)` + add_node/add_edge/add_conditional_edges + START/END + `Command(update, goto)` + `Send()` map-reduce
- Persistence: `InMemorySaver` (dev) / `PostgresSaver` (prod), `config={"configurable": {"thread_id": ...}}`; long-term = `Store`/`InMemoryStore`
- LangSmith tracing = env vars only: `LANGSMITH_TRACING=true` + `LANGSMITH_API_KEY`; evals: `client.evaluate(target, data, evaluators)` + openevals LLM-as-judge
- LangSmith free tier: $0, 5k traces/mo, 14-day retention - enough for the course

### Leader-track evidence pack

- Anthropic definitions: workflows = predefined code paths, agents = model directs own process; "add complexity only when it demonstrably improves outcomes"
- McKinsey 6 lessons (50+ builds): workflow not agent · agents aren't always the answer · stop AI slop w/ evals · verify every step · reuse case · humans remain essential
- Autonomy ladder synthesis: rules/RPA → single LLM call → workflow → agent → multi-agent (flexibility up, auditability down)
- Named failures: Replit prod-DB deletion (July 2025, Fortune); Klarna reversal arc (AI=700 FTEs → CSAT drop → hybrid rebalance); runaway ~$5k/day cost cases; ~$340k avg failed project
- Lethal trifecta (Willison): private data + untrusted content + external comms = exploitable; Meta "Rule of Two"
- Build-vs-buy: buy $50-500k/yr vs build $15-50k MVP + $3.2-13k/mo run; TCO crossover ~1M conversations/yr; MIT: buy/partner succeeds ~2x internal builds
- ROI both sides: Klarna -80% resolution/$40M claim, Uber ~21k dev-hours, LinkedIn SQL Bot VS Gartner 40%+ agentic projects canceled by 2027, MIT 95% pilots no P&L impact, 78% pilot / 14% scaled
- Adoption cred: $1.25B valuation (Oct 2025), ~300M monthly downloads ecosystem, 400+ named LangGraph production deployments, 35% of Fortune 500
- Vocabulary bridge: 22 terms with one-liners (in leader research report) - session a2 backbone
- EU AI Act enforcement Aug 2026: logging, human oversight, penalties to EUR 35M / 7%

### Honest-positioning pack (b1 + a5 backbone)

- Criticisms: abstraction overhead, 0.x churn history, debugging pain, bloat-for-simple-RAG, 2026 raw-SDK migration discourse
- Fair responses: 1.0 surface-area cut + stability promise; content blocks solve real provider divergence; LangSmith answers debugging (but is the paid product - say so)
- Alternatives slide: raw SDK (single provider, zero magic) / PydanticAI (type-safety, FastAPI teams) / CrewAI (fast role-based prototyping) / LlamaIndex (retrieval-first; hybrid ingestion+LangGraph is 2026 best practice) / LangGraph wins on cycles+state+HITL+durability

## Track arcs

### Leader track (a1-a6, 6 x 45 min, thinking mode)

| # | Title | Difficulty | Core evidence |
|---|---|---|---|
| a1 | Chatbot, robot, or colleague? The autonomy ladder | green | Anthropic definitions, McKinsey L1-2, RPA hybrid, agent-washing |
| a2 | Speaking agent - the vocabulary bridge | green | 22-term glossary as "questions each term lets you ask" |
| a3 | When agents go wrong - failure modes brief | yellow | Replit, cascades, runaway costs, "governance gaps not model gaps" |
| a4 | The lethal trifecta + the governance stack | yellow | Willison/Rule of Two, HITL gates, spend caps, audit trails, EU AI Act |
| a5 | Build, buy, or blend - the investment decision | orange | Cost tables, TCO crossover, MIT buy-vs-build, free-framework/paid-trust vendor model |
| a6 | Proving it - ROI and the honest scorecard | orange | Klarna full arc centerpiece, benchmarks vs Gartner/MIT skepticism, 5-metric scorecard |

Each ends with "questions to ask your data team" checklist + homework + quiz + cheat sheet.

### Builder track (b1-b10, 45 min each, running project: "DataDesk" - a data-team assistant grown across all 10)

| # | Title | Difficulty | Sources | Coverage |
|---|---|---|---|---|
| b1 | Do you even need a framework? | green | S7 ✓, S10 ✓, S6 ◐ | scratch agent in raw SDK → same in create_agent; alternatives slide; ecosystem map; stability story |
| b2 | Models, messages, tools | green | S1 ✓, S4 ✓ | init_chat_model, Claude ↔ Ollama swap, content blocks, bind_tools, structured output |
| b3 | create_agent properly | yellow | S1 ✓, S3-A ✓ | agent loop, system_prompt, streaming; DataDesk v1 |
| b4 | Middleware - the production layer | yellow | S1 ✓ | built-ins (Summarization/HITL/PII/retry/fallback) + custom hooks; yanked-release pin lesson |
| b5 | LangGraph mental model | orange | S2 ✓, S3-C M1 ✓ | StateGraph/nodes/edges/conditional, chain → router → agent; when to eject from create_agent |
| b6 | State, memory, persistence | orange | S2 ✓, S3-C M2/M5 ✓ | checkpointers, thread_id, Store, short vs long-term |
| b7 | Human-in-the-loop + time travel | orange | S2 ✓, S3-C M3 ✓ | interrupts, breakpoints, state editing, approval gates for DataDesk |
| b8 | RAG the 1.x way | yellow | S1 ◐, S10 ✓ | loaders/splitters/embeddings/vector store, agentic retrieval, langchain-classic caveat, LlamaIndex honesty |
| b9 | Multi-agent + subgraphs | red | S2 ✓, S3-C M4 ✓, S3-D ◐ | supervisor, Send/map-reduce, subgraphs; Deep Agents overview |
| b10 | LangSmith - trace, eval, ship | red | S5 ✓, S3-E/F ◐ | env-var tracing, datasets, evaluate(), LLM-as-judge, free tier; OSS vs LangSmith Deployment |

## Not covered by design (honest list)

- LangChain JS/TS (Python only)
- LangSmith Fleet (no-code builder), Monitoring Production Agents course depth, multi-tenant auth deployment
- Deep Agents full course (overview card in b9 only)
- LCEL / classic chains (taught as history in b1; langchain-classic exists for legacy code)
- Advanced RAG variants (Corrective/Self/Adaptive RAG - namechecked in b8)
- Official Academy certificates stay with LangChain Academy (free, login required) - say so on pages

## Pre-delivery re-verify list

- PyPI versions + changelog (weekly churn; yanked releases happened twice)
- Claude model IDs in examples vs Anthropic current list
- LangSmith pricing/free-tier numbers
- Academy catalog (new courses appear; classic LangGraph course may get 1.0 refresh)
- Leader stats: Gartner/MIT numbers date-stamped 2025 - check for 2026 updates before exec delivery
