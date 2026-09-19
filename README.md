# starlight — SIP adoption kit

A minimal template for adopting the [Starlight Intelligence Protocol (SIP)](https://starlightintelligence.org/protocol)
in your own repository. Fork it, describe your work in `sip-profile.json`, push, and CI produces a
conformance receipt that is signed with Sigstore and checkable by anyone.

The full substrate (vaults, agents, MCP, operational layer) lives in
[`frankxai/Starlight-Intelligence-System`](https://github.com/frankxai/Starlight-Intelligence-System).
You do not need it to use this kit.

## What is verifiable and what is declared

- **Verifiable:** the receipt. `sip/conform.mjs` checks `sip-profile.json` against 17 rules and writes
  a receipt that pins the profile's SHA-256. On every push to `main`, CI attests that receipt with
  GitHub artifact attestations (Sigstore keyless signing, public transparency log). Anyone can check
  it with `gh attestation verify`, and anyone can re-run the checker on the same bytes.
- **Declared:** the "Built on SIP" block that `/sip-attest` emits (see `SIP.md`). It is a label you
  write about your own work. Nothing signs it and nothing checks it. Treat it as a pointer to the
  receipt, not as evidence.

A PASS receipt says the profile is well-formed and its projections do not leak. It does not say the
claims inside the profile are true. That is what the Source and Evaluation nodes are for: they name
what a reader can check each claim against.

## Quickstart

1. **Fork**

   ```bash
   gh repo fork frankxai/starlight --clone --fork-name my-sip-node
   cd my-sip-node
   ```

   Attestations work on public repositories on any plan. For private repositories they need GitHub
   Enterprise Cloud; the conform step still runs everywhere.

2. **Edit `sip-profile.json`.** It currently describes this kit: its maintainer, the kit itself,
   one claim (that `sip/` is an unmodified copy of the upstream checker at `sip/PINNED_COMMIT`), the
   file that claim rests on, and the conformance run. Replace every node with your own. Start from
   `protocol/fixtures/valid-profile.json` in the SIS repository if you need more node types; the
   node and edge types are documented in `protocol/README.md` there.

   Check it locally. Node 18 or later, nothing to install:

   ```bash
   node sip/conform.mjs sip-profile.json --json sip-receipt.json
   ```

   Exit 0 is PASS, 1 is FAIL (the output names every failing element), 2 is a usage or parse error.

3. **Push to `main`.** `.github/workflows/sip-receipt.yml` then:
   - checks that `sip/` matches upstream `protocol/` at `sip/PINNED_COMMIT`, byte for byte;
   - runs the checker and fails the job unless the verdict is PASS;
   - uploads `sip-receipt.json` as a workflow artifact;
   - on `main` only, attests it: subject `sip-profile.json`, predicate the receipt.

   Pull requests run the same checks without attesting.

   If your fork should not claim the vendoring (for example, you patched `sip/`), delete that claim
   from your profile and the vendoring step from the workflow.

4. **Verify**, from any machine with the GitHub CLI:

   ```bash
   gh attestation verify sip-profile.json \
     --repo <you>/<fork> \
     --predicate-type https://starlightintelligence.org/protocol/receipt/v0.1.0
   ```

   This checks that the file you hold has the digest the attestation names, that it was signed by
   your repository's workflow, and that the entry is in the transparency log. Add `--format json` to
   read the receipt itself.

   `.gitattributes` keeps `sip-profile.json` byte-exact across checkouts; without that, a Windows
   checkout with `core.autocrlf` would hash differently and fail verification.

## Offline signing

For private work, or when nothing may be published to a log: Ed25519 over a DSSE v1 envelope around
an in-toto v1 Statement. Nothing leaves your machine.

```bash
node sip/sign.mjs keygen .sip                     # once; writes .sip/.gitignore for the private key
node sip/conform.mjs sip-profile.json --json sip-receipt.json
node sip/sign.mjs sip-receipt.json --key .sip/sip-signing.key --out sip-receipt.dsse.json
```

Publish `.sip/sip-signing.pub` and the envelope. A verifier runs:

```bash
node sip/verify.mjs sip-receipt.dsse.json --pub .sip/sip-signing.pub --profile sip-profile.json
```

`--profile` re-runs the checker on the exact bytes and requires the same verdict, so the verifier
trusts the checker rather than the signer. `sign.mjs` refuses to sign anything but a complete PASS.

Never commit `.sip/sip-signing.key`. `keygen` writes a `.gitignore` next to it and this repository's
`.gitignore` also excludes it. On Windows the key is protected only by its folder's ACL; `keygen`
prints the `icacls` command that restricts it.

## Which spec is canonical

`sip/PINNED_COMMIT` names the `frankxai/Starlight-Intelligence-System` commit the checker was copied
from. That commit's `protocol/` (graph v0.1.0) and `SIP.md` (v1.1.1 at the time of copying) are the
canonical spec for this kit. `SIP.md` in this repository is the older v1.1.0 adoption note pinned to
`d69374d`; it is kept for its layer 1–5 summary and is not the reference.

To update the checker, repeat the copy from a newer checkout and commit the new `PINNED_COMMIT` with
it, as described in `protocol/INSTALL.md` upstream.

## What's in this kit

| File | What it is |
|------|-----------|
| `sip-profile.json` | The evidence graph this repository publishes about itself |
| `sip/` | The vendored checker, signer and verifier. Zero dependencies. MIT, from upstream |
| `sip/PINNED_COMMIT` | The upstream commit `sip/` was copied from |
| `.github/workflows/sip-receipt.yml` | Vendoring check, conformance, receipt attestation |
| `SIP.md` | SIP adoption note (v1.1.0, see above) |
| `SKILL.md` | Behavior contract loaded by AI agents in this repo |
| `AGENTS.md` | Voice slots (architect, sovereign-creator, protocol-defender, implementer, overseer) |
| `MEMORY.md` | Durable state, commitments, open forks |
| `CANON.md` | Optional: archetypes, world rules, domain constants |
| `SOUL.md` | The 1–3 invariants of your essence |
| `STACK.md` | Stack overrides |
| `.claude/commands/sip-attest.md` | Emits the declared "Built on SIP" block |
| `LICENSE` | Repository license notice (see below) |

## License

See `LICENSE`. As of commit `c25cee2` the kit's own text is not under an open license; the vendored
`sip/` code remains MIT under its upstream source, `frankxai/Starlight-Intelligence-System`.

## Not included

Nothing is registered, listed or verified by Starlight. There is no directory of adopters. The value
of a receipt is that your claims carry a checkable chain, to you first and to anyone reading your
repository second.
