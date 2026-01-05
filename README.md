# CIA × Opacity: A Framework for Measuring Multi-Agent Cooperation

## Motivation

Cooperation in multi-agent systems is typically evaluated with aggregate metrics—team score, social welfare, win rate. These numbers obscure the underlying causes of success or failure:

- Agents may fail despite **aligned incentives** because coordination is difficult.
- Agents may fail despite **easy coordination** because incentives are misaligned.
- Agents may succeed in **self-play** yet collapse with novel partners, revealing brittle conventions rather than robust cooperative capacity.

A single performance number conflates these distinct failure modes. Without disentangling them, we cannot make precise claims about when and why cooperation emerges or breaks down.

## Core Question

**How do cooperation outcomes and robustness change as we independently vary incentive alignment and information difficulty?**

## Two Organizing Axes

This framework decomposes multi-agent settings along two orthogonal dimensions:

### Common-Interest Alignment (CIA)

CIA captures the degree to which agents' objectives are shared versus contested.

- **High CIA**: Agents have largely compatible objectives. The challenge is coordination—finding compatible strategies, not negotiating over surplus.
- **Low CIA**: Agents have partially conflicting objectives. Cooperation involves bargaining, contested resource allocation, or social dilemmas where individual and collective interests diverge.

### Information Opacity

Opacity captures the inferential difficulty agents face in understanding the environment and each other.

Opacity increases through:
- Partial observability (limited sensing, occlusion)
- Observation noise
- Delayed or sparse feedback
- Private information (hidden types, values, intentions)
- Weak public monitoring

The goal is to treat information difficulty as a **controlled experimental variable** rather than an uncontrolled confound.

## The CIA × Opacity Map

The two axes define a space where different cooperative challenges live:

```
                         Information Opacity
                    Low                     High
                ┌───────────────────┬───────────────────┐
                │                   │                   │
      High      │   COORDINATION    │    COORDINATION   │
       CIA      │   (transparent)   │    (opaque)       │
                │                   │                   │
                │  Shared goals,    │  Shared goals,    │
                │  full information │  hidden state     │
                │                   │                   │
                ├───────────────────┼───────────────────┤
                │                   │                   │
       Low      │   BARGAINING      │    BARGAINING     │
       CIA      │   (transparent)   │    (opaque)       │
                │                   │                   │
                │  Contested goals, │  Contested goals, │
                │  known preferences│  private info     │
                │                   │                   │
                └───────────────────┴───────────────────┘
```

Each quadrant poses a qualitatively different challenge:

| Quadrant | Challenge | Failure Mode |
|----------|-----------|--------------|
| High CIA, Low Opacity | Pure coordination—find compatible strategies | Convention mismatch |
| High CIA, High Opacity | Coordinate under uncertainty | Misreading partner state/intent |
| Low CIA, Low Opacity | Negotiate fair division with known preferences | Strategic holdout, inefficient conflict |
| Low CIA, High Opacity | Negotiate under asymmetric/private information | Exploitation, signaling failures, adverse selection |

## Why This Framework

Most multi-agent evaluations implicitly fix a point in this space and report performance. This makes it difficult to determine:

- Whether an agent that succeeds at coordination can also handle contested incentives
- Whether an agent that handles full information degrades gracefully under opacity
- Whether strong self-play performance reflects robust cooperation or overfitted conventions

**This framework differs from standard benchmarks by:**

1. **Explicit axis variation**: Environments are designed or selected to span the CIA × Opacity space, not sampled arbitrarily.
2. **Controlled sweeps**: Performance is measured across axis levels, revealing degradation patterns rather than point estimates.
3. **Cross-play as default**: Partner generalization is a primary metric, not an afterthought.
4. **Separation of concerns**: Distinguishes "can't coordinate" from "won't cooperate" from "only works with familiar partners."

## Meta-Game Evaluation

Standard evaluation pairs agents with themselves (self-play) or a narrow set of partners. This rewards strategies that exploit specific conventions and punishes strategies that are robust but less specialized.

This framework adopts a **meta-game perspective**:

1. Construct a diverse **policy library** for each setting (learned policies, heuristics, and where appropriate, LLM-based agents).
2. Evaluate via **cross-play**: each agent is paired against many partners from the library.
3. Measure not just average performance, but **partner-dependent variance**—how stable is an agent's behavior across the space of possible partners?

This approach surfaces the difference between agents that cooperate robustly and agents that merely coordinate well with copies of themselves.

## What This Framework Produces

A **CIA × Opacity benchmark map** that:

- Organizes multi-agent environments by incentive structure and information difficulty
- Identifies which agent architectures succeed in which regimes
- Reveals how performance degrades across axis sweeps
- Tests whether cooperative capabilities generalize across partners and environment variants

## Status

This project is in early development. The evaluation protocol, environment selection, and axis quantification methods are under active design.
