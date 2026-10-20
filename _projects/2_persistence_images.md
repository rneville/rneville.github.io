---
layout: page
title: Persistence images
description: A stable vector representation that makes topological features usable in standard machine-learning pipelines. 1,400+ citations.
img: assets/img/projects/LT4-2_PI50_bump.png
importance: 1
github: https://github.com/CSU-TDA/PersistenceImages
---

**Paper:** [Persistence Images: A Stable Vector Representation of Persistent Homology](https://jmlr.org/papers/v18/16-337.html), _Journal of Machine Learning Research_ 18(8):1–35 (2017). **Cited 1,400+ times** (Google Scholar).

**Code:** [github.com/CSU-TDA/PersistenceImages](https://github.com/CSU-TDA/PersistenceImages) (MATLAB, released with the paper)

**Adopted by the community:** Python implementation in [scikit-tda / persim](https://persim.scikit-tda.org/en/latest/notebooks/Persistence%20images.html), with related implementations in GUDHI and R's TDA ecosystem

<div class="row justify-content-center">
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/LT4-2_PI50_bump.png" title="A persistence image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    A 50×50 persistence image of the dimension-1 persistent homology (loops) of data from the linked twist map, a discrete-time dynamical system, at parameter value 4.2. The topological summary becomes a fixed-size grid that can be fed directly into a machine-learning model.
</div>

### The problem

Persistent homology is a tool from topological data analysis that gives a multiscale summary of the shape of a data set, such as its clusters, loops, and voids, and which of them persist across scales. Its standard output, the persistence diagram, is a set of points of varying size. That makes it awkward to use with most machine-learning methods, which expect fixed-length feature vectors.

### Approach

We introduced the **persistence image**, a way to turn a persistence diagram into a finite-dimensional vector:

- Each point in the diagram is replaced by a weighted Gaussian, giving a smooth surface.
- That surface is integrated over a pixel grid to produce an image, which flattens to a vector of fixed length.
- We proved the transformation is **stable**: small perturbations in the input data produce only small changes in the persistence image.

### Results

- Compared with existing topological representations, persistence images showed significant gains in classification performance.
- Because they are ordinary vectors, persistence images work with standard ML tools. Linear sparse support vector machines, for example, pick out which topological features actually discriminate between classes.
- They enabled high-accuracy inference of parameter values from the output of a discrete dynamical system (the linked twist map) and a partial differential equation (the anisotropic Kuramoto–Sivashinsky equation).

The method has since become a standard part of the topological data analysis toolkit, with implementations in the major open-source libraries.

### Skills and tools

Feature engineering · topological data analysis · machine learning (SVMs, sparse classifiers) · stability proofs · MATLAB · open-source software
