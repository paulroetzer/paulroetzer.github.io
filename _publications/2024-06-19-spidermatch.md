---
layout: publication
title: SpiderMatch: 3D Shape Matching with Global Optimality and Geometric Consistency
authors: [me, fb]
date: 2024-05-01 12:00:00 +0800
pin: false
math: true
mermaid: false
venue: CVPR 2024
github: https://github.com/paul0noah/spider-match
---

## Abstract

> Finding shortest paths on product spaces is a pop- ular approach to tackle numerous variants of matching problems, including the dynamic time warping method for matching signals, the matching of curves, or the matching of a curve to a 3D shape. While these approaches admit the computation of globally optimal solutions in polynomial time, their natural generalisation to 3D shape matching is widely known to be intractable. In this work we address this issue by proposing a novel path-based formalism for 3D shape matching. More specifically, we consider an al- ternative shape discretisation in which one of the 3D shapes (the source shape) is represented as a SpiderCurve, i.e. a long self-intersecting curve that traces the 3D shape sur- face. We then tackle the 3D shape matching problem as finding a shortest path in the product graph of the Spider- Curve and the target 3D shape. Our approach introduces a set of novel constraints that ensure a globally geometri- cally consistent matching. Overall, our formalism leads to an integer linear programming problem for which we ex- perimentally show that it can efficiently be solved to global optimality. We demonstrate that our approach is compet- itive with recent state-of-the-art shape matching methods, while in addition guaranteeing geometric consistency.

## Video
Will follow soon 🚧

## Bibtex
```bibtex
@inproceedings{roetzer2024spidermatch,
    author     = {Paul Roetzer and Florian Bernard},
    title     = { SpiderMatch: 3D Shape Matching with Global Optimality and Geometric Consistency },
    booktitle = {IEEE Conference on Computer Vision and Pattern Recognition (CVPR)},
    year     = 2024,
}
```
