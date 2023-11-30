---
title: Mean Curvature Flow in Python
author: me
date: 2023-11-10 11:33:00 +0800
categories: [Blog, Python]
tags: [python]
pin: false
math: false
mermaid: false
---

# Mean Curvature Flow in Python

This post contains the port of this [matlab implementation](https://www.alecjacobson.com/weblog/?tag=mean-curvature-flow) of mean curvature to python.

With mean curvature flow we can map a genus 0 shape to a sphere:

![Desktop View](/assets/img/posts/meancurvflow/meancurvflow_0.png){: width="200" style="margin-left:auto; margin-right:auto"}

![Desktop View](/assets/img/posts/meancurvflow/meancurvflow_1.png){: width="200" style="margin-left:auto; margin-right:auto"}

![Desktop View](/assets/img/posts/meancurvflow/meancurvflow_2.png){: width="200" style="margin-left:auto; margin-right:auto"}


### ⚙️ Requires Python modules
We need the following python modules which are easily installable through pip.
```
igl
numpy
scipy
# optional, only necessary for debugging
vedo 
```

### 🐍 Python Code

With the following function we can perform mean curvature flow. The code assumes that we have a matrix `v` (`v.shape = (|v|, 3)`) which contains the vertex positions and a matrix `f` (`f.shape = (|f|, 3)`) which contains the triangulation.
The function returns `u` (`u.shape = (|v|, 3)`) which contains the new vertex positions of the mesh.

```python
import igl
from scipy.sparse.linalg import spsolve
def mean_curv_flow(v, f, max_iter=100, delta=10):
    debug = False # set to True for visualising intermediate steps
    dense = False # set to True to enable computation with dense matrices
    if debug:
        import vedo
        plt = vedo.Plotter(bg=[255, 255, 255])
        mesh = vedo.Mesh((v, f))
        mesh.cmap("hot", mesh.points()[:, 2])
        plt.show(mesh, interactive=False)
        plt.process_events()
    L = igl.cotmatrix(v, f)
    if dense:
        L = L.todense()
    u = v
    i = 0
    while i <= max_iter:
        u_last = u
        M = igl.massmatrix(u, f, igl.MASSMATRIX_TYPE_BARYCENTRIC)
        if dense:
            M = M.todense()
            u = np.linalg.solve(M - delta * L, M @ u)
        else:
            u = spsolve(M - delta * L, M @ u) # with
        u = u / np.sqrt((0.5 * igl.doublearea(u, f)).sum())
        u = u - u.mean(axis=0)
        rel_change = np.linalg.norm(u - u_last) / u.shape[0]

        if rel_change <= 1e-5:
            if debug:
                print('converged')
            break

        i = i + 1
        if debug:
            mesh.points(u)
            plt.show(mesh, interactive=False)

    if debug:
        plt.interactive()
    return u
```
