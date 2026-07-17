# Presenter notes - Builder session 4 · Middleware: the production layer

Student-facing page: courses/b4-middleware.html. These notes are for the presenter only.

## Preflight (do the night before, not the morning)

- [ ] venv active, pins verified; confirm the CURRENT langchain version installed (`pip show langchain`) and skim the changelog since 1.3.14 at docs.langchain.com - middleware signatures are exactly the surface that regressed before, and this session quotes them live
- [ ] Check PyPI release history and confirm 1.3.5 / 1.2.5 still show the yanked flag - you will show or describe this page in Part 2
- [ ] ANTHROPIC_API_KEY set + warm-up invoke run; ALSO rehearse the unset drill: `unset ANTHROPIC_API_KEY` in a scratch shell and confirm the fallback actually catches and answers via llama3.1 on your machine
- [ ] Ollama warm: `ollama run llama3.1` executed once tonight - the fallback demo dies theatrically if the local model cold-loads for 30 seconds
- [ ] Seeded demo CSV `data/orders.csv` in place; DataDesk v1 from b3 runs clean (it is the file both demos edit)
- [ ] Seeded PII input ready to paste: "Request from jane.doe@example.com: how many rows in the orders data?" - fake address, never a real one
- [ ] Pre-run the summarization beat once: know roughly how many turns your setup needs before the summary kicks in at max_tokens_before_summary=4000, so you can pace the loop
- [ ] Two shells open and labeled: KEY (normal) and NO-KEY (outage drill) - fumbling env vars live undermines the exact reliability story you are telling
- [ ] Projector zoom tested; the onion SVG is the session's one diagram - it must be readable from the back row

## Run of show

| Min | Beat | Notes |
|-----|------|-------|
| 0-3 | Recap + tonight's claim | "v1 is a good demo and an audit failure: it ships stakeholder emails to a cloud API. Tonight we fix that in one list." |
| 3-9 | Part 1: why middleware | Onion SVG on projector zoom; the 0.x horror (duplication, tangling, gaps) in 90 seconds; order matters - PII outermost |
| 9-14 | Part 1: the built-in five | Table pass, one line each; flag HITL as "b7 deep dive" so nobody derails into approval flows tonight |
| 14-18 | Part 2: the yank story | Tell it as a story, not a slide: shipped, broke SummarizationMiddleware users, recalled. Land "pin, and upgrade on purpose" |
| 18-30 | Demo 1: armor | Add the two rings; paste the seeded fake email; the PII scrub reveal (printing the redacted message the model actually received) is the loudest moment of the night - pause on it |
| 30-40 | Demo 2: graceful degrade | Baseline in KEY shell, then switch to NO-KEY shell, same command; narrate the silence while the fallback catches; compare answer quality honestly |
| 40-42 | The reframe | "The fallback IS the privacy mode" - one architecture, two policies; restore the key on screen so nobody's b5 starts broken |
| 42-45 | Q&A + homework pointer | Name the smoke-test-file homework - it is the bridge to b10's eval suite |

## Never-cut beats

1. The PII scrub reveal - printing the message stack and finding the redacted address. It is the difference between claiming compliance and demonstrating it; if time collapses, cut everything else in Demo 1 first
2. The fallback demo in the NO-KEY shell - the outage that degrades instead of crashes is the session's thesis made visible
3. The engine-swap dividend framing - fallback and privacy mode are the same line; this is why the course made them carry two engines since b1
4. The yank story with the pin advice (langchain>=1.3,<2) - thirty seconds that will save someone's production Friday

## Cuts if long

- The custom-hooks self-study card (before_model / after_model / wrap) - point at it; nobody should write custom middleware before needing to
- The changelog-ritual self-study card - compress to one sentence: "changelog, yank check, smoke tests, then bump"
- Demo 1 step 4 (summarization long-thread loop) - describe it and assign the run as homework; the PII reveal must not lose time to it
- The rate-limiting aside - one clause, move on

## Q&A landmines

- "Does PIIMiddleware guarantee no PII ever leaks?" - No tool guarantees that. It scrubs the patterns you configure, at the boundary you placed it. It turns "we hope nobody pasted an email" into "emails are redacted by declared policy, here is the line and its tests" - a compliance posture, not a force field. Weird formats and novel identifiers still need review.
- "Why not fall back Claude-to-Claude (another hosted model) instead of local?" - You can - the middleware takes any model string. We chose local because it doubles as the privacy path and survives a full provider outage, not just a model incident. Choose fallbacks by failure mode.
- "Summarization changed my agent's memory of early turns" - Yes, that is the trade: summaries compress, and details blur. Tune max_tokens_before_summary, and treat "what must never blur" as a b6 persistent-state question, not a summarization setting.
- "If 1.x can ship a regression, why trust the stability promise?" - The promise is about intent, the yank is about process: it broke, it was recalled publicly, ranges skip it. Pins plus your own smoke tests are how professionals consume ANY dependency, not a LangChain-specific tax.
- "Is unsetting the API key a realistic outage simulation?" - It simulates auth/provider failure at the call site, which is what the middleware sees. Real outages also include timeouts and 529s - the same ring catches those; retry-with-backoff for flaky-but-up providers is the tool-retry sibling.
