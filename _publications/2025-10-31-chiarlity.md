---
layout: publication
title: "Symmetry Informative and Agnostic Feature Disentanglement for 3D Shapes"
authors: [tw, ww, me, ne, fb]
date: 2025-10-30 12:00:00 +0800
pin: false
math: true
mermaid: false
image:
  path: /assets/img/publications/geco.png
  alt: Schematic illustration of our method
venue: 3DV 2026
---

## Abstract

> Shape descriptors, i.e. per-vertex features of 3D meshes or point clouds, are fundamental to shape analysis. Over the past decades, various handcrafted geometry-aware descriptors and feature refinement techniques have been proposed. Recently, several studies have initiated a new research direction by leveraging features from image foundation models to create semantics-aware descriptors, demonstrating advantages across tasks like shape matching, editing, and segmentation. Symmetry, another key concept in shape analysis, has also attracted increasing attention. Consequently, constructing symmetry-aware shape descriptors is a natural progression. Although a recent method successfully extracted symmetry-informative feature from semantic-aware descriptors, its features are only one-dimensional, neglecting other valuable semantic information. Besides, the extracted symmetry-informative feature is usually noisy and yields tiny miss-classified patches. To address these gaps, we propose a feature disentanglement approach which at the same time is symmetry informative and symmetry agnostic. Further, we propose a feature refinement technique to improve robustness of predicted symmetry informative features. Extensive experiments, including intrinsic symmetry detection, left/right classification, and shape matching, demonstrate the effectiveness of our proposed framework compared to various state-of-the-art methods, both qualitatively and quantitatively. We will release our code upon acceptance.


## Bibtex
```bibtex
@inproceedings{weissberg2026symmetry,
    author    = {Tobias Weissberg and Weikang Wang and Paul Roetzer and Nafie El Amnrani and Florian Bernard},
    title     = {Symmetry Informative and Agnostic Feature Disentanglement for 3D Shapes},
    booktitle = {3DV},
    year      = 2026
}
```
