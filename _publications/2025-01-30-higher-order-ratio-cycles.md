---
layout: publication
title: "Higher-Order Ratio Cycles for Fast and Globally Optimal Shape Matching"
authors: [me, ve, dc, zl, fb]
date: 2025-06-10 12:00:00 +0800
pin: false
math: true
mermaid: false
image:
  path: /assets/img/publications/ratiocycles.png
  alt: Schematic illustration of our method
venue: CVPR 2025
github: https://github.com/paul0noah/product-graph-cycles/
pdf: https://openaccess.thecvf.com/content/CVPR2025/papers/Roetzer_Higher-Order_Ratio_Cycles_for_Fast_and_Globally_Optimal_Shape_Matching_CVPR_2025_paper.pdf
---

## Abstract

> In this work we address various shape matching problems that can be cast as finding cyclic paths in a product graph. This involves for example 2D-3D shape matching, 3D shape matching, or the matching of a contour to a graph. In this context, matchings are typically obtained as the minimum cost cycle in the product graph. Instead, inspired by related works on model-based image segmentation, we consider minimum ratio cycles, which we combine with the recently introduced conjugate product graph in order to allow for higher-order matching costs. With that, on the one hand we avoid the bias of obtaining matchings that involve fewer/shorter edges, while on the other hand being able to impose powerful geometric regularisation, e.g. to avoid zig-zagging. In our experiments we demonstrate that this not only leads to improved matching accuracy in most cases, but also to significantly reduced runtimes (up to two orders of magnitude, depending on the setting).

Also check out the [appendix](https://openaccess.thecvf.com/content/CVPR2025/supplemental/Roetzer_Higher-Order_Ratio_Cycles_CVPR_2025_supplemental.pdf)!

## Bibtex
```bibtex
@inproceedings{roetzer2025higherorder,
    author    = {Paul Roetzer and Viktoria Ehm and Daniel Cremers and and Zorah L\"ahner and Florian Bernard},
    title     = {Higher-Order Ratio Cycles for Fast and Globally Optimal Shape Matching},
    booktitle = {CVPR},
    year      = 2025
}
```
