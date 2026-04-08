# Oil-Spill
Abstract—Hyperspectral imaging (HSI) has emerged as a
powerful tool for monitoring marine oil spills as a result of its
ability to capture rich spectral information. Accurate detection
of oil spills in hyperspectral data is challenging due to high
dimensionality, spectral variability, and environmental noise. The
HOSD benchmark data set introduced an unsupervised Isolation
Forest (iForest)-based framework for oil spill detection, achieving
promising results without requiring labeled data. However, raw
spectral inputs or linear dimensionality reduction methods such
as PCA may not fully capture complex nonlinear patterns inher
ent in hyperspectral images. In this research, we propose a hybrid
framework that integrates an Autoencoder (AE) with the existing
iForest pipeline to enhance feature representation and anomaly
detection performance. The AE is trained in an unsupervised
manner to learn a compact, nonlinear latent representation
of the spectral data, effectively reducing dimensionality while
preserving discriminative information. Each pixel spectrum is
encoded into a low-dimensional latent vector which is then
fed into the iForest for anomaly scoring. This approach takes
advantage of both deep feature learning and tree-based anomaly
detection, with the aim of improving spatial coherence and
reducing false positives. Preprocessing steps are applied including
bad band removal, spectral smoothing, and normalization to
ensure robust learning. The latent representation of the AE
captures subtle spectral variations that are difficult to detect
using linear methods alone. Thresholding and morphological
post-processing are employed to convert anomaly scores into
refined oil spill masks. Quantitative evaluation is performed
using precision, recall, F1-score, and Intersection-over-Union
(IoU) metrics, while qualitative analysis is conducted through
visualization of detection maps.
Index Terms—Hyperspectral imaging, anomaly detection, au
toencoder, isolation forest, oil spill detection.
