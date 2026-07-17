# Presenter notes - Leader session 4 · The lethal trifecta and the governance stack

Student-facing page: courses/a4-trifecta-governance.html. These notes are for the presenter only.

## Preflight (do the night before, not the morning)

- [ ] Projector zoom tested (toolbar button) - the trifecta circles and the 2x2 matrix are the two SVGs the whole session hangs on
- [ ] Rehearse the Willison sentence out loud until it lands in one breath: "private data + untrusted content + external comms = exploitable by design"
- [ ] Have the "helpful inbox agent" example ready to retell WITHOUT the page - it is your whiteboard moment
- [ ] Pre-pick a plausible agent use case for the exercise walkthrough in case the room freezes (email triage or invoice handling both work)
- [ ] Check whether this audience touches the EU market - if yes, the AI Act self-study card gets promoted to a live 2-minute beat
- [ ] Print or preload a blank approval-matrix worksheet (use case / 8-10 actions / three columns / spend cap / audit question)
- [ ] Know who in the room owns security or compliance - they will either be your ally or your toughest Q&A, find out which before minute 0

## Run of show

| Min | Beat | Notes |
|-----|------|-------|
| 0-3 | Welcome + the reframe | Say it plainly: "agent security is a property of what you ALLOW it to touch - which makes it your decision, not the vendor's". That sentence frames the whole hour |
| 3-10 | Trifecta circles walkthrough | SVG on projector zoom. Walk the three legs one at a time, THEN reveal the overlap. Do not rush the circle walkthrough - it is the session |
| 10-14 | Willison's rule + inbox-agent story | Tell the crafted-email attack slowly; the room goes quiet when they realize no hacking was involved |
| 14-17 | Rule of Two | Land it as a design checkbox they can score in a meeting; run the three "pick two" combinations quickly |
| 17-23 | Governance: HITL gates + 2x2 matrix | Second SVG. The placement test ("mistake cost vs delay cost") is the take-home; warn about rubber-stamping over-gated humans |
| 23-28 | Spend caps + circuit breakers | The 2am Saturday question wakes up every ops-minded person in the room |
| 28-33 | Dual-identity audit trails | Sell it as continuity with SOC 2/SOX/GDPR, not novelty - that is how it gets budget |
| 33-43 | Exercise: the approval matrix | Everyone works one use case; circulate; nudge people sorting everything into "needs approval" toward the placement test |
| 43-45 | Q&A + homework pointer | Point at the 5 data-team questions - "your homework is a conversation, not a reading" |

## Never-cut beats

1. The trifecta circles walkthrough (the emotional and intellectual core - if time collapses, cut everything else first)
2. The planted-instruction attack story - leaders must FEEL that the attack is just an email, not hacking
3. The Rule of Two as a thirty-second meeting test - it is the tool they will actually use next week
4. The gate placement test (mistake cost vs delay cost) - without it, "add human oversight" degrades into rubber-stamp theater

## Cuts if long

- The prompt-injection vs jailbreak table (marked self-study - never present it, just point at it)
- The evals + EU AI Act card detail (self-study; keep only the Aug 2026 date and penalty number if EU-relevant)
- Exercise steps 4-5 (spend cap + audit question) - can move whole into homework
- The stress-test prompt walkthrough - name it, do not run it live

## Q&A landmines

- "Can't we just tell the agent to ignore malicious instructions?" - No: instructions and data arrive as the same text; a written rule is just more text and a crafted injection can outweigh it. Prompt defenses are advisory; permission design is structural. This is THE core misconception - answer it patiently every time it appears.
- "Our vendor says their model is injection-resistant." - Good, and irrelevant to the design question: resistance lowers the odds, the trifecta sets the stakes. Ask the vendor which trifecta leg their product removes or supervises; a serious vendor has an answer.
- "Doesn't gating everything make agents pointless?" - Yes, and that is a real failure mode: over-gated humans rubber-stamp. That is why placement follows the mistake-cost vs delay-cost test, not fear.
- "Is the EU AI Act really our problem?" - If you touch the EU market, enforcement is Aug 2026 with penalties to EUR 35M or 7% of global turnover, and the required controls are literally this session's checklist. If you do not, the checklist is still what your auditors will converge on.
- "Who should own this - security, data, or the business?" - The controls are implemented by the technical team, but placement decisions (what the agent may touch, where gates go) are business-owned. That split is the session's whole thesis; do not let the room delegate it away.
