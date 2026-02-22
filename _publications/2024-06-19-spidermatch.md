---
layout: publication
title: "SpiderMatch: 3D Shape Matching with Global Optimality and Geometric Consistency"
authors: [me, fb]
date: 2024-06-01 12:00:00 +0800
pin: false
math: true
mermaid: false
image:
  path: /assets/img/publications/spidermatch.png
  alt: Schematic illustration of our method
venue: 🏆 CVPR 2024
github: https://github.com/paul0noah/spider-match
youtube: https://www.youtube.com/watch?v=iEceCKHDbY4
pdf: https://openaccess.thecvf.com/content/CVPR2024/papers/Roetzer_SpiderMatch_3D_Shape_Matching_with_Global_Optimality_and_Geometric_Consistency_CVPR_2024_paper.pdf
supp: https://openaccess.thecvf.com/content/CVPR2024/supplemental/Roetzer_SpiderMatch_3D_Shape_CVPR_2024_supplemental.pdf
poster: /assets/pdf/posters/spidermatch.pdf
---

🏆 This paper was awarded "Best Student Paper Runner-Up" at CVPR 2024 and with that was among the best 0.09% of all papers.

## Abstract

> Finding shortest paths on product spaces is a pop- ular approach to tackle numerous variants of matching problems, including the dynamic time warping method for matching signals, the matching of curves, or the matching of a curve to a 3D shape. While these approaches admit the computation of globally optimal solutions in polynomial time, their natural generalisation to 3D shape matching is widely known to be intractable. In this work we address this issue by proposing a novel path-based formalism for 3D shape matching. More specifically, we consider an al- ternative shape discretisation in which one of the 3D shapes (the source shape) is represented as a SpiderCurve, i.e. a long self-intersecting curve that traces the 3D shape sur- face. We then tackle the 3D shape matching problem as finding a shortest path in the product graph of the Spider- Curve and the target 3D shape. Our approach introduces a set of novel constraints that ensure a globally geometri- cally consistent matching. Overall, our formalism leads to an integer linear programming problem for which we ex- perimentally show that it can efficiently be solved to global optimality. We demonstrate that our approach is compet- itive with recent state-of-the-art shape matching methods, while in addition guaranteeing geometric consistency.

## Video
{% include embed/youtube.html id='iEceCKHDbY4' %}


## Bibtex
```bibtex
@inproceedings{roetzer2024spidermatch,
    author     = {Paul Roetzer and Florian Bernard},
    title     = { SpiderMatch: 3D Shape Matching with Global Optimality and Geometric Consistency },
    booktitle = {IEEE Conference on Computer Vision and Pattern Recognition (CVPR)},
    year     = 2024
}
```
