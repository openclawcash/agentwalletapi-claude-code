# OpenClawCash Agent Wallet (Claude Code plugin)

Managed EVM and Solana wallets for AI agents — balances, transfers, swaps, approvals, governance policy checks, cross-chain bridges, Get Paid checkout escrow, Polymarket, and YieldWolf Casino. Backed by the [OpenClawCash agent API](https://openclawcash.com/mcp).

This plugin connects Claude Code to the OpenClawCash MCP server (`@openclawcash/mcp-server` on npm) and bundles the `agentwalletapi` skill so Claude reads the same safety model, workflow, and wallet-label rules that every other OpenClawCash integration uses.

## Install

```
/plugin install openclawcash/agentwalletapi-claude-code
```

This is a standalone repo (`.claude-plugin/plugin.json` sits at its own root), so it installs directly — no marketplace step needed. Confirmed: `/plugin marketplace add owner/repo` only ever discovers `.claude-plugin/marketplace.json` at a repo's literal root, with no subpath support, so a plugin nested in a subfolder of a bigger repo needs one and a plugin at a repo's own root doesn't. This repo is one of three siblings (`../codex/`, `../hermes/`) that live in the same local folder for development convenience, but each publishes as its own separate repo.

After installing, set your API key before starting Claude Code:

```bash
export OPENCLAWCASH_AGENT_KEY=occ_your_api_key
```

Get a key at [openclawcash.com](https://openclawcash.com) (sign up, create a wallet, open API Keys).

## What you get

- The `openclawcash` MCP server (`npx -y @openclawcash/mcp-server`), exposing wallet, transfer, swap, checkout, Polymarket, and YieldWolf Casino tools.
- The `agentwalletapi` skill, so Claude follows the same approval-mode and policy-check guidance as every other OpenClawCash client.

See [`skills/agentwalletapi/SKILL.md`](skills/agentwalletapi/SKILL.md) for the full endpoint reference, safety model, and wallet label rules.

## Maintainers

This plugin's `skills/agentwalletapi/` is **hard-linked** to `../codex/skills/agentwalletapi/` — same bytes, same inode, one copy on disk across both sibling repos, but each still stands alone if published/cloned separately. Neither is the source of truth; [agentwalletapiSkill](https://github.com/openclawcash/agentwalletapi) is. After a version bump there, from the parent folder (not from inside this repo):

```bash
bash ../scripts/sync-skill.sh
```

then bump `version` in this repo's `.claude-plugin/plugin.json` and the sibling `../codex/.codex-plugin/plugin.json`, and commit each repo separately.
