# Jenna Wang

Graduate student in Shanghai working on **audio-visual foundation models**. I build
small, open-source tools for the recurring problems in audio-visual learning —
aligning the two modalities, measuring how they line up in time, and handing what
the encoders see and hear to a language model.

A common thread runs through everything below: the numerical core is **pure NumPy**,
so each library installs in seconds, has no GPU or model-download requirement, and is
**fully tested offline by default**. The heavy machinery — PyTorch encoders, media
I/O, hosted LLMs — always lives behind an optional extra, never in the critical path.

---

## Research interests

- **Self-supervised audio-visual representation learning** — contrastive objectives,
  cross-modal retrieval, alignment diagnostics
- **Audio-visual synchronization** — lip-sync offset estimation and active-speaker
  detection from cross-modal correspondence
- **Audio-visual large language models** — the bridge from encoder features to the
  tokens an LLM can read, for video captioning, summarization, and QA

---

## Featured projects

These are the libraries I maintain — each a focused piece of the audio-visual pipeline,
from representation to synchronization to language.

| Project | What it does |
|---------|--------------|
| [**avalign**](https://github.com/stella-sage553/avalign) | Contrastive audio-visual alignment toolkit. CLIP-style **symmetric InfoNCE** over a NumPy core: log-mel spectrograms, SpecAugment, retrieval metrics (recall@k, MRR, median rank) and alignment diagnostics — with optional PyTorch encoders, model, and trainer. |
| [**syncscope**](https://github.com/stella-sage553/syncscope) | Audio-visual **synchronization and active-speaker detection**. Cross-correlates audio energy against visual motion: the peak gives the lip-sync offset, and the same correlation in sliding windows tells you *which* face is speaking. |
| [**avlex**](https://github.com/stella-sage553/avlex) | A composable framework that **bridges audio-visual encoders to LLMs** for video captioning and understanding. Splits encode → fuse → bridge → prompt → generate into swappable parts (token bridge, linear projector, Perceiver resampler, Q-Former), runnable end-to-end offline. |

---

## How these fit together

```
        avalign                 syncscope                  avlex
  learn aligned A/V    ▶   measure temporal      ▶   turn encoder features
   representations          correspondence            into language
 (InfoNCE, retrieval)   (offset, active speaker)   (bridge → prompt → LLM)
```

Each project is deliberately small and composable, with a typed public API, a CLI,
synthetic data generators for tests and demos, and CI on every push.

---

## Tech stack

![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?logo=numpy&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?logo=pytorch&logoColor=white)
![librosa](https://img.shields.io/badge/librosa-4D02A2)
![OpenCV](https://img.shields.io/badge/OpenCV-5C3EE8?logo=opencv&logoColor=white)
![pytest](https://img.shields.io/badge/pytest-0A9EDC?logo=pytest&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?logo=githubactions&logoColor=white)
![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)

---

## Principles

- **Offline by default.** If a `pip install` can't run it on a laptop with no network,
  the abstraction is in the wrong place.
- **Reproducible.** Seeded synthetic generators, deterministic preprocessing, and tests
  that don't depend on downloaded weights or media.
- **Composable over monolithic.** Encoder, fusion, bridge, loss, and metrics are separate
  pieces you can swap and test in isolation — not one hard-wired model class.
