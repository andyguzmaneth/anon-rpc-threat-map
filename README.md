# anon-RPC threat map

> **DRAFT / EXPERIMENTAL.** Personal working notes, not an Ethereum Foundation publication.
> Not reviewed, not a security audit. Most ratings are analysis, not measurement, and will change.
> Do not cite this as the anon-RPC threat model.

Page: https://andyguzmaneth.github.io/anon-rpc-threat-map/

A map of who can learn what about a wallet user when RPC traffic goes through
[anon-RPC](https://github.com/ethereum/anon-rpc). Hiding the user's IP from the RPC provider is one
adversary. This repo maps the others: exit and guard relays, the tor-js gateway, a relay operator with a
network share, the user's ISP, the network near the RPC, an ISP and RPC provider together, a national
government, a global passive adversary, an active on-path attacker, the code path that delivers the worker,
the wallet's own backends, and the public chain as the second end of timing attacks.

## What is on the page

- **Adversary matrix.** Adversaries as rows. Columns show what each one can learn: IP, query content,
  linkable sessions, timing, the link from IP to on-chain address, and whether it can single out the user
  as an anonymity-tool user. Cells are rated protected, at risk, exposed, unmeasured, or no vantage point.
  The format follows the [Privacy Benchmark](https://privacybenchmark.org/projects/aztec?tab=matrix)
  adversary matrix.
- **Stack selector.** Four transports: direct RPC, anon-RPC with a Tor exit, anon-RPC to an onion service,
  and a mixnet with cover traffic. Three optional layers: PIR, traffic shaping in the worker, and
  jurisdiction-diverse RPCs. Changed cells are outlined.
- **Path diagram.** Where each adversary sits on the request path for the selected transport.
- **Helps and gaps, attacks, defenses with status, draft scope, open questions, sources.**

## Layout

| Path | Content |
|---|---|
| `docs/index.html` | The page. Self-contained, no build step, no external requests. |
| `docs/model.js` | All data: properties, transports, layers, adversaries with per-cell ratings and notes, attacks, defenses, questions, sources. Edit this file to change the map. |

Rating codes in `model.js`: `P` protected, `R` at risk, `X` exposed, `U` unmeasured, `N` no vantage point.
Each adversary has one six-character string per transport, in column order. A layer overrides single
cells with a value and a note.

To view locally, open `docs/index.html` in a browser.

## Status of the content

- Spec facts are checked against anon-rpc `SPEC.md` v0.3.2 (2026-09-25).
- Latency figures are single-run measurements from one location.
- The mixnet column describes design goals. No mixnet transport is integrated with anon-RPC.
- Traffic shaping, timing-safe tx watching, delayed broadcast, and jurisdiction diversity are proposals.
- The scope section is a draft position, not an agreed one.

Corrections and disagreements are welcome as issues.

## License

Content is released under [CC0 1.0](LICENSE).
