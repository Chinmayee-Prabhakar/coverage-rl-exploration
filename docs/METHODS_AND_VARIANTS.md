# Methods and historical variants

This document summarizes **observed implementation features** in the historical code archive. It is not a specification of an executable program included in this repository, nor a claim that every variant was jointly integrated and evaluated.

## Problem motivation

The starting question was whether an actor–critic policy could adapt exploration decisions using the history of locations visited in a search region. The original ambition involved cooperative UAV coverage. The recovered implementations used a two-dimensional particle simulator; the coverage scenario was **single-agent**. There was no recovered flight dynamics, sensing footprint, search-target detection, communications model, or demonstrated multi-agent coverage policy.

## Environment and observations

A coverage-oriented scenario in the recovered workspace extends a simple OpenAI MPE scenario. The local environment adaptation exposed agent positions to the training caller as an additional return value, departing from the upstream four-element step contract.

Historical scripts used multiple incompatible observation representations:

| Variant | What the archive supports | Evidence in original audit |
| --- | --- | --- |
| Visitation-count map | A discretized **52 × 52 = 2,704-cell** history attached to a six-component base observation, yielding 2,710 features | `main - large.py`, lines 59–70 and 108–146; custom scenario, lines 111–135 |
| Coordinate history | A history of visited positions appended to an observation | `main - Copy (2).py`, lines 101–117 |
| Cumulative coverage | Explicit running coverage percentage calculated from visited cells | `Miscellaneous/Current.py`, lines 249–263 |
| Latent representation | Separate encoder experiments on flattened coordinate/count triples; not demonstrated to improve RL | `autoencoder_online.py`, lines 18–83 and 114–196 |

The variants were not consistently interoperable. Some history features were replaced or digitized by the training loop, and some scenario features were left as placeholders. This is one of the obstacles to reproducing the old experiments from their archived files.

## Coverage accounting and rewards

The recovered scripts contain multiple experiments, not one canonical reward:

- **First-visit bonus and revisits:** one variant assigned **+2** for a newly visited in-bounds cell and penalized repeat visits based on their accumulated count (`main - Copy (2).py`, lines 123–133).
- **Revisit-weighted penalty:** another variant used **−2 × visit count** (`main - large.py`, lines 150–160).
- **New coverage plus cumulative term:** a further variant assigned **+6** for a new interpolated cell and **+2 × cumulative coverage percentage** each step; its revisit penalty was commented out (`Miscellaneous/Current.py`, lines 215–228).
- **Traversal approximation:** the same experiment sampled **five points** between successive positions, mapped them to bins, removed duplicates, and updated history. The active routine was linear interpolation, not exact traversed-cell enumeration (`Miscellaneous/Current.py`, lines 63–67 and 182–231).

These choices are reported as *attempts*, not as verified improvements. In particular, adding cumulative coverage to every step can reward lingering after early exploration; sparse interpolation can miss traversed cells, and boundaries/overflow bins were not consistently defined.

## Autoencoder exploration

A separate encoder compressed **8,112 input dimensions to 50** using intermediate layers (8,112 → 4,000 → 1,000 → 500 → 50), with decoder-based reconstruction checks. The recovered training variant does **not** establish a fully integrated policy operating on the learned latent coverage map. Reconstruction error is not equivalent to coverage-policy performance.

## Algorithm context

The workspace included a MADDPG-style learner derived from Philip Tabor's tutorial, OpenAI MPE environment code, and a separate Shariq Iqbal implementation. The standard centralized-critic/decentralized-actor concept came from established MADDPG research, not an original algorithm developed in this project. The recovered three-agent example was **not** a cooperative coverage result.

## Source boundaries

All path/line references in this document identify files in the **private historical archives** from the read-only audit; those files are not redistributed in this repository. The source archive lacked `.git` metadata, so its personal code authorship and the exact development sequence cannot be established from Git history. See [Provenance](PROVENANCE.md).
