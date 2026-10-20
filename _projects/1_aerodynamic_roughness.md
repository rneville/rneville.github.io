---
layout: page
title: Aerodynamic roughness of snow surfaces
description: Geometric techniques for estimating multi-scale, directional surface roughness from LiDAR data
img: assets/img/projects/aero_roughness_surface.png
importance: 2
github: https://github.com/rneville/Z0-Lettau-LiDAR-Watershed
---

**Paper:** [A New Formulation and Code to Compute Aerodynamic Roughness Length for Gridded Geometry—Tested on Lidar-Derived Snow Surfaces](https://doi.org/10.3390/rs17121984), _Remote Sensing_ 17(12), 1984 (2025)

**Code:** [github.com/rneville/Z0-Lettau-LiDAR-Watershed](https://github.com/rneville/Z0-Lettau-LiDAR-Watershed) (MATLAB)

### The problem

Snowpack sits at the interface between the Earth and the atmosphere, and its surface shapes how air moves across it. Snow accumulation, terrain, and wind continually reshape that surface at many length scales, producing roughness that is both multi-scale and spatiotemporally complex. As the surface evolves, it changes albedo, wind resistance, energy exchange, and meltwater production. Surface roughness is a key input to snow-hydrology and climate models, so these models need accurate, scalable ways to estimate it.

<div class="row justify-content-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/aero_roughness_surface.png" title="Gridded snow surface" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    A gridded snow surface elevation model, the input to the roughness computation.
</div>

### Approach

Working with snow hydrologists, we developed a new way to estimate the aerodynamic roughness length (z<sub>0</sub>) of a snow surface directly from gridded LiDAR elevation data:

- **Feature detection:** a watershed segmentation divides the surface into individual roughness elements.
- **Roughness estimate:** Lettau's formula is applied to the elements found in the segmentation, capturing roughness at multiple scales.
- **Directionality:** the estimate depends on wind direction, so it captures the anisotropy of features such as drifts and sastrugi.

### Data and results

Aerodynamic roughness has traditionally been measured in the field by installing wind towers and fitting wind-speed profiles. These campaigns are expensive and labor-intensive, and they sample conditions at only a few points. As a result, roughness has been difficult to compute from real-world data at scale.

Our code computes it directly from LiDAR, which is widely available and far cheaper to collect than wind-tower measurements. Because it works from the full elevation surface, the method takes the entire geometry of a region into account rather than a handful of point measurements. We applied it to LiDAR scans of several snowfields outside Boulder, Colorado, and compared the results with other roughness estimates.

### Skills and tools

Geometric data analysis · image segmentation · LiDAR / gridded elevation data · MATLAB · interdisciplinary collaboration
