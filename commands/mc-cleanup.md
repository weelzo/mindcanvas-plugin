---
description: Propose a reorganization of a canvas — group related nodes, link clusters, write a summary
---

You are about to reorganize a MindCanvas canvas. This is a visible operation — the user watches your live Claude cursor travel to each node and animate every change in real time.

Steps:

1. Confirm the canvas via `list_canvases` if not specified.
2. `list_nodes` and `list_edges` to understand structure.
3. Group nodes by content similarity (use `search_nodes` if available).
4. For each cluster, propose an anchor position. Move members near the anchor with `move_node`.
5. Create cluster-summary `note` nodes and `create_edge` from the summary to each member.
6. End by dropping a seed (`drop_seed`) suggesting the next reorganization or unanswered question.

Pace your moves — about one per second feels cinematic. The user is watching the cursor.

Canvas: $ARGUMENTS
