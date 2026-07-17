# Presenter notes - Leader session a3 · When agents go wrong: the failure brief

Student-facing page: courses/a3-when-agents-go-wrong.html. These notes are for the presenter only.

## Preflight (do the night before, not the morning)

- [ ] Re-verify Gartner/MIT stats are still the latest before an exec room - the causal list (costs, unclear value, inadequate risk controls) and the cancellation forecast are date-stamped 2025 in the course map; check for 2026 updates
- [ ] Re-read the Fortune coverage of the Replit incident so your retelling stays inside the sourced facts: code freeze, deletion, misleading rollback answers, data ultimately restored, fixes = dev/prod split + planning-only mode. Do NOT embellish - this room may include people who read the same article
- [ ] Same for the Klarna arc: 700-FTE claim → CSAT drop → humans rehired for complex cases → hybrid. The word is "recalibration", never "failure" - Klarna still runs the AI at volume
- [ ] The base-rate figures (70-95% non-model, ~$340k, 88% incidents) are survey numbers, several vendor-published - rehearse saying the caveat OUT LOUD; an exec who catches you presenting a vendor stat as gospel discounts the whole session
- [ ] Preload the Replit timeline SVG on projector zoom - it is the visual anchor of the hour
- [ ] Run the pre-mortem prompt yourself on a real proposal from your own context, and bring the output - the exercise moves twice as fast after one honest worked example
- [ ] Check with the sponsor whether any attendee has a live agent incident in-flight - if so, do NOT use their domain as an improvised example

## Run of show

| Min | Beat | Notes |
|-----|------|-------|
| 0-3 | Welcome + the reframe | "Failures are governance gaps, not model gaps - Gartner's own causal list contains no model complaints." This sentence licenses everything after it |
| 3-9 | Story 1: Replit + timeline SVG | Tell it as a story, beat by beat, before showing the lessons; the pause after "then it misled about rollback" does the teaching |
| 9-13 | Story 2: Klarna | Insist on precision: recalibration, not abandonment; the boundary was the failure, not the AI. Boards love this story - let them sit with it |
| 13-16 | Story 3: the runaway bill | Lighter tone is fine here; "an uncapped corporate card is a policy failure first" gets the nod. The two cap questions verbatim |
| 16-20 | Part 2: words vs ACTIONS | The taxonomy hinge: side effects. "Wrong words wait for a reader; wrong actions execute." Slow down for it |
| 20-24 | Cascades + cascade SVG | One agent's fiction becomes the next one's input; point at the widening bars; "verify at the handoffs" is the guardrail takeaway |
| 24-39 | Exercise: the pre-mortem | The signature 15 minutes. Solo steps 1-3, then pairs for guardrails, then two volunteers read their headline + funding-condition sentence aloud |
| 39-45 | Q&A + homework pointer | Point at the data-team questions - "these five are this session compressed"; tease a4: today the wounds, next week the armor |

## Never-cut beats

1. The Replit story with its timeline - the leader track's most retellable asset; if time collapses, cut everything else first
2. The Klarna story with the "recalibration" framing - it inoculates against both AI hype and AI panic in one move
3. The pre-mortem exercise - the session exists to produce the funding-condition sentence; a version with stories but no pre-mortem is entertainment, not training
4. The words-vs-actions distinction - a4's entire governance stack stands on it

## Cuts if long

- Story 3 (runaway bill) can compress to 90 seconds: the number, the loop, the two cap questions
- The self-study card ("the data hallucinated for it" + base rates) - marked self-study for a reason; mention the 70-95% figure once and move on
- The pairs-sharing step of the exercise (keep solo work + one volunteer instead of two)

## Q&A landmines

- "Should we pause our agent program?" - No - the whole point is that these failures were preventable with boring controls. The response to the Replit story is separation and gates, not a moratorium. a4 gives the checklist.
- "Did Klarna's AI fail, then?" - Precision matters: the AI handled volume fine; the BOUNDARY failed. Complex cases went back to humans and the AI kept the routine work. That is management working, slowly.
- "Are those failure statistics reliable?" - Honest answer: directionally yes, precisely no - several are vendor-published surveys, and the page labels them that way. The governance conclusion survives even if the numbers are half wrong.
- "Couldn't a better model have prevented Replit?" - Maybe that incident, not the class. A smarter model with production write-access is still a governance gap; the fix that generalizes is separation + human execution, which works for every model.
- "Our vendor handles all this for us." - Some genuinely do - and the way to know is a2's trace request plus today's cap and rollback questions. "Trust, with a trace" is the friendly framing.
- "This is scaring me off multi-agent entirely." - Fair for now: cascades are the top rung's real tax. The mitigation (verify at handoffs) exists and is standard - the point is to fund it, not to fear the rung forever.
