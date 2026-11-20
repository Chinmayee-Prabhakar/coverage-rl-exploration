# Provenance and authorship boundaries

## Basis of this release

A read-only audit compared two local historical source folders against known upstream repositories and inspected their environment, learner, media, and checkpoints. The historical source folders did not contain `.git` metadata. The comparison established **file lineage**, not who personally made each change.

No historical source code is included in this public-release candidate. This page records the relevant external references and the reasons source files were withheld.

| Source | Pinned comparison revision | Historical relationship | Redistribution decision |
| --- | --- | --- | --- |
| [Philip Tabor — MADDPG](https://github.com/philtabor/Multi-Agent-Deep-Deterministic-Policy-Gradients) | [`a3c294aa6834f348a7401306dff3e67919c861f5`](https://github.com/philtabor/Multi-Agent-Deep-Deterministic-Policy-Gradients/tree/a3c294aa6834f348a7401306dff3e67919c861f5) | Main actor/critic, replay buffer, and training scaffold in the recovered workspace largely copied or adapted from this repository | **Exclude all source and modified derivatives:** no explicit license grant was identified in the audited source history |
| [OpenAI — Multi-Agent Particle Environments](https://github.com/openai/multiagent-particle-envs) | [`83ba4d1aeb00282f7c4acd6912435b3ca642c227`](https://github.com/openai/multiagent-particle-envs/tree/83ba4d1aeb00282f7c4acd6912435b3ca642c227) | Original 2D simulator, standard scenarios, and adapted custom scenarios | MIT-license reuse may be possible with the required notice, but **no source is bundled here** |
| [Shariq Iqbal — MADDPG-PyTorch](https://github.com/shariqiqbal2810/maddpg-pytorch) | [`40388d7c18e4662cf23c826d97e209df9003d86c`](https://github.com/shariqiqbal2810/maddpg-pytorch/tree/40388d7c18e4662cf23c826d97e209df9003d86c) | Separate copied implementation inside the archive, including nine identical upstream demonstration GIFs | Exclude code and media; cite as an historical reference only |
| [OpenAI — MADDPG](https://github.com/openai/maddpg) | [`3ceefa0ada3ff31d633dd0bde8ff95213ce99be3`](https://github.com/openai/maddpg/tree/3ceefa0ada3ff31d633dd0bde8ff95213ce99be3) | Original algorithm reference; direct file-level derivation **not established** by the audit | Reference only; no code distributed |

## Historical local additions identified by the audit

These source modifications are important to the project narrative, but archive metadata does not independently authenticate personal authorship or full rights:

- A discretized visitation-history observation, new-cell and revisit rewards, and one historical coverage training scaffold.
- Interpolated path-based visitation accounting and cumulative coverage summaries.
- Modified particle-environment observations/step return values, plus scenario variants.
- Autoencoder experiments for compressing coverage-history representations.

Some additions were interleaved with an unlicensed third-party training scaffold. Neither copying the full mixed file nor cosmetically extracting its code would resolve that issue. This release therefore describes concepts and measured limitations **without shipping any source from those scripts**.

## Attribution limits

- The audit found no `.git` directory in either archive; it cannot establish a personal commit history or a complete author-by-author ownership record.
- Source similarity identifies relationships to inspected upstream snapshots, not proof that a particular person downloaded or authored a file.
- File dates and archived ZIP snapshots do not establish authenticated development dates.
- This repository's narrative documents the project as reported by its researcher and checked against source evidence; it does not present file metadata as proof of sole software authorship.
- University/course/collaborator agreements were not independently reviewed. The release **contains no historical source or experimental data**, reducing the redistribution risk, but does not purport to be a legal opinion.

## What was excluded

Full learner and environment source trees; adapted training scripts (including mixed-origin derivatives); autoencoder scripts of uncertain provenance; third-party GIFs and unrelated graphics; saved model/optimizer artifacts; CSV outputs lacking reproducible configurations; bundled Python environments and caches; personal system paths and archived ZIP backups.

For methods and experimental limitations, see [Methods and historical variants](METHODS_AND_VARIANTS.md) and [Findings and limitations](FINDINGS_AND_LIMITATIONS.md).
