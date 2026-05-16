---
name: certorix-diagnostic-assistant
description: Build, navigate, and publish Certorix diagnostic trees and certified facts using the Certorix MCP server. Guides Claude to create structured troubleshooting flows, verify product facts, and connect helpdesk knowledge bases.
---

# Certorix Diagnostic Assistant

## When to use this skill
Use this skill when the user wants to:
- Build or edit diagnostic trees for product troubleshooting
- Navigate an existing diagnostic tree step by step
- Create or search certified product facts
- Connect a helpdesk KB to a diagnostic flow
- Publish a tree with a Certorix VNT cryptographic seal

## How to use the Certorix MCP server

### Available tools
- `list_trees` — list all diagnostic trees in the organization
- `get_tree(treeId)` — get the full node graph of a tree
- `create_tree(metadata, nodes)` — create a new tree
- `update_tree(treeId, metadata, nodes)` — update an existing tree
- `publish_tree(treeId)` — publish and generate a VNT seal
- `list_facts(q?, status?)` — search the certified facts library
- `create_fact(subject, predicate, object)` — add a new certified fact
- `list_kb_articles(q?)` — browse synced helpdesk KB articles
- `get_helpdesk_status` — check helpdesk integration status

### Node types for diagnostic trees
- `question` — branching node with `options[]`, each with `text` and `nextNodeId`
- `solution` — terminal node with `message` and optional `kbArticles[]` and `ticketAction`
- `info` — informational step with `text` and `nextNodeId`
- `input` — collects user input with `label` and `nextNodeId`
- `condition` — evaluates logic with `conditions[]` and `defaultNextNodeId`
- `jump` — redirects to another node with `targetNodeId`

### Rules
1. Always call `list_trees` before suggesting edits — confirm the tree exists
2. Every node must have a valid `nextNodeId` pointing to an existing node
3. Trees must have a `startNodeId` and at least one `solution` node
4. Call `get_tree` before `update_tree` to inspect the current structure
5. After creating or updating a tree, offer to call `publish_tree`

### Example: creating a tree
```json
{
  "metadata": { "title": "WiFi Connectivity", "startNodeId": "q_start" },
  "nodes": {
    "q_start": { "type": "question", "text": "Is the WiFi indicator on?", "options": [
      { "text": "Yes", "nextNodeId": "q_signal" },
      { "text": "No",  "nextNodeId": "s_power" }
    ]},
    "q_signal": { "type": "question", "text": "Can you see your network name?", "options": [
      { "text": "Yes", "nextNodeId": "s_password" },
      { "text": "No",  "nextNodeId": "s_router" }
    ]},
    "s_power":    { "type": "solution", "message": "Check that the device WiFi is enabled in Settings." },
    "s_password": { "type": "solution", "message": "Try re-entering your WiFi password." },
    "s_router":   { "type": "solution", "message": "Restart your router and try again." }
  }
}

