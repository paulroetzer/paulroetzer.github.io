---
layout: publication
title: Geometrically Consistent Partial Shape Matching
authors: [ve, me, marvin, maolin, fb, dc]
date: 2024-02-27 12:00:00 +0800
pin: false
math: true
mermaid: false
venue: 3DV 2024
image:
  path: /assets/img/publications/partialwindheuser.png
  alt: We find geometrically consistent matchings between a template shape (middle) and partial shapes.
arxiv: https://arxiv.org/pdf/2309.05013.pdf
---

## Abstract

> Finding correspondences between 3D shapes is a crucial problem in computer vision and graphics, which is for example relevant for tasks like shape interpolation, pose transfer, or texture transfer. An often neglected but essential property of matchings is geometric consistency, which means that neighboring triangles in one shape are consistently matched to neighboring triangles in the other shape. Moreover, while in practice one often has only access to partial observations of a 3D shape (e.g. due to occlusion, or scanning artifacts), there do not exist any methods that directly address geometrically consistent partial shape matching. In this work we fill this gap by proposing to integrate state-of-the-art deep shape features into a novel integer linear programming partial shape matching formulation. Our optimization yields a globally optimal solution on low resolution shapes, which we then refine using a coarseto-fine scheme. We show that our method can find more reliable results on partial shapes in comparison to existing geometrically consistent algorithms (for which one first has to fill missing parts with a dummy geometry). Moreover, our matchings are substantially smoother than learning-based state-of-the-art shape matching methods.


## Bibtex
```bibtex
@inproceedings{ehm2024geometric,
    title={Geometrically Consistent Partial Shape Matching},
    author     = {Ehm, Viktoria and Roetzer, Paul and Eisenberger, Marvin and Gao, Maolin and Bernard, Florian and Cremers, Daniel},
    booktitle = {International Conference on 3D Vision (3DV)},
    year     = 2024
}
```
