# Reinforcement Learning for Coverage Path Planning

I investigated whether reinforcement-learning policies could learn efficient area coverage when given information about where an agent had already traveled. The original motivation was cooperative search and coverage by multiple UAVs. 

**Outcome:** the policies did not achieve satisfactory coverage. The experience highlighted the difficulty of specifying useful observations and rewards for a long-horizon exploration task. This repository documents the attempted approaches and their limitations.

## What I explored

- **Coverage history as an observation:** discretizing the search region and adding visited-cell counts or trajectory history to the agent's state.
- **Exploration rewards:** testing new-cell bonuses, revisit penalties, and cumulative-coverage terms.
- **Path-based visitation estimates:** approximating cells traversed between successive reported positions, rather than counting only endpoints.
- **Representation size:** exploring an autoencoder to compress a high-dimensional position-and-visit representation.

See [Methods and historical variants](docs/METHODS_AND_VARIANTS.md), and [Findings and limitations](docs/FINDINGS_AND_LIMITATIONS.md) for what remains unverified.

## Scope and interpretation

The historical workspace combined publicly available MADDPG/PyTorch and Multi-Agent Particle Environment (MPE) implementations with local experimental modifications. Its recovered coverage scenario created **one agent**. A separate three-agent scenario existed, but had a standard distance-based reward.

The conceptual investigation was motivated by multi-agent actor–critic methods.

## What is in this repository

This is a **documentation-only, permission-conscious archival release**:

- **Included:** a historical methods summary, observed limitations, source provenance, and attribution/redistribution notes.
- **Not included:** historical learner or training code, modified scenario files, third-party repositories, model checkpoints, virtual environments, figures of uncertain origin, or reconstructed performance results.
- **Not provided:** working installation, training, evaluation, or reproduction commands. 

## Takeaways

My main takeaway was that choosing an algorithm such as MADDPG is not enough: the observations must communicate the coverage objective, the reward must incentivize efficient *global* rather than merely local exploration, and a larger history vector can complicate training. These were **hypotheses and lessons from an inconclusive study**, not confirmed causal explanations for the performance observed.

## Credit and provenance

The historical experiments used or compared existing implementations from:

- [Philip Tabor — Multi-Agent Deep Deterministic Policy Gradients](https://github.com/philtabor/Multi-Agent-Deep-Deterministic-Policy-Gradients) — historical learner/training scaffold; **no code from this project is redistributed here**.
- [OpenAI — Multi-Agent Particle Environments](https://github.com/openai/multiagent-particle-envs) — MIT-licensed particle environment used as a starting point.
- [Shariq Iqbal — MADDPG-PyTorch](https://github.com/shariqiqbal2810/maddpg-pytorch) — an additional MIT-licensed implementation present in the historical workspace.

See [Provenance](docs/PROVENANCE.md) and [Third-party notices](THIRD_PARTY_NOTICES.md). This release describes historical files; it does not assert that all modifications can be attributed to one person solely from archive metadata.
