---
order: 400
description: Agent archetypes and use cases for the Art Blocks MCP server.
---

# What Can You Build

Four agent archetypes to show what's possible with 21 tools and 500+ on-chain generative art projects.

---

## Autonomous Collector

An agent that monitors live mints and acts on configurable criteria.

Poll `discover_live_mints` on a schedule, filter by price or scarcity, evaluate trait distributions and secondary floor via `get_project`, then build a ready-to-sign transaction.

> "Alert me when an Art Blocks Studio project drops below 0.05 ETH with more than 50% supply remaining. If the secondary floor is above mint price, auto-build the transaction."

---

## Creator Pipeline

An agent that helps artists set up, launch, and manage their projects.

Scaffold a new project with `scaffold_artblocks_project` (vanilla JS, p5.js, or Three.js), monitor mint progress after launch, track who's collecting, and manage PostParams configuration.

> "Scaffold a p5.js project. After launch, track mint velocity and alert me when 50% is sold."

---

## Social Collector

An agent that powers collection-driven social experiences.

Load any wallet's collection via `get_wallet_tokens`, cross-reference collections between wallets to find taste overlap, and surface recommendations based on owned artists and project tags.

> "Compare my collection with 0xabc's. What artists do we both collect? What do they own that I don't?"

---

## Research Agent

An agent for market intelligence, art historical research, or curation.

Search the full catalog with `discover_projects`, pull trait and rarity data, build artist profiles with `get_artist`, and run custom queries via the GraphQL tools for advanced analysis.

> "Find all curated p5.js projects from 2023 that are sold out. Rank by secondary floor price."
