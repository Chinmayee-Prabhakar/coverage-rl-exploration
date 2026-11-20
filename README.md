# Reinforcement Learning for Coverage: An Exploratory Study

**Graduate research exploration · 2023–2024 · Status: incomplete / inconclusive**

I investigated whether reinforcement-learning policies could learn efficient area coverage when given information about where an agent had already traveled. The original motivation was cooperative search and coverage by multiple UAVs. The recovered experiments, however, primarily implemented **single-agent coverage in a two-dimensional particle environment**, not a demonstrated multi-UAV coverage system.

**Outcome:** the policies did **not** achieve satisfactory coverage. The experience highlighted the difficulty of specifying useful observations and rewards for a long-horizon exploration task. This repository documents the attempted approaches and their limitations rather than presenting an unverified success.

## What I explored

- **Coverage history as an observation:** discretizing the search region and adding visited-cell counts or trajectory history to the agent's state.
- **Exploration rewards:** testing new-cell bonuses, revisit penalties, and cumulative-coverage terms.
- **Path-based visitation estimates:** approximating cells traversed between successive reported positions, rather than counting only endpoints.
- **Representation size:** exploring an autoencoder to compress a high-dimensional position-and-visit representation.

See [Methods and historical variants](docs/METHODS_AND_VARIANTS.md) for what is supported by the recovered archives, and [Findings and limitations](docs/FINDINGS_AND_LIMITATIONS.md) for what remains unverified.

## Scope and interpretation

The historical workspace combined publicly available MADDPG/PyTorch and Multi-Agent Particle Environment (MPE) implementations with local experimental modifications. Its recovered coverage scenario created **one agent**. A separate three-agent scenario existed, but had a standard distance-based reward; it is **not evidence of cooperative coverage training**. The archive does not support claims of a new MADDPG algorithm, real UAV dynamics, successful coordinated search, or a measured performance improvement.

The conceptual investigation was motivated by multi-agent actor–critic methods, but the methods and observations discussed here should not be interpreted as a successful multi-agent RL demonstration.

## What is—and is not—in this repository

This is a **documentation-only, permission-conscious archival release**:

- **Included:** a historical methods summary, observed limitations, source provenance, and attribution/redistribution notes.
- **Not included:** historical learner or training code, modified scenario files, copied third-party repositories, model checkpoints, virtual environments, figures of uncertain origin, or fabricated/reconstructed performance results.
- **Not provided:** working installation, training, evaluation, or reproduction commands. Nothing here is claimed to reproduce the original experimental run.

That omission is deliberate. The main historical learner was derived from a third-party repository with **no explicit redistribution license located in the inspected history**. The original archives also have unresolved file-level authorship for several local additions, and their checkpoint/run configurations cannot be reliably reconstructed. Rather than redistribute uncertain code or silently rewrite the project, I am documenting its research trajectory faithfully.

## Takeaways

My main takeaway was that choosing an algorithm such as MADDPG is not enough: the observations must communicate the coverage objective, the reward must incentivize efficient *global* rather than merely local exploration, and a larger history vector can complicate training. These were **hypotheses and lessons from an inconclusive study**, not confirmed causal explanations for the performance observed.

## Credit and provenance

The historical experiments used or compared existing implementations from:

- [Philip Tabor — Multi-Agent Deep Deterministic Policy Gradients](https://github.com/philtabor/Multi-Agent-Deep-Deterministic-Policy-Gradients) — historical learner/training scaffold; **no code from this project is redistributed here**.
- [OpenAI — Multi-Agent Particle Environments](https://github.com/openai/multiagent-particle-envs) — MIT-licensed particle environment used as a starting point.
- [Shariq Iqbal — MADDPG-PyTorch](https://github.com/shariqiqbal2810/maddpg-pytorch) — an additional MIT-licensed implementation present in the historical workspace; its media are not presented as my results.

See [Provenance](docs/PROVENANCE.md) and [Third-party notices](THIRD_PARTY_NOTICES.md). This release describes historical files; it does not assert that all modifications can be attributed to one person solely from archive metadata.

## Project status

**Archival; no further development planned for this release.** The goal is to record an authentic exploratory research experience, including the unsuccessful outcome, rather than complete an algorithm or offer a production-ready package.
