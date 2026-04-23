# SIP — Adopted from `starlightintelligence.org/protocol`

**Pinned version:** `v1.1.0`
**Pinned commit:** [`d69374dbf17432d37a82499edc6f40a90194a51e`](https://github.com/frankxai/Starlight-Intelligence-System/blob/d69374dbf17432d37a82499edc6f40a90194a51e/SIP.md) (canonical SIP.md at adoption time)
**Substrate source of truth:** [`frankxai/Starlight-Intelligence-System`](https://github.com/frankxai/Starlight-Intelligence-System), file `SIP.md`.
**Canonical URL:** [starlightintelligence.org/protocol](https://starlightintelligence.org/protocol)

> **Why pin a commit?** The canonical SIP.md is mutable — Frank Riemer / Starlight Holding BV updates it as the protocol evolves. This kit pins to the commit you adopted. When you upgrade to a newer SIP version, bump the pin and re-attest. SIP semver guarantees a 90-day deprecation window on breaking changes (per SIP § Versioning), so you have time. **Fail-closed verification CI workflow lands in adoption kit v0.2** (per /openclaw-audit CRITICAL 3 remediation).

## What this means

This repo adopts the **Starlight Intelligence Protocol (SIP)** as its substrate. That commits this node to:

- **Layer 1 — File contract.** This repo carries `SKILL.md`, `AGENTS.md`, `MEMORY.md` (required) and `CANON.md`, `SOUL.md`, `STACK.md` (optional but recommended). All present.
- **Layer 2 — Attestation.** Every artifact composed with SIP elements carries a "Built on SIP" block, emitted by `/sip-attest`. Decorative attestation is a breach.
- **Layer 5 — Sovereignty + attribution.** The non-negotiable social contract (SIP § 5) is in force. Sovereignty is not waivable inside this node's declared domain. Attribution on cross-node artifacts is mandatory.

The full spec — including Layers 3 (MCP registry), 4 (command taxonomy), 6 (archetype extension), versioning, and license terms — lives at the canonical URL above. Read it once; this file does not duplicate it.

## License terms (inherited)

- **SIP spec itself:** MIT (Frank Riemer / Starlight Holding BV).
- **Reference command implementations** (`.claude/commands/sip-attest.md`): MIT.
- **Arcanea canon** (if you adopt it via `CANON.md`): CC-BY-NC 4.0, © Arcanea BV.
- **This repo's content** (whatever you build): owned by you, licensed per your `LICENSE` file.

## Worked example — your first attestation

This README itself is a SIP-composed artifact (it loads file-contract, names the protocol, ships with `/sip-attest`). After running `/sip-attest README.md` from this repo, you'll get a block like this:

```
---
**Built on SIP** — Starlight Intelligence Protocol

Substrate: starlightintelligence.org/protocol v1.1.0
Layers used: [file-contract, attestation, commands]

Verticals:
- <your-node-name>@<commit-sha> · adopted SIP via the starlight kit

Canon:
- none

Nodes:
- <your-node-name> · role: sovereign-creator · ships first attested artifact

Generated: <ISO date>
Attestation is compounding, not credit transfer: every composition strengthens every node.
---
```

Paste it into the footer of any artifact you ship. That's the protocol working.

---

**Built on SIP** · v1.1.0 · MIT
