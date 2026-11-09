---
name: "de-slop-page"
description: "Strip the AI-generated look from a web page's styling without changing features, copy facts or structure. Use when asked to de-slop, humanize, or remove the AI look from a UI, even if not named."
---

# De-slop a page

Change the craft of a page, never what it does. Features, behavior, facts and section order stay. No new sections or components. The page URL (a local dev URL) is the input; if it is missing or still a placeholder, ask for it. If no repo folder is connected, ask the user to connect one before the build phase.

Why the gates: styling edits across a whole page are easy to start and hard to review. The audit phase is read-only so the user can steer the direction before any code moves, and the guard at the end exists because "styling only" erodes quietly.

## Phase 0: Before shots and baseline (read-only)

Use Chrome DevTools MCP if present, otherwise the preferred browser tools. Leave any login to the user; never read credentials.

- Save before-shots outside the repo, emulating 1440x900 and 390x844, in screen-height pieces.
- Record build and test results.
- Run `lighthouse_audit` (or the closest available audit) and record accessibility failures on desktop and mobile.

Nothing in the repo changes in this phase.

## Phase 1: Plan, then stop for approval

Present all three, then stop and wait for the user's OK.

1. **Slop list.** Number every sign of AI slop and where it shows: purple gradients, glows, gradient text, emoji labels, sparkle badges, wide-tracked caps, endless loops, drifting spacing. If the page is mostly fine, say so and fix only these.
2. **Direction, three lines.**
   - World: its setting or material.
   - Focus: 1-2 spots get rich color and detail; the rest stays quiet.
   - Signature: one small detail only this product would have.
   Real brand colors, logos and fonts stay (a purple gradient is not a brand color).
3. **Copy table**, current vs proposed, tone only: exclamation marks, "Welcome back" greetings, hype words. No claim, number, price, name or legal line changes.

## Phase 2: Passes (only after approval)

Work on a new branch. One commit per pass, applied across the whole page:

1. Spacing: 4px grid, same things same size.
2. Color: one neutral scale tinted toward World, three text levels, one accent saved for Focus spots, no hue gradients or glows.
3. Icons: the project's line icons replace emoji, one size and stroke.
4. Copy: approved rows only.
5. Type: weights 400 and 500, sentence case, the project's font.
6. Layout: alignment and proportions inside sections only.
7. Details: consistent radii, quiet badges, the Signature.
8. Visuals: remove decorative filler; generate nothing.
9. Motion: remove loops, transition-all, hover scale-ups.

### Rules

- Only styling and approved copy change. Anything else (logic, data, config, a new package or font) goes on an approval list, unbuilt.
- Theme files count as styling; name any other pages a change reaches.
- Keep every id, data- and aria- attribute. Never edit a test to pass it: copy-only breaks go on the approval list.
- Text stays at WCAG AA: 4.5:1, or 3:1 for large text. Every control keeps a visible focus state.
- Never push or merge.

## Phase 3: Check

After the last commit, retake the same shots, then:

- **Build and tests:** no new failures. No tests? Click only controls that cannot write, send, delete or pay, and call that weaker proof.
- **Audit:** rerun `lighthouse_audit`; no new failures. It cannot score text over images or gradients, so list those as unchecked. Tab through to see focus states. Grep for motion items stills cannot show.
- **Judge:** a fresh subagent, not a fork. It gets only the before and after shots and the slop list, edits nothing. It marks each item gone, still there or can't tell, citing the screenshot, and flags anything broken at phone width. Swap test: would this page still make sense with another company's name?
- **Guard:** a fresh subagent on the same terms. It gets only the rules above, the approved copy rows and the full branch diff, and lists every change that is not styling or approved copy.

Subagents get only what is listed so they judge the result on its own, not on the reasoning that produced it.

## Phase 4: Fix and stop

Wait for both reports, fix what they find, then retake shots and rerun the check with a new judge and guard. Two rounds max, then stop even if items remain. If the swap test fails, push World and Signature, styling only. If frozen copy causes the failure, just report it.

## Example

Slop list entry:
`3. Gradient text on the hero heading (.hero h1, 1440 and 390 shots, first screen). Purple-to-pink background-clip text.`

Copy table row (tone only):

| Where | Current | Proposed |
|---|---|---|
| Hero subhead | "Supercharge your workflow today!" | "Plan your week in one place." |

The row changes tone only. Any price, number, name or legal line stays exactly as written, and a change that would alter a claim goes on the approval list instead.

## Output

Final slop marks, test and audit results, and the approval list. End with what you need from the user: merge, revert, or a call on each approval.