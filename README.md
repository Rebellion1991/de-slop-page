# de-slop-page

Claude skill that strips the AI look from a web page's styling (gradients, glows, emoji, drifting spacing) without touching features or copy facts.

## What it does

Audits a page at desktop and phone width, lists every sign of AI slop, proposes a visual direction and a tone-only copy table, then stops for your approval. After that it works through nine styling passes on a new branch, one commit each, and checks the result with an independent judge and guard. It never pushes or merges.

## Example

Slop list entry: `3. Gradient text on the hero heading (.hero h1, first screen)`.

| Where | Current | Proposed |
|---|---|---|
| Hero subhead | "Supercharge your workflow today!" | "Plan your week in one place." |

Prices, numbers, names and legal lines never change.

## Install

**As a plugin (marketplace):**

```bash
claude plugin marketplace add Rebellion1991/de-slop-page
claude plugin install de-slop-page@de-slop-page
```

**Manually (copy the skill folder):**

```bash
git clone https://github.com/Rebellion1991/de-slop-page
cp -r de-slop-page/skills/de-slop-page ~/.claude/skills/
```

## Use

Ask Claude to de-slop, humanize or remove the AI look from a page, and give it the local dev URL. The skill needs a browser tool (Chrome DevTools MCP preferred) and the repo folder.

Status: early release, not yet tested on real pages.

## License

MIT. See [LICENSE](LICENSE).
