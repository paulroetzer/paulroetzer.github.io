---
layout: publication
title: "High-Resolution 3D Shape Matching with Global Optimality and Geometric Consistency"
authors: [ne, me, fb]
date: 2025-06-05 12:00:00 +0800
pin: false
math: true
mermaid: false
image:
  path: /assets/img/publications/highres.png
  alt: Schematic illustration of our method
venue: SGP 2025
github: https://github.com/NafieAmrani/SuPa-Match
---

## Abstract

> 3D shape matching plays a fundamental role in applications such as texture transfer and 3D animation. A key requirement for many scenarios is that matchings exhibit geometric consistency, which ensures that matchings preserve neighbourhood relations across shapes. Despite the importance of geometric consistency, few existing methods explicitly address it, and those that do are either local optimisation methods requiring accurate initialisation, or are severely limited in terms of shape resolution, handling shapes with only up to 3,000 triangles. In this work, we present a scalable approach for geometrically consistent 3D shape matching that, for the first time, scales to high-resolution meshes with up to 10,000 triangles. Our method follows a two-stage procedure: (i) we compute a globally optimal and geometrically consistent mapping of surface patches on the source shape to the target shape via a novel integer linear programming formulation. (ii) we find geometrically consistent matchings of corresponding surface patches which respect correspondences of boundaries of patches obtained from stage (i). With this, we obtain dense, smooth, and guaranteed geometrically consistent correspondences between high-resolution shapes. Empirical evaluations demonstrate that our method is scalable and produces high-quality, geometrically consistent correspondences across a wide range of challenging shapes. We will make our code public upon acceptance.


## Bibtex
```bibtex
@inproceedings{amrani2025highres,
    author    = {Nafie El Amrani and Paul Roetzer and Florian Bernard},
    title     = {High-Resolution 3D Shape Matching with Global Optimality and Geometric Consistency},
    booktitle = {SGP},
    year      = 2025
}
```
