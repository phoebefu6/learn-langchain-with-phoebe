# Presenter notes - Builder session 1 · Do you even need a framework?

Student-facing page: courses/b1-need-a-framework.html. These notes are for the presenter only.

## Preflight (do the night before, not the morning)

- [ ] Fresh venv created and tested: `pip install anthropic "langchain>=1.3,<2" langchain-anthropic langchain-ollama` all resolve cleanly (pin check - two 1.x releases have been yanked before)
- [ ] `ANTHROPIC_API_KEY` set on the presenter machine AND one warm-up call already made (first-call auth failures on stage are avoidable)
- [ ] Ollama installed, `ollama pull llama3.1` done on home wifi, one tool-calling test run completed
- [ ] `data.csv` seeded in the demo folder: synthetic, with a date column and a few thousand rows so csv_stats returns satisfying numbers
- [ ] Both demo files pre-written and run once end to end: the scratch loop (Demo 1) and the create_agent version (Demo 2) - you type live but keep the working copies one tab away
- [ ] Projector zoom tested (toolbar button); the agent-loop SVG and stack SVG are the two you will zoom
- [ ] Check docs.langchain.com changelog + PyPI versions the morning of - this course promises 2026-current truth

## Run of show

| Min | Beat | Notes |
|-----|------|-------|
| 0-3 | Welcome + the premise | "Tonight you build an agent with NO framework, then decide if the framework deserves your code." The honesty is the hook - say it first |
| 3-9 | Part 1: what an agent actually is | Agent-loop SVG on projector zoom. Land the line "it is a while-loop" before showing any code. Workflow vs agent definition is the rent-payer |
| 9-15 | Part 2: the 2026 stack map | Stack SVG. Four products, one trench coat. The langchain-classic / pipe-operator history beat matters - half the room has old tutorials open |
| 15-18 | Part 3: two engines | Setup card + the one-line swap. Poll the room: who has a key, who is on Ollama. Nobody gets left behind tonight |
| 18-32 | Demo 1: agent from scratch | Everyone builds. Type the loop live, narrate the two round trips. Step 5 ("now break it") sets up the whole course - do not rush it |
| 32-40 | Demo 2: three lines of LangChain | The deletion is the demo: watch loop code disappear. Run the engine swap live. End with the one-sentence verdict exercise |
| 40-45 | Q&A + homework pointer | Homework: second tool in both versions + both engines working before b2 |

## Never-cut beats

1. The scratch loop demo (Demo 1) - the entire track's credibility rests on "agents are never magic again"; if time collapses, cut Part 2 depth, never this
2. The one-line engine swap run live - it is the framework's whole opening argument
3. The "for DataDesk, the framework is/is not worth it because..." sentence - b10 revisits it with evals; it must exist
4. Workflow vs agent definition - every later session leans on it

## Cuts if long

- Part 1 self-study card (autonomy ladder table) - marked self-study for a reason
- Part 2 adoption-evidence card - one sentence ("$1.25B, 300M downloads a month, both skeptic currents real") and move on
- Demo 1 step 5 discussion can shrink to 30 seconds if the room is already feeling the pain
- The alternatives card can compress to "raw SDK, PydanticAI, CrewAI, LlamaIndex - the table is on the page"

## Q&A landmines

- "Why not just use the Anthropic SDK forever?" - Honest answer: for one provider and simple chains, do. The framework earns its keep at state, approval gates, provider swapping, durable runs - which is exactly what b5-b7 build. Tonight you felt the first hint, not the whole case.
- "Is LangChain still a mess? I got burned in 0.x." - Fair wound. 1.0 cut the surface area, one blessed entry point, no-breaking-changes-until-2.0 promise. We still pin versions because two 1.x releases were yanked. Trust, with a lockfile.
- "Should we use CrewAI/PydanticAI instead?" - The alternatives card is on the page and it is honest. If their pitch fits your case better, take it - this course teaches you to defend the choice, not to be loyal.
- "My Ollama model will not call tools." - Tool calling needs a tool-tuned model; llama3.1 works, tiny or older models often do not. Also first token is slow on 8GB machines - normal, not broken.
- "Can I use company data in the demos?" - Claude path: only if your org allows the API. Ollama path: yes, nothing leaves the machine. That split discipline starts tonight and never relaxes.
