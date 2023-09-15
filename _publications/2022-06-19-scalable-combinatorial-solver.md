---
layout: publication
title: "A Scalable Combinatorial Solver for Elastic Geometrically Consistent 3D Shape Matching"
authors: [me, ps, dc, fb]
date: 2022-06-18 12:00:00 +0800
pin: false
math: true
mermaid: false
image:
  path: /assets/img/publications/smcomb.png
  alt: Our Combinatorial Solver is Faster than Previous Approaches and is Applicable to Partial Shapes
venue: CVPR 2022
arxiv: https://arxiv.org/abs/2204.12805
github: https://github.com/paul0noah/sm-comb
youtube: https://youtu.be/uPwqOXYw1kw
pdf: https://csdl-downloads.ieeecomputer.org/proceedings/cvpr/2022/6946/00/694600a428.pdf?Expires=1688627315&Policy=eyJTdGF0ZW1lbnQiOlt7IlJlc291cmNlIjoiaHR0cHM6Ly9jc2RsLWRvd25sb2Fkcy5pZWVlY29tcHV0ZXIub3JnL3Byb2NlZWRpbmdzL2N2cHIvMjAyMi82OTQ2LzAwLzY5NDYwMGE0MjgucGRmIiwiQ29uZGl0aW9uIjp7IkRhdGVMZXNzVGhhbiI6eyJBV1M6RXBvY2hUaW1lIjoxNjg4NjI3MzE1fX19XX0_&Signature=WvWURJOZUFSYzvW5O-dXrZZkc8vyDNL9erU~5oBSNoAs4FIS~t4VzkuUuvzLBW2yDw0yXRNMeUTSBECK6qLBhmYI45LyRuHcYoSZ-Z-0xhcXuAti-12CVd9iqDWhxiDb6hFpkjgIEv02l1WqIgXkZuTmkT52p0S79OjHct5yZewYHp6jOaQ6-bVUgNet8PtEvB28QOAJLzGdWg4UbRBtEz3AbaWXwnDRiNNq~4CuVqrzUlZ37xyfvyy9FOZ9k86b3H3vWVJG9udTE-wxLDtkXqxtZUYDyPGOwzKAG2cu05VnzD0d5S772Od9eJgXADw4c1hGpA-Dsk2Q1QenfWzaxw__&Key-Pair-Id=K12PMWTCQBDMDT
---

## Abstract

> We present a scalable combinatorial algorithm for globally optimizing over the space of geometrically consistent mappings between 3D shapes. We use the mathematically elegant formalism proposed by Windheuser et al. where 3D shape matching was formulated as an integer linear program over the space of orientation-preserving diffeomorphisms. Until now, the resulting formulation had limited practical applicability due to its complicated constraint structure and its large size. We propose a novel primal heuristic coupled with a Lagrange dual problem that is several orders of magnitudes faster compared to previous solvers. This allows us to handle shapes with substantially more triangles than previously solvable. We demonstrate compelling results on diverse datasets, and, even showcase that we can address the challenging setting of matching two partial shapes without availability of complete shapes.

## Bibtex
```bibtex
@inproceedings{roetzer2022scalable,
  title={A scalable combinatorial solver for elastic geometrically consistent 3d shape matching},
  author={Roetzer, Paul and Swoboda, Paul and Cremers, Daniel and Bernard, Florian},
  booktitle={Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition},
  pages={428--438},
  year={2022}
}
```
