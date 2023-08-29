---
layout: publication
title: "Unsupervised Learning of Robust Spectral Shape Matching"
authors: [dongc, me, fb]
date: 2023-07-05 12:00:00 +0800
pin: false
math: true
mermaid: false
venue: SIGGRAPH 2023 (TOG)
image:
  path: /assets/img/publications/urssm.png
  alt: Our Method is Robust in a Broad Range of Challenging Scenarios
arxiv: https://arxiv.org/abs/2304.14419
pdf: https://dl.acm.org/doi/10.1145/3592107
github: https://github.com/dongliangcao/Unsupervised-Learning-of-Robust-Spectral-Shape-Matching
youtube: https://www.youtube.com/watch?v=Gt-wvLPceRc&t=4s
---

## Abstract

> We consider the problem of finding a continuous and non-rigid matching between a 2D contour and a 3D mesh. While such problems can be solved to global optimality by finding a shortest path in the product graph between both shapes, existing solutions heavily rely on unrealistic prior assumptions to avoid degenerate solutions (e.g. knowledge to which region of the 3D shape each point of the 2D contour is matched). To address this, we propose a novel 2D-3D shape matching formalism based on the conjugate product graph between the 2D contour and the 3D shape. Doing so allows us for the first time to consider higher-order costs, i.e. defined for edge chains, as opposed to costs defined for single edges. This offers substantially more flexibility, which we utilise to incorporate a local rigidity prior. By doing so, we effectively circumvent degenerate solutions and thereby obtain smoother and more realistic matchings, even when using only a one-dimensional feature descriptor. Overall, our method finds globally optimal and continuous 2D-3D matchings, has the same asymptotic complexity as previous solutions, produces state-of-the-art results for shape matching and is even capable of matching partial shapes.  

## Video

{% include embed/youtube.html id='Gt-wvLPceRc' %}

## All Qualitative Results

Visit our <a href="https://github.com/dongliangcao/urssm">project page</a> to view all qualitative results!

## Bibtex
```bibtex
@article{cao2023unsupervised,
  title={Unsupervised Learning of Robust Spectral Shape Matching}, 
  author={Dongliang Cao and Paul Roetzer and Florian Bernard},
  journal = {ACM Transactions on Graphics (TOG)},
  year = {2023},
  publisher = {ACM New York, NY, USA},
  doi = {10.1145/3592107},
  url = {https://doi.org/10.1145/3592107}
}
```

