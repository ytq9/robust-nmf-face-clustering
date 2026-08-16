# Robust NMF for Face Image Clustering

An experimental comparison of robust non-negative matrix factorization (NMF) methods for face-image clustering under salt-and-pepper noise. The project evaluates whether reconstruction robustness translates into better clustering quality on the ORL and Extended Yale B datasets.

## Project scope

This was completed as a four-person COMP5328 Advanced Machine Learning project.

Primary contribution represented in this repository:

- implemented L2-NMF with multiplicative updates;
- implemented L1-NMF with projected gradient updates;
- built grayscale conversion, image resizing, normalization, and salt-and-pepper noise preprocessing;
- contributed to the experimental design and evaluation pipeline.

The L2,1-NMF and hypersurface/Charbonnier NMF implementations were team contributions and are retained in the notebook so the original comparison remains reproducible.

## Compared methods

| Method | Robustness mechanism |
| --- | --- |
| L2-NMF | Squared reconstruction loss with multiplicative updates |
| L1-NMF | Absolute reconstruction loss with non-negative projected updates |
| L2,1-NMF | Column-wise robust loss via iterative reweighting |
| Hypersurface NMF | Charbonnier-weighted multiplicative updates |

The evaluation reports clustering accuracy, normalized mutual information (NMI), and relative reconstruction error (RRE). Each reported result uses five trials with a random 90% sample of the data.

## Recorded results

The following values are preserved from the executed notebook for salt-and-pepper noise experiments. Lower RRE is better; higher accuracy and NMI are better.

| Dataset | Method | Accuracy | NMI | RRE |
| --- | --- | ---: | ---: | ---: |
| ORL | L2-NMF | 0.4083 ± 0.0234 | 0.6117 ± 0.0160 | 0.2613 ± 0.0010 |
| ORL | L1-NMF | **0.5933 ± 0.0196** | **0.7709 ± 0.0104** | 0.2687 ± 0.0022 |
| ORL | Hypersurface NMF | 0.4800 ± 0.0133 | 0.6707 ± 0.0064 | **0.2311 ± 0.0013** |
| ORL | L2,1-NMF | 0.4928 ± 0.0277 | 0.6706 ± 0.0223 | 0.2621 ± 0.0004 |
| Extended Yale B | L2-NMF | 0.1159 ± 0.0057 | 0.1390 ± 0.0068 | 0.2877 ± 0.0004 |
| Extended Yale B | L1-NMF | **0.2344 ± 0.0035** | 0.2858 ± 0.0164 | **0.2356 ± 0.0007** |
| Extended Yale B | Hypersurface NMF | 0.0953 ± 0.0029 | 0.0976 ± 0.0078 | 0.2768 ± 0.0011 |
| Extended Yale B | L2,1-NMF | 0.2236 ± 0.0090 | **0.3030 ± 0.0178** | 0.2520 ± 0.0004 |

These results illustrate an important limitation of reconstruction-based model selection: the method with the lowest RRE does not necessarily provide the best clustering accuracy or NMI.

## Repository structure

```text
.
├── data/
│   └── README.md
├── notebooks/
│   └── robust_nmf_face_clustering.ipynb
├── .gitignore
├── README.md
└── requirements.txt
```

## Setup

Python 3.9 or newer is recommended.

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
jupyter lab notebooks/robust_nmf_face_clustering.ipynb
```

Download the ORL and Extended Yale B datasets separately and arrange them as described in [`data/README.md`](data/README.md). The datasets are intentionally excluded from version control because their redistribution terms should be checked at the original sources.

## Reproducibility notes

- The notebook expects image files in PGM format.
- ORL images are resized from 92 × 112 by a factor of 2.
- Extended Yale B images are resized from 168 × 192 by a factor of 3.
- Random seeds are set inside the repeated-sampling evaluation, but library-version differences may produce small variations.
- Accuracy uses majority-label assignment for each K-means cluster; NMI is label permutation invariant.

## Academic-use note

This repository preserves an academic team project for portfolio and reproducibility purposes. If you are currently enrolled in a course using a similar assignment, follow your institution's academic-integrity rules and do not submit this work as your own.
