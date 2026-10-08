# Threat model

| Threat | Control or limitation |
|---|---|
| Spoofing | Admin/member authorization, absent-auth tests. |
| Tampering | Fixed unique membership, checked arithmetic, bounded loops. |
| Repudiation | Events and transaction receipts; no real-world identity guarantees. |
| Information disclosure | Public addresses/amounts; no personal fields. |
| Denial of service | Missing contributors can lock pots indefinitely; no recovery. |
| Elevation of privilege | No admin withdrawal; only fully funded settlement. |

Malicious or frozen tokens and storage archival remain risks. An independent human review is pending.
