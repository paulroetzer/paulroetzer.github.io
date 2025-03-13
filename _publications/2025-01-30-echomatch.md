---
layout: publication
title: "EchoMatch: Partial-to-Partial Shape Matching via Correspondence Reflection"
authors: [yx, ve, me, mg, ne, fb, dc]
date: 2025-01-30 12:00:00 +0800
pin: false
math: true
mermaid: false
image:
  path: /assets/img/publications/echomatch.png
  alt: Schematic illustration of our method
venue: CVPR 2025
---

## Abstract

> Finding correspondences between 3D shapes is a crucial problem in computer vision and graphics. While most research has focused on finding correspondences in settings where at least one of the shapes is complete, the realm of partial-to-partial shape matching remains under-explored. Yet it is of importance since, in many applications, shapes are only observed partially due to occlusion or scanning. Finding correspondences between partial shapes comes with an additional challenge: We not only want to identify correspondences between points on either shape but also have to determine which points of each shape actually have a partner. To tackle this challenging problem, we present EchoMatch, a novel framework for partial-to-partial shape matching that incorporates the concept of correspondence reflection to enable an overlap prediction within a functional map framework. With this approach, we show that we can outperform current SOTA methods in challenging partial-to-partial shape matching problems.


## Bibtex
```bibtex
@inproceedings{xie2025echomatch,
    author     = {Yizheng Xie and Viktoria Ehm and Paul Roetzer and Nafie El Amrani and Maolin Gaoa and Florian Bernard and Daniel Cremers},
    title     = {EchoMatch: Partial-to-Partial Shape Matching via Correspondence Reflection},
    booktitle = {CVPR},
    year     = 2025
}
```
