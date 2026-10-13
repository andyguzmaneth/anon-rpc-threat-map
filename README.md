# anon-RPC threat map

> **DRAFT / EXPERIMENTAL.** Personal working notes, not an Ethereum Foundation publication.
> Not reviewed, not a security audit. Most ratings are analysis, not measurement, and will change.
> Do not cite this as the anon-RPC threat model.

Page: https://andyguzmaneth.github.io/anon-rpc-threat-map/

A map of who can learn what about a wallet user when RPC traffic goes through
[anon-RPC](https://github.com/ethereum/anon-rpc), by adversary and by the anonymity network plugged into it.

anon-RPC is a socket: a wallet loads a hash-pinned worker, and the worker carries traffic over one network.
Workers exist for Tor (tor-js), Nym (mixFetch) and Nox. Each network gives different protection, so the
ratings belong to the network, not to anon-RPC. Hiding the user's IP from the RPC provider is one adversary.
This repo maps the others: exit, entry and bridge nodes, an operator with a network share, the user's ISP,
the network near the RPC, an ISP and RPC provider together, a national government, a global passive
adversary, an active on-path attacker, the code path that delivers the worker and the node list, the
wallet's own backends, and the public chain as the second end of timing attacks.

## What is on the page

- **Network profiles.** Each network on the properties that decide the ratings: who sees the user's IP,
  mixing delay, cover traffic, end-to-end TLS, message sizes, who runs the nodes, where the node list comes
  from, client identity, blocking resistance, who controls the worker pin, latency.
- **Compare networks.** One property (default: can the adversary link IP to on-chain address), every
  adversary, every network side by side.
- **Rating a network that plugs in.** The method: eleven questions, and which cells each answer decides.
  Use it to rate a network before it has a column.
- **Adversary matrix.** Adversaries as rows. Columns show what each one can learn: IP, query content,
  linkable sessions, timing, the link from IP to on-chain address, and whether it can single out the user
  as an anonymity-tool user. Cells are rated protected, at risk, exposed, unmeasured, or no vantage point.
  The format follows the [Privacy Benchmark](https://privacybenchmark.org/projects/aztec?tab=matrix)
  adversary matrix.
- **Stack selector.** Five options: direct RPC (baseline), Tor with an exit, Tor to an onion service, Nym,
  and Nox. Three optional layers: PIR, traffic shaping in the worker, and jurisdiction-diverse RPCs.
  Changed cells are outlined.
- **Path diagram.** Where each adversary sits on the request path for the selected transport.
- **Helps and gaps, attacks, defenses with status, draft scope, open questions, sources.**

## Layout

| Path | Content |
|---|---|
| `docs/index.html` | The page. Self-contained, no build step, no external requests. |
| `docs/model.js` | All data: properties, networks with profiles, rating rules, layers, adversaries with per-cell ratings and notes, attacks, defenses, questions, sources. Edit this file to change the map. |

Rating codes in `model.js`: `P` protected, `R` at risk, `X` exposed, `U` unmeasured, `N` no vantage point.
Each adversary has one six-character string per network, in column order. Notes and layer overrides are
keyed by a network id, a comma-separated list of ids, or `all`.

### Adding a network

1. Add an entry to `networks` in `docs/model.js` with every `profile` field filled and a `path`.
2. Answer the questions in `rules` for it. Each answer names the cells it decides.
3. Add a cells string and notes for that network to every adversary.

To view locally, open `docs/index.html` in a browser.

## Status of the content

- Spec facts are checked against anon-rpc `SPEC.md` v0.3.2 (2026-09-25).
- Latency figures are single-run measurements from one location.
- Nym and Nox facts come from their worker repositories. The Nox operator count comes from its public
  topology endpoint on 2026-10-13 and will change as operators join.
- Mixnet ratings against timing and both-ends observers are design properties. None is measured.
- Traffic shaping, timing-safe tx watching, delayed broadcast, and jurisdiction diversity are proposals.
- The scope section is a draft position, not an agreed one.

Corrections and disagreements are welcome as issues.

## License

Content is released under [CC0 1.0](LICENSE).
