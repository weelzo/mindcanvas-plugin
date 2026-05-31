---
description: Open / list / inspect a MindCanvas canvas
---

You have been asked to operate on a MindCanvas. Steps:

1. Call `list_canvases` to see what's available.
2. If the user named a specific canvas, find it by name (case-insensitive). Otherwise, ask which one.
3. Call `list_nodes` on that canvas and report a brief structural summary: total nodes, breakdown by type, any obvious clusters or orphans.
4. Ask the user what they want to do next.

User request: $ARGUMENTS
