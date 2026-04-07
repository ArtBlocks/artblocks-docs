# Agent Skills

[Agent Skills](https://github.com/ArtBlocks/skills) are markdown instruction files that teach AI agents domain-specific workflows and best practices for Art Blocks. They tell the agent *how* to use MCP tools effectively — which tool to pick for a given question, what parameters matter, what order to call tools in, and how to interpret results.

Skills activate automatically based on what you ask. No special syntax needed — just prompt naturally.

---

## Why install skills?

Without skills, agents can call MCP tools but lack Art Blocks domain knowledge. With skills installed, agents know:

- **Which tool to use** for each type of question (e.g., `get_artist` for artist lookups vs. `discover_projects` for browsing)
- **How to chain tools** together (e.g., check eligibility before building a mint transaction)
- **Art Blocks concepts** like project ID format, verticals, hash-based determinism, and user profiles with linked wallets
- **Best practices** for GraphQL queries (preferred `_metadata` tables, chain filtering, curated field lists)

---

## Installation

### Quick install (all skills)

```bash
npx skills add ArtBlocks/skills
```

### Global install (available across all your projects)

```bash
npx skills add ArtBlocks/skills -g
```

### Install to a specific agent

```bash
npx skills add ArtBlocks/skills -a cursor
npx skills add ArtBlocks/skills -a claude-code
```

After installing, reload Cursor (`Cmd+Shift+P` → "Reload Window") for skills to take effect.

---

## Available Skills

| Skill | Use when... |
|-------|-------------|
| [**discover-artblocks-projects**](https://github.com/ArtBlocks/skills/blob/main/skills/discover-artblocks-projects/SKILL.md) | Browsing, searching, or filtering projects — what's live, dropping soon, in a wallet, or matching a tag/price range |
| [**get-artist**](https://github.com/ArtBlocks/skills/blob/main/skills/get-artist/SKILL.md) | Looking up an artist and exploring their body of work across Art Blocks |
| [**get-token-metadata**](https://github.com/ArtBlocks/skills/blob/main/skills/get-token-metadata/SKILL.md) | Looking up a specific token's traits, media URLs, listing info, owner, hash, and project context |
| [**mint-artblocks-token**](https://github.com/ArtBlocks/skills/blob/main/skills/mint-artblocks-token/SKILL.md) | Minting a token — pricing, minter types, allowlists, multi-wallet eligibility, building transactions |
| [**scaffold-art-script**](https://github.com/ArtBlocks/skills/blob/main/skills/scaffold-art-script/SKILL.md) | Creating or converting a generative art script for Art Blocks (p5.js, Three.js, vanilla JS) |
| [**configure-postparams**](https://github.com/ArtBlocks/skills/blob/main/skills/configure-postparams/SKILL.md) | Setting on-chain PostParam values on a minted token |
| [**query-artblocks-data**](https://github.com/ArtBlocks/skills/blob/main/skills/query-artblocks-data/SKILL.md) | Custom GraphQL queries for data not covered by domain-specific tools (sales history, aggregations, complex joins) |

Each skill is a standalone markdown file — click any skill name above to read the full source.

---

## Supported Agents

Skills work with any agent that supports the [open agent skills spec](https://skills.sh). The Art Blocks MCP server can be connected to any agent that supports MCP over HTTP.

| Agent | MCP | Skills |
|-------|-----|--------|
| Cursor | ✅ | ✅ |
| Claude Code | ✅ | ✅ |
| Claude Desktop | ✅ | — |
| Codex | ✅ | ✅ |

---

## Manual Installation

If your agent doesn't support `npx skills`, you can copy skill directories directly:

```bash
# Clone the repo
git clone https://github.com/ArtBlocks/skills.git

# Copy all skills into your project
cp -r skills/skills/* /your-project/.cursor/skills/

# Or copy a single skill
cp -r skills/skills/discover-artblocks-projects /your-project/.cursor/skills/
```

For personal/global use, copy into `~/.cursor/skills/` instead of a project directory.

---

## Feedback

Found a bug, missing a skill, or have a suggestion?

- **GitHub Issues** — [open an issue](https://github.com/ArtBlocks/skills/issues)
- **Discord** — reach out in the [Art Blocks Discord](https://discord.gg/artblocks)
