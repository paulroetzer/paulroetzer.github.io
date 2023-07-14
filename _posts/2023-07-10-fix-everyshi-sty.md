---
title: Fix \@EveryShipout@AtNextHook Error
author: Paul Roetzer
date: 2023-07-10 11:33:00 +0800
categories: [Blog, Latex]
tags: [latex]
pin: false
math: false
mermaid: false
---

# Fix everyshi.sty not Working for Conference Latex Templates

⚠️ For a recent ICCV paper (as well as previous CVPR papers) we encountered the following error
```latex
LaTeX Error: Command \@EveryShipout@AtNextHook already defined.
```

✨ This is some bug in the conference templates which appears when using `pgfplot` package and can be fixed by adding the following lines *before* importing pgfplots:
```latex
% fix for everyshi.sty not working with tikz for diverse conference templates:
\makeatletter
\@namedef{ver@everyshi.sty}{}
\makeatother
\usepackage{pgfplots} % pgfplots import MUST come after the above three lines and not before
```
