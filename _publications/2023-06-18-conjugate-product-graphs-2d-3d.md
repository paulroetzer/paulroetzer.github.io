---
layout: publication
title: "Conjugate Product Graphs for Globally Optimal 2D-3D Shape Matching"
authors: [me, zl, fb]
date: 2023-06-18 12:00:00 +0800
pin: false
math: false
mermaid: false
image:
  path: /assets/img/publications/conjprodgraphs.jpg
  alt: Ours vs Lähner et al.
venue: CVPR 2023
arxiv: https://arxiv.org/abs/2211.11589
github: https://github.com/paul0noah/sm-2D3D
youtube: https://www.youtube.com/watch?v=qr_-n8NHWC4
pdf: https://openaccess.thecvf.com/content/CVPR2023/papers/Roetzer_Conjugate_Product_Graphs_for_Globally_Optimal_2D-3D_Shape_Matching_CVPR_2023_paper.pdf
---

## Abstract

> We consider the problem of finding a continuous and non-rigid matching between a 2D contour and a 3D mesh. While such problems can be solved to global optimality by finding a shortest path in the product graph between both shapes, existing solutions heavily rely on unrealistic prior assumptions to avoid degenerate solutions (e.g. knowledge to which region of the 3D shape each point of the 2D contour is matched). To address this, we propose a novel 2D-3D shape matching formalism based on the conjugate product graph between the 2D contour and the 3D shape. Doing so allows us for the first time to consider higher-order costs, i.e. defined for edge chains, as opposed to costs defined for single edges. This offers substantially more flexibility, which we utilise to incorporate a local rigidity prior. By doing so, we effectively circumvent degenerate solutions and thereby obtain smoother and more realistic matchings, even when using only a one-dimensional feature descriptor. Overall, our method finds globally optimal and continuous 2D-3D matchings, has the same asymptotic complexity as previous solutions, produces state-of-the-art results for shape matching and is even capable of matching partial shapes.  

## Video

{% include embed/youtube.html id='qr_-n8NHWC4' %}

## Poster
 <object data="/assets/pdf/posters/conjugate2d3d.pdf#toolbar=0&navpanes=0&pagemode=none" type="application/pdf"
 type="application/pdf" style="min-height:40vh;width:100%">
<p>Unable to display PDF file. <a href="/assets/pdf/posters/conjugate2d3d.pdf">Download</a> instead.</p>
</object>


## Bibtex
```bibtex
@inproceedings{roetzer2023conjugate,
    author     = {Paul Roetzer and Zorah L\"ahner and Florian Bernard},
    title     = { Conjugate Product Graphs for Globally Optimal 2D-3D Shape Matching },
    booktitle = {IEEE Conference on Computer Vision and Pattern Recognition (CVPR)},
    year     = 2023,
}
```
