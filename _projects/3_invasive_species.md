---
layout: page
title: Spotting invasive plants in citizen-science photos
description: Fine-tuned a DINOv3 vision transformer to identify 40 invasive plant species of the Desert Southwest from iNaturalist photos, reaching 93.1% top-1 accuracy.
img: assets/img/projects/invasive_species_map.png
importance: 1
github: https://github.com/Erdos-Projects/fall-2026-invasive-species
---

**Program:** [Erdős Institute](https://www.erdosinstitute.org) Deep Learning Boot Camp, Fall 2026 ([project page](https://www.erdosinstitute.org/project-database/fall-2026/deep-learning-boot-camp/spotting-invasive-plant-species-from-citizen-science-photos))

**Team:** Craig Corsi, Jay Desai, Rachel Neville, and Apostolos Zournas

**Links:** [code](https://github.com/Erdos-Projects/fall-2026-invasive-species) · [slides](https://www.erdosinstitute.org/_files/ugd/9e93a7_bc9d545d75054f3a8acd1e26acb1cfc1.pdf) · [executive summary](https://www.erdosinstitute.org/_files/ugd/9e93a7_64bee08acdcf47a7be1d015ba4a481ea.pdf)

<div class="row justify-content-center">
    <div class="col-sm-12 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/invasive_errors_by_group.png" title="Test-set error rate by group" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Test-set error rate by group for the two final models. For invasive species, errors are missed or misclassified photos; for the not-invasive groups, they are false positives. Both models struggle most with native species on watch lists (right).
</div>

### My contributions

- Came up with the problem and scoped it for the project.
- Curated the lists of invasive plant species from regional, state, and federal sources.
- Ran the ConvNeXt-Tiny and SigLIP 2 fine-tuning experiments.
- Wrote the slides, and organized and published the GitHub repository.

### The problem

Invasive plant species outcompete native species for water and soil nutrients and fundamentally change the ecosystems they spread into. In the Southwest they alter fire regimes, reduce biodiversity, and disrupt food webs. Catching small, localized infestations early, before they require large-scale or expensive intervention, is one of the most effective containment tools. But field surveys can't cover the land at the scale needed, while citizen-science platforms like iNaturalist collect huge numbers of plant photos from volunteers.

### What we built

An image classifier that looks at a plant photo from the Desert Southwest and either names one of **40 regionally invasive species** or answers _not invasive_, including for native species that look very similar.

### Data

- **Source:** about 19,000 research-grade photos from the [iNaturalist](https://www.inaturalist.org/) API, covering Arizona, New Mexico, and eastern California.
- **Labels:** invasive species drawn from published regional, state, and federal invasive and noxious-weed lists. The _not invasive_ class covers 401 other species, including native look-alikes and introduced species that aren't invasive here.
- **Leakage-safe splits:** each photographer appears in only one split, and validation and test photos were all uploaded after the pretrained models' training data was collected. A separate test set of species never seen in training checks how the model handles unfamiliar plants.

### Approach

- **Model search:** fine-tuned nine pretrained backbones (ResNet-18 through ResNet-152, ConvNeXt-Tiny, DINOv3 ViT-S/16, a plant-specific DINOv3, and SigLIP 2) with a shared training recipe, tuning each one change at a time across 55 runs.
- **Baselines:** compared every fine-tuned model against a logistic regression on its frozen features, and against BioCLIP 2, a large biology-specific vision–language model used zero-shot.
- **Model selection:** chose the final model with bootstrap confidence intervals on validation macro-F1, then evaluated once on the held-out test set.

### Results

The fine-tuned **DINOv3 ViT-S/16** reached **93.1% top-1 accuracy** on the test set and 91.8% accuracy on species never seen in training, with only 21.6 million parameters and about 10 ms per photo on a T4 GPU. Accuracy is lower on the invasive photos alone (77%): most test photos are of non-invasive species, which the model classifies correctly more often. BioCLIP 2 reaches 95% on the invasive photos.

BioCLIP 2, used zero-shot, scored higher still (98.7%), but it is 14 times larger and 14 times slower. That makes the fine-tuned DINOv3 the practical choice when compute is limited, and BioCLIP 2 the choice when accuracy matters most. Both models struggled most with native species on watch lists, which are exactly the plants experts also flag for monitoring.

### Skills and tools

Python · PyTorch · computer vision · transfer learning and fine-tuning (vision transformers, CNNs) · zero-shot vision–language models · data curation via API · experiment design · bootstrap model comparison · team collaboration
