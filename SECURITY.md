# Security

Report vulnerabilities privately through GitHub Security Advisories. Never attach real credentials, raw build logs, authorization headers, cookies, private keys, source archives or artifact bodies.

The verifier is offline and non-executing. It rejects traversal, symlink inputs, oversized manifests, malformed hashes, secret-shaped material and raw/log/body/content fields. Artifact writes stay inside an explicit workspace-relative directory and are verified by read-back.

A conforming receipt is not proof that the recorder or sandbox was trustworthy and is not provenance authentication. Pair this verifier with a trusted access recorder, enforced sandbox and signed provenance where those properties matter.
