---
layout: publication
title: "DiscoMatch: Fast Discrete Optimisation for Geometrically Consistent 3D Shape Matching"
authors: [me, aa, dc, fb, ps]
date: 2024-09-30 12:00:00 +0800
pin: false
math: true
mermaid: false
image:
  path: /assets/img/publications/discomatch.jpg
  alt: Schematic illustration of our method
venue: ECCV 2024
github: https://github.com/paul0noah/disco-match
pdf: https://www.ecva.net/papers/eccv_2024/papers_ECCV/papers/07026.pdf
arxiv: https://arxiv.org/abs/2310.08230
supp: https://www.ecva.net/papers/eccv_2024/papers_ECCV/papers/07026-supp.pdf
poser: /assets/pdf/posters/discomatch.pdf
---

## Abstract

> In this work we propose to combine the advantages of learning-based and combinatorial formalisms for 3D shape matching. While learning-based methods lead to state-of-the-art matching performance, they do not ensure geometric consistency, so that obtained matchings are locally non-smooth. On the contrary, axiomatic, optimisation-based methods allow to take geometric consistency into account by explicitly constraining the space of valid matchings. However, existing axiomatic formalisms do not scale to practically relevant problem sizes, and require user input for the initialisation of non-convex optimisation problems. We work towards closing this gap by proposing a novel combinatorial solver that combines a unique set of favourable properties: our approach (i) is initialisation free, (ii) is massively parallelisable and powered by a quasi-Newton method, (iii) provides optimality gaps, and (iv) delivers improved match- ing quality with decreased runtime and globally optimal results for many instances.


## Bibtex
```bibtex
@inproceedings{roetzerabbas2024discomatch,
    author     = {Paul Roetzer and Ahmed Abbas and Dongliang Cao and Florian Bernard and Paul Swoboda},
    title     = { DiscoMatch: Fast Discrete Optimisation for Geometrically Consistent 3D Shape Matching },
    booktitle = {In Proceedings of the European conference on computer vision (ECCV)},
    year     = 2024
}
```
