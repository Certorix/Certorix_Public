Certorix
Multi-tenant SaaS platform for AI-powered diagnostic trees and cryptographically verified product knowledge.

What is Certorix?
Certorix combines two tightly integrated products under one account:

🌳 Diagnostic Tree Builder — Build and embed guided diagnostic trees that walk customers and Ai/Llms step-by-step through troubleshooting, leading them to clear resolutions or support tickets.
🔬 FactFlow — Publish structured product claims (semantic triples), verify them with AI, and certify them with zero-knowledge proofs (BBS+ tokens).

Together they form a product trust layer: from structured guided support to cryptographically verifiable product facts.

Beta — free to start, no credit card required → certorix.online


Products at a Glance
🌳 Diagnostic Tree Builder
Feature Details Editor Visual drag-and-drop, 6 node typesAI Generation Generate trees from plain text in seconds via AI AssistantChat — ask anything about your flows Signing Every published tree is HMAC-SHA256 signed → DTT Verified sealEmbediFrame, Freshdesk portal, shareable link, AI chat widgetIntegrationsFreshdesk, MCP (ChatGPT / AI agents), Widget Generator History Version history with rollback, undo/redo, auto-save
Node types:
Type Purposequestion Presents options that route to other nodes input Captures free-text, stored as a variable info Displays instructions or images condition Auto-routes based on previously captured valuessolutionEnd of branch — resolution, KB links, action buttonsjumpContinues flow inside another tree

🔬 FactFlow — AI-Verified Product Facts
Feature Details FactsSemantic triples: Subject > Predicate > Object AI Verification Zero-knowledge proof (selective disclosure) VNTs Veridium Notary Tokens (Ed25519) — gold / silver / bronze tiers Knowledge Graph Visual graph of all published facts as nodes and edges LifecycleDraft → AI Verified → Certified → Published

API
Full OpenAPI 3.0 spec: docs/api/openapi.yaml · Live spec
Public endpoints (no auth)
GET  /public/search-tree            — Search published trees by org
POST /public/diagnostic/start       — Start a diagnostic session
POST /public/diagnostic/next        — Advance one step
GET  /public/diagnostic/:sessionId  — Get session state
POST /public/tickets/create         — Create Freshdesk ticket from widget
GET  /public/vnt/:vntId             — Verify a Veridium Notary Token

Private endpoints require Authorization: Bearer <jwt>.

MCP / AI Agent Integration
Certorix exposes an MCP plugin so AI agents (ChatGPT, Claude, custom agents) can search and run diagnostic trees programmatically:

About the Creator
Certorix is built and maintained by Jaume Martí Anguera.

🌐 Website: certorix.online
📬 Contact: via certorix.online
