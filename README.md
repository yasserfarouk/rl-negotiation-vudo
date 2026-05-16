# Reinforcement Learning for Automated Negotiation: A Utility-Dependent Outcome Projection Codec

**Yasser Mohammad** — NEC Corporation, Tokyo, Japan
`y.mohammad@nec.com`

This repository hosts the [paper](paper.pdf) and [poster](poster.pdf) for our work
on a new *codec* (observation encoder + action decoder) for reinforcement
learning in automated negotiation, published in the **8th Games, Agents, and
Incentives Workshop (GAIW 2026)**, held with **AAMAS 2026** (25th
International Conference on Autonomous Agents and Multiagent Systems,
25–29 May 2026, Paphos, Cyprus).

## Main idea

Most RL approaches to automated negotiation pick one of two extremes when
encoding offers for the policy:

- **Utility-Projection** — represent each offer by its scalar utility. This
  generalizes across scenarios but discards *all* outcome-space structure: a
  buyer cannot tell that the seller is anchored on a specific delivery date.
- **Raw-Outcome** — represent each offer as a one-hot or per-issue vector.
  This retains structure but breaks the moment the issues, utility function,
  or outcome-space size changes.

We propose **VUDO** (Vector Utility-Dependent Outcome projection): encode each
outcome as the *vector of weighted value-function evaluations* of a Generalized
Linear Aggregation (GLA) utility. Two outcomes that yield the same value-function
vector for every agent are *negotiation-equivalent* — they share utilities,
ranks, and relations to every other outcome — so the policy gets everything
it needs to act, with a representation that is **invariant** to outcome-space
size and issue labeling. The action decoder inverts the projection via cached
nearest-neighbour search, so any standard RL algorithm and architecture works
out of the box (no hand-crafted features, no graph neural networks).

We also introduce **NegMAS-RL**, a unified framework that represents an
RL-for-AN problem as a tuple `(D, C = (OE, AD), RF)`. Most existing SOTA
methods — RLBOA, Sengupta, VeNAS, MiPN, Renting⁺, … — turn out to be
specific choices of `(OE, AD, RF)` on the same PANSession Generation Process.

**Empirically**, VUDO outperforms SOTA RL and heuristic baselines on the
hardest generalization scenarios (varying utilities, outcome spaces,
reservation values, and opponents) in advantage, welfare, and fairness, and
matches SOTA heuristics on simple single-scenario, single-opponent settings.
It adds only ~3.5% parameters and ~1.5% training time over the closest
generalist baseline.

## Files

| File | Description |
|---|---|
| [`paper.pdf`](paper.pdf) | GAIW 2026 paper |
| [`poster.pdf`](poster.pdf) | GAIW 2026 poster (A0) |

## Citation

```bibtex
@inproceedings{mohammad2026vudo,
  author    = {Yasser Mohammad},
  title     = {Reinforcement Learning for Automated Negotiation:
               A Utility-Dependent Outcome Projection Codec},
  booktitle = {Proceedings of the 8th Games, Agents, and Incentives Workshop (GAIW 2026),
               held with the 25th International Conference on Autonomous Agents
               and Multiagent Systems (AAMAS 2026)},
  year      = {2026},
  month     = may,
  address   = {Paphos, Cyprus},
  note      = {Workshop paper}
}
```
