# starlight — SIP adoption kit

**Fork this. Add your domain. Ship attested.**

This is the minimal template for adopting the [Starlight Intelligence Protocol (SIP)](https://starlightintelligence.org/protocol) in your own work. Eleven files, mostly placeholders. You fill them in for your domain — the protocol does the rest.

The full substrate (vaults, agents, MCP, operational layer) lives at [`frankxai/Starlight-Intelligence-System`](https://github.com/frankxai/Starlight-Intelligence-System). You don't need it to start. Adopt this kit, ship one attested artifact, then compose upward when you're ready.

## 60-second adoption

1. **Fork or clone this repo** into your own GitHub.
   ```
   gh repo fork frankxai/starlight my-creator-stack
   cd my-creator-stack
   ```

2. **Edit `SOUL.md`** — replace `<your-name>` and `<your-domain-one-sentence>` with your own. This is the thing that must not drift as you compose with others.

3. **Edit `SKILL.md`** — set the voice rules and invariants for your work. This is what AI agents adopt when they load your context.

4. **Run `/sip-attest README.md`** in Claude Code (or any SIP-aware harness) to emit your first "Built on SIP" attestation block. Paste it into this README's footer.

That's it. You're now a sovereign node on SIP.

## What's in this kit

| File | What it is |
|------|-----------|
| `SIP.md` | Protocol declaration — adopts substrate at a pinned version |
| `SKILL.md` | Behavior contract loaded by AI agents in this repo |
| `AGENTS.md` | Voice slots (architect, sovereign-creator, protocol-defender, implementer, overseer) |
| `MEMORY.md` | Durable state, commitments, open forks |
| `CANON.md` | Optional — your archetypes / world rules / domain constants |
| `SOUL.md` | The 1–3 invariants of your essence that override any protocol convenience |
| `STACK.md` | Stack overrides on top of the recommended sovereign stack |
| `.claude/commands/sip-attest.md` | The one command every SIP node ships with |
| `LICENSE` | MIT, with the SIP scope clause |
| `.gitignore` | Sensible defaults — keeps `private/` and `.starlight/` out |

## Next

- **Spawn verticals.** When one repo isn't enough, declare verticals in your `MEMORY.md` and give each its own SIP-compliant subrepo.
- **Forge alliances.** When you compose with other sovereign nodes, run `/alliance-forge` (lives in the full substrate). Every alliance artifact carries multi-node attestation.
- **Read the spec.** Full SIP at [starlightintelligence.org/protocol](https://starlightintelligence.org/protocol). Full substrate at [`frankxai/Starlight-Intelligence-System`](https://github.com/frankxai/Starlight-Intelligence-System).

---

*Paste your `/sip-attest` output below this line.*
