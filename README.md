# Oil Spill Detection in Hyperspectral Remote Sensing Imagery

## Overview

Oil spills are among the most destructive environmental disasters affecting marine ecosystems. They contaminate water bodies, threaten aquatic life, disrupt coastal economies, and require rapid detection for effective containment and cleanup. Traditional monitoring methods often rely on manual interpretation of satellite imagery, which can be time-consuming, labor-intensive, and difficult to scale across large oceanic regions.

This project presents an intelligent oil-spill detection framework that leverages hyperspectral remote sensing, machine learning, and deep learning techniques to automatically identify oil-contaminated regions in marine environments. Instead of relying on handcrafted rules or extensive labeled datasets, the framework learns meaningful spectral representations from hyperspectral imagery and identifies oil spills as anomalies within the data.

The proposed approach combines dimensionality reduction, representation learning, anomaly detection, clustering, classification, and spatial segmentation into a unified detection pipeline capable of handling the complexity of high-dimensional hyperspectral data.


## Problem Statement

Detecting oil spills from satellite imagery is a challenging task due to:

- High dimensionality of hyperspectral data.
- Presence of sensor noise and atmospheric interference.
- Spectral similarity between oil-covered water and surrounding ocean surfaces.
- Limited availability of labeled training data.
- Variability in environmental and illumination conditions.

The objective of this project is to develop a robust and scalable framework capable of automatically detecting oil spills while minimizing false detections and preserving spatial consistency.


## Why Hyperspectral Imaging?

Conventional RGB imagery captures only three spectral channels:

- Red
- Green
- Blue

Hyperspectral sensors capture information across hundreds of spectral bands, providing a detailed spectral signature for every pixel in the image.

Because oil and water interact differently with electromagnetic radiation, their spectral responses differ across wavelengths. These differences may not be visible in standard imagery but become distinguishable in hyperspectral data.

This rich spectral information enables more accurate detection of oil spills, provided that the high dimensionality and noise within the data are effectively managed.


## Research Motivation

Traditional oil-spill detection methods often face several limitations:

### Manual Feature Engineering

Many approaches depend on predefined spectral indices and threshold-based techniques that require expert knowledge and may not generalize across datasets.

### Curse of Dimensionality

Hyperspectral imagery contains hundreds of highly correlated bands, increasing computational complexity and making model training more difficult.

### Scarcity of Labels

Accurately annotated oil-spill datasets are limited and expensive to produce, reducing the effectiveness of fully supervised learning approaches.

To address these challenges, this project adopts a hybrid unsupervised learning framework capable of learning useful representations directly from the data.


## Conceptual Framework

The central idea behind this project is simple:

> Instead of explicitly teaching the system what oil looks like, teach it what normal ocean water looks like and identify anything that behaves differently.

Since oil-covered regions occupy only a small portion of the image compared to the surrounding ocean, they naturally appear as anomalies in the spectral feature space.

The framework is therefore designed around anomaly detection principles, enhanced through feature learning and spatial refinement.


# Methodology

## 1. Noise Reduction and Feature Enhancement

### Minimum Noise Fraction (MNF)

Hyperspectral images often contain significant noise and redundancy.

The MNF transformation is applied to:

- Reduce sensor noise
- Remove redundant information
- Improve signal quality
- Preserve the most informative spectral components

MNF effectively compresses the original spectral space while retaining meaningful information necessary for oil-spill detection.


## 2. Deep Feature Learning

### Autoencoder-Based Representation Learning

After MNF transformation, the data is passed through a deep Autoencoder.

An Autoencoder is a neural network that learns a compressed representation of the input while attempting to reconstruct the original data.

This enables the model to:

- Capture nonlinear spectral relationships
- Learn compact latent representations
- Remove irrelevant variations
- Improve feature separability

The learned latent space serves as the foundation for subsequent anomaly detection.


## 3. Anomaly Detection

### Isolation Forest

Oil-covered pixels are relatively rare compared to normal water pixels.

Isolation Forest is used to identify these rare observations by isolating data points that differ significantly from the majority.

Advantages include:

- No requirement for labeled data
- Effective handling of high-dimensional features
- Strong performance on anomaly detection tasks

Pixels receiving high anomaly scores become candidate oil-spill regions.


## 4. Spectral Structure Discovery

### K-Means Clustering

Not all anomalies correspond to actual oil spills.

Anomalous pixels may also arise from:

- Sensor artifacts
- Surface reflections
- Environmental disturbances

K-Means clustering groups anomalous pixels according to spectral similarity, helping distinguish potential oil regions from other anomalous structures.


## 5. Classification Refinement

### Support Vector Machine (SVM)

Cluster boundaries generated by K-Means may be coarse or ambiguous.

Support Vector Machines are used to refine these boundaries and improve class separation.

The SVM stage helps:

- Reduce false positives
- Improve decision boundaries
- Increase classification reliability

This produces a more accurate oil-spill prediction map.

## 6. Spatial Refinement

### Random Walker Segmentation

Pixel-wise classification can lead to fragmented and noisy predictions.

To incorporate spatial context, Random Walker segmentation is applied.

The image is represented as a graph where:

- Pixels act as nodes
- Neighboring pixels are connected through weighted edges

Labels propagate across the graph based on similarity, producing smoother and more coherent oil-spill regions.

This final stage improves spatial consistency and reduces isolated misclassifications.


# Complete Detection Pipeline

Hyperspectral Image
        │
        ▼
Noise Variance Estimation
        │
        ▼
MNF Transformation
        │
        ▼
Autoencoder Feature Extraction
        │
        ▼
Isolation Forest
        │
        ▼
K-Means Clustering
        │
        ▼
SVM Refinement
        │
        ▼
Random Walker Segmentation
        │
        ▼
Oil Spill Detection Map


---

# Technology Stack

## Programming Language

- Python 3.x

## Development Environment

- Jupyter Notebook

## Deep Learning

- TensorFlow
- Keras

## Machine Learning

- Scikit-Learn

## Scientific Computing

- NumPy
- SciPy

## Data Analysis

- Pandas

## Image Processing

- Scikit-Image

## Visualization

- Matplotlib
- Seaborn

---

# Key Algorithms Used

| Component | Purpose |

| MNF | Noise reduction and dimensionality reduction |
| Autoencoder | Nonlinear feature extraction |
| Isolation Forest | Unsupervised anomaly detection |
| K-Means | Spectral clustering |
| SVM | Classification refinement |
| Random Walker | Spatial segmentation and smoothing |



# Dataset

The framework is evaluated using benchmark hyperspectral oil-spill scenes.

Each dataset contains:

- Hyperspectral image cube
- Ground-truth oil-spill mask

Example dataset structure:

```
GM1.mat
GM2.mat
GM3.mat
...
GM18.mat
```

Each image consists of:

Height × Width × Spectral Bands

along with corresponding ground-truth annotations used for evaluation.



# Performance Evaluation

The effectiveness of the framework is assessed using standard classification metrics.

## ROC Curve

The Receiver Operating Characteristic (ROC) curve measures the trade-off between:

- True Positive Rate
- False Positive Rate

across multiple decision thresholds.

## AUC Score

The Area Under the Curve (AUC) summarizes overall detection performance.

Higher AUC values indicate:

- Better discrimination capability
- Lower false-positive rates
- More reliable oil-spill identification


# Results

The proposed framework demonstrates several advantages:

- Effective noise suppression through MNF.
- Improved feature representation using Autoencoders.
- Robust unsupervised anomaly detection.
- Enhanced classification through SVM refinement.
- Spatially coherent detection maps after Random Walker segmentation.
- Improved detection performance compared to conventional dimensionality reduction approaches such as KPCA.


# Applications

This framework can be extended to numerous remote sensing and environmental monitoring applications, including:

- Marine pollution monitoring
- Offshore oil-spill surveillance
- Environmental risk assessment
- Coastal ecosystem protection
- Hyperspectral anomaly detection
- Disaster response systems
- Remote sensing analytics


# Future Work

Potential improvements include:

- Vision Transformer (ViT)-based feature extraction
- Graph Neural Networks (GNNs)
- Self-supervised representation learning
- Real-time satellite monitoring systems
- Multi-sensor data fusion
- Explainable AI for anomaly interpretation


# Conclusion

This project demonstrates how hyperspectral remote sensing and machine learning can be combined to solve a critical environmental monitoring problem. By integrating dimensionality reduction, deep representation learning, anomaly detection, classification, and spatial refinement, the framework provides a comprehensive solution for automated oil-spill detection in complex marine environments.

The work highlights the potential of hybrid unsupervised learning approaches for analyzing high-dimensional remote sensing data while reducing dependence on large labeled datasets.
