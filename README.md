# DSH Build Hermeticity Proof

**Maintainer / Author：贺去病 (He Fangsheng / Dosen) · [hequbing.com](https://www.hequbing.com)**

An offline, deterministic evidence layer for DeepSeek Harness supply chains. It verifies whether an explicit, hash-only build access receipt stayed inside its declared file, environment, network, clock, randomness and output closure.

It **does not execute** a build, **does not enforce** a sandbox, authenticate the receipt, or prove that unrecorded accesses could not occur. It also **does not prove reproducibility**. A `hermetic` verdict means only that the supplied receipt is internally complete and policy-conformant.

## Complementary boundary

- `dsh-reproducible-build-proof` compares independently operated rebuild receipts for byte-identical specified outputs.
- `dsh-attestation-proof` verifies DSSE/in-toto signatures, subjects and signer thresholds.
- This plugin checks one recorded build's declared external-influence closure: file reads/writes, environment reads, network, clock and randomness.

Observed undeclared access fails. A denied undeclared attempt is retained as containment evidence but does not breach the closure. Observed network access always fails under the v1 deny-only network policy. Declared inputs and outputs must all appear in the receipt; the source revision, invocation, clock value, random seed and allowed environment values are hash-bound.

## Install

```bash
dsh plugin add github:dongsheng123132/dsh-build-hermeticity-proof#COMMIT
```

The bundle exposes `dsh_build_hermeticity_inspect` and `dsh_build_hermeticity_verify` from one headless core. The independent MCP stdio server exposes `build_hermeticity_inspect` and `build_hermeticity_verify`. The CLI accepts `inspect` or `verify` plus an explicit JSON path.

See [`examples/hermetic.json`](examples/hermetic.json). Reports contain only hashes, counts, booleans, classifications and verdicts. Secret-shaped material, raw logs and body/content fields are rejected. The DSH verify tool reads a workspace-relative non-symlink manifest, writes only to an explicit workspace-relative `artifactDir`, creates deterministic content-addressed output exclusively, and verifies it by read-back.

```bash
npm test
npm run check
npm run smoke:plugin
npm run smoke:mcp
python C:/Users/YOU/.codex/skills/.system/plugin-creator/scripts/validate_plugin.py .
```

Node.js 22 or newer is required. The verifier has no runtime dependency, spawns no process and makes no network request.
