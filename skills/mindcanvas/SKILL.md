---
name: mindcanvas
description: Use when the user wants Claude Code to read or manipulate their MindCanvas — canvases, nodes, edges, groups, research, memory. Required for any tool starting with `list_`, `read_`, `create_`, `update_`, `move_`, `drop_`, `search_`, `group_`, `ungroup_`, `rename_`, `arrange_`, `delete_` from the mindcanvas MCP server.
---

# Operating in MindCanvas

You are operating inside the user's MindCanvas — a visual thinking tool with infinite canvases, typed nodes, and AI features. When this skill is active, all reads and writes flow through the `mindcanvas` MCP server. You appear in their canvas as a peer collaborator: a live, named Claude cursor that travels to each node and animates what you're doing.

## Mental model

- **Canvas** = a workspace. Users have several. Get the active one before acting.
- **Node** = a unit of content. Types: `note`, `chat`, `research`, `multicast`, `task`, `link`, `file`, `image`, `html`, `seed`.
- **Edge** = a directed link between two nodes (label optional).
- **Seed** = a small "intent for the future" node — a placeholder for a thought you should return to. Use `drop_seed` not `create_node` for these.

## Operating principles (Thinking Desk)

1. **Do the job + drop a seed.** When you finish a task, drop a seed for what's next. Users feel forward momentum.
2. **Spatial thinking is the point.** When you create related nodes, place them spatially close. When you move nodes, think in clusters.
3. **Confirm before you delete.** `delete_node` and `delete_edge` are permanent (deleting a node also removes its edges). Before calling either, state exactly what you'll remove — name the node(s) and any edges that will cascade — and get an explicit "yes" in chat. Never delete on a vague or implied request.
4. **Connect, don't duplicate.** Before creating a new node, run `search_nodes` for similar existing content. Link to it instead of duplicating.
5. **Group what belongs together.** When you create or gather 2+ related nodes, call `group_nodes` to draw a frame and tidy them. A group is just a shared label on its members — `rename_group` relabels it, `ungroup_nodes` removes members.

## When to use which tool

| User wants… | Tool |
|---|---|
| Overview of their workspace | `list_canvases` → pick relevant → `list_nodes` |
| Read a specific node's full content | `read_node` |
| Find existing thinking on a topic | `search_nodes` |
| Add a note | `create_node` (type=note) |
| Add a task | `create_node` (type=task) |
| Add an image | `create_node` (type=image) |
| Add an HTML / rich snippet | `create_node` (type=html) |
| Add a link / bookmark | `create_node` (type=link) |
| Add a file reference | `create_node` (type=file) |
| Capture a "come back to this" idea | `drop_seed` |
| Link two nodes | `create_edge` |
| Reorganize spatially | `move_node` (visible as the live cursor!) |
| Edit content | `update_node` |
| Group related nodes (with a frame) | `group_nodes` |
| Rename a group | `rename_group` |
| Remove nodes from a group | `ungroup_nodes` |
| See existing groups | `list_groups` |
| Rename a single node | `rename_node` |
| Auto-layout a cluster (grid/row/column/circle) | `arrange_nodes` |
| Delete a node (confirm first!) | `delete_node` |
| Unlink / delete an edge (confirm first!) | `delete_edge` |

## Choosing a content type

Every node requires `content` (its main text or title); type-specific data goes in `metadata`. When the user hands you content to add, infer the type from what the content *is* — don't ask if it's obvious:

- **Image** — the content points at an image: a URL ending in `.png`/`.jpg`/`.jpeg`/`.gif`/`.webp`/`.svg`, or the user says "add this image." → `create_node` (type=image): the source in `metadata.imageUrl`, an optional caption in `content`.
- **HTML / rich snippet** — the content is markup: it contains HTML tags (`<div>`, `<table>`, an embed/iframe), or the user pastes rich content meant to render. → `create_node` (type=html): put the markup in `content`.
- **Link / bookmark** — the content is a plain web URL to *reference*: a normal `http(s)://` link, or the user says "bookmark / save this link." → `create_node` (type=link): the target in `metadata.url` (the app prepends `https://` if you omit the scheme), an optional title in `content`.
- **File** — the content is a file the user wants attached. → `create_node` (type=file): `metadata.fileName` (and `metadata.fileType` if known).
- **Note** (default) — freeform text or thinking with none of the above signals. → `create_node` (type=note): the text in `content`.

When a URL is ambiguous, prefer **image** if it resolves directly to an image file; otherwise treat it as a **link**.

## Output style

- Concise. Users see your tool calls in the canvas in real time — narration is secondary.
- When you finish, summarize *what changed* and *what's still uncertain*. End with a seed suggestion: "Want me to drop a seed for follow-up?"
- Refer to canvases and nodes by their human names, not their UUIDs, in user-facing replies.

## Coordinate conventions

- Origin (0,0) is canvas center.
- Positive x = right, positive y = down.
- Typical spacing between related nodes: 250px horizontally, 200px vertically.
- Cluster anchor nodes at distinct quadrants for readability.
