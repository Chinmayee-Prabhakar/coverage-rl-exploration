# Findings and limitations

## Outcome

The exploration did **not** yield satisfactory area coverage. The original research objective was ambitious—cooperative learned coverage—but the actual recovered coverage task was single-agent and no trustworthy success or improvement claim can be reconstructed from the archive.

Two plausible problems motivated the investigation:

1. Local first-visit bonuses and cumulative coverage terms might not encourage globally efficient search or avoid repeated visits.
2. Dense visitation histories could increase the observation and replay-memory burden, making learning difficult.

Those remain **possible explanations**, not conclusions verified by controlled comparisons. The available materials do not establish which mechanism caused the unsuccessful result.

## What the read-only technical audit established

The following describe **audited historical code**, not code shipped or executed by this archival repository.

| Area | Audit observation | What it prevents us from claiming |
| --- | --- | --- |
| Coverage task | Recovered coverage environment instantiated one particle agent | Working multi-agent cooperation or UAV search |
| Actor–critic updates | A three-agent synthetic update failed with an in-place PyTorch autograd error | Reliable multi-agent MADDPG training |
| Memory budget | At one million transitions the 2,710-feature float64 replay configuration was estimated to need about **80.8 GiB**, before training overhead | Practical large-scale training at the recorded settings |
| Policies/checkpoints | Saved network shapes did not match the current historical training architecture and observations | Reliable replay of a trained coverage policy |
| Evaluation | Action noise was not consistently disabled and no held-out multi-seed evaluation was recovered | Quantitative policy improvements or reproducibility |
| Environment interface | The modified step returned an extra position field, while some callers still expected four values | A single stable runnable interface |
| Autoencoder | The encoder was evaluated for reconstruction, not a proven closed-loop policy benefit | Demonstrated latent-map performance improvement |

The archived materials contain no documented head-to-head evaluation that would establish superiority over random walk, systematic sweep, or frontier-based coverage. Images and GIFs found in the source workspace could not be confidently linked to the resulting local policies; inherited demonstration GIFs were identical to upstream files.

## Reproducibility statement

The historical code requires cleanup, dependency resolution, compatible checkpoints, stable environment semantics, and independent evaluation before it can be considered reproducible. This repository intentionally does not present historical code, checkpoints, graphs, or commands as if those issues had been fixed.

## What the experience taught me

The value of the project was in learning to think about state representation and objective design: learning-based control is not automatically effective when the task specification does not make long-term behavior learnable. The inconclusive outcome helped clarify why method selection, reward shaping, memory costs, and credible evaluation all matter.

This is a reflective archival account, not a formal causal finding or a claim of new MADDPG methodology.
