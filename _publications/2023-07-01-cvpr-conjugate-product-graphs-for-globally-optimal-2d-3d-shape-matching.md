---
title: "Conjugate Product Graphs for Globally Optimal 2D-3D Shape Matching"
author: 'Paul Roetzer, <b>Zorah Lähner</b>, Florian Bernard'
date: 2023-06-17 12:00:00 +0800
categories: [Shapes, Correspondences]
tags: [publication]
pin: true
math: true
mermaid: false
image:
  path: /assets/img/posts/gif_from_plot/torusrot_nobounce.gif
  alt: Animated Plot from Matlab
---

## Abstract

> We consider the problem of finding a continuous and non-rigid matching between a 2D contour and a 3D mesh. While such problems can be solved to global optimality by finding a shortest path in the product graph between both shapes, existing solutions heavily rely on unrealistic prior assumptions to avoid degenerate solutions (e.g. knowledge to which region of the 3D shape each point of the 2D contour is matched). To address this, we propose a novel 2D-3D shape matching formalism based on the conjugate product graph between the 2D contour and the 3D shape. Doing so allows us for the first time to consider higher-order costs, i.e. defined for edge chains, as opposed to costs defined for single edges. This offers substantially more flexibility, which we utilise to incorporate a local rigidity prior. By doing so, we effectively circumvent degenerate solutions and thereby obtain smoother and more realistic matchings, even when using only a one-dimensional feature descriptor. Overall, our method finds globally optimal and continuous 2D-3D matchings, has the same asymptotic complexity as previous solutions, produces state-of-the-art results for shape matching and is even capable of matching partial shapes.  

## Resources



## Bibtex

    @inproceedings{roetzer2023conjugate,
        author     = {Paul Roetzer and Zorah L\"ahner and Florian Bernard},
        title     = { Conjugate Product Graphs for Globally Optimal 2D-3D Shape Matching },
        booktitle = {IEEE Conference on Computer Vision and Pattern Recognition (CVPR)},
        year     = 2023,
    }
