# OpenClawCash Agent Wallet (Claude Code plugin)

Managed EVM and Solana wallets for AI agents — balances, transfers, swaps, approvals, governance policy
checks, cross-chain bridges, Escrow (formerly Get Paid) checkout, Polymarket, and YieldWolf Casino. Backed by the
[OpenClawCash agent API](https://openclawcash.com/mcp).

The plugin connects Claude Code to the `openclawcash` MCP server (`@openclawcash/mcp-server` on npm) and
bundles the `agentwalletapi` skill, so Claude follows the same safety model, approval flow, and
wallet-label rules as every other OpenClawCash integration. Wallet keys and policy enforcement stay
server-side.

## Install

```
/plugin marketplace add openclawcash/agentwalletapi-claude-code
/plugin install agentwalletapi@openclawcash
```

Claude Code asks for your API key when you install (it is stored by Claude Code, not in the plugin).
Change it later with `claude plugin configure agentwalletapi@openclawcash`.

Get a key at [openclawcash.com](https://openclawcash.com) (sign up, create a wallet, open API Keys).

## Requirements

| | |
|---|---|
| Required setting | `agent_key`, prompted at install (sensitive) |
| Optional env var | `OPENCLAWCASH_BASE_URL` (default `https://openclawcash.com`) |
| Runtime | Node.js with `npx` available |

The key is only ever sent to `https://openclawcash.com` (or an `https://<subdomain>.openclawcash.com` host).

### Two ways in, two key names

- **The MCP tools** get your key from the install prompt (`agent_key`) and pass it to the server as
  `OPENCLAWCASH_AGENT_KEY`. This is the normal path.
- **The bundled skill's shell script** (`skills/agentwalletapi/scripts/agentwalletapi.sh`) is a separate
  command-line path. It reads `AGENTWALLETAPI_KEY` from a `.env` file that
  `skills/agentwalletapi/scripts/setup.sh` creates next to it. You only need this if you call the script
  directly; the MCP tools work without it.

## What you get

- The `openclawcash` MCP server, exposing wallet, transfer, swap, approvals, checkout, Polymarket, and
  YieldWolf Casino tools.
- The `agentwalletapi` skill — endpoint reference, safety model, and wallet-label rules; see
  [`skills/agentwalletapi/SKILL.md`](skills/agentwalletapi/SKILL.md).

## Layout

```
.claude-plugin/plugin.json   plugin manifest
.claude-plugin/marketplace.json   one-plugin marketplace (what `marketplace add` reads)
.mcp.json                    MCP server declaration
skills/agentwalletapi/       the skill
```

## License

MIT — see [LICENSE](LICENSE). "OpenClawCash" is a trademark of OpenClawCash; forks must not imply
endorsement.
