# MindCanvas for Claude Code

**Think in your terminal. Watch it happen on your canvas.**

Drive your [MindCanvas](https://mindcanvas.app) from Claude Code — read, create,
connect, and reorganize nodes in plain language. Every move lands **live** in the
web app, where a named Claude cursor travels your canvas as it works.

```
> reorganize my "Research" canvas into themes and link the related findings

  ⠿ reading   → 18 nodes, 3 loose clusters
  ⠿ creating  → 3 theme notes
  ⠿ linking   → 18 edges
  Done. Dropped a seed for the next pass.
```

## Install

In Claude Code, run:

```
/plugin marketplace add weelzo/mindcanvas-plugin
/plugin install mindcanvas@mindcanvas
```

On first enable, paste your **MindCanvas session token** when prompted. Get it by
signing in at [mindcanvas.app](https://mindcanvas.app), opening the browser
console (⌥⌘I / F12), and running:

```js
JSON.parse(Object.entries(localStorage).find(([k]) => k.includes('auth-token'))[1]).access_token
```

Copy the `eyJ…` string. Tokens last ~1 hour — when you hit auth errors, grab a
fresh one via `/plugin` → MindCanvas → configure.

The plugin acts as **you**, over HTTPS, scoped to your own canvases. Your token
stays in your OS keychain; no content leaves your MindCanvas.

## Try it

```
> list my canvases
> summarize the "Inbox" canvas and tell me what's unresolved
> create a task list from this meeting note and link it to the project node
> /mindcanvas:mc-cleanup Research      # reorganize a canvas, live
```

## License

MIT © MindCanvas — see [LICENSE](LICENSE).
