# Motion Registration and Denoising for ST-MRF
This repository provides the implementation of the motion correction and denoising pipeline used in the study: "Physics-informed optimization of saturation-transfer MRI protocols using nondifferentiable Bloch models" published in Physics in Medicine and Biology (2026).

---

## 🔍 Overview

The pipeline consists of two main stages to enhance the quality of multidimensional Magnetic Resonance Fingerprinting (MRF) data:

1. Motion Registration (STN + NCC): Compends for motion artifacts by registering all dynamic scans to a reference ($S_0$) image. It utilizes a Spatial Transformer Network (STN) optimized with a Normalized Cross-Correlation (NCC) loss.

2. Denoising (MD-S2S): Applies a self-supervised denoising technique (Multidimensional-Self2Self) to the registered images. This stage uses an optimization scheme where the network is trained and tested on the same dataset, making it applicable even without a large training corpus.

---

## 🧠 Architecture

1. Spatial Transformer Network (STN).
The RegNet class estimates a 2D affine transformation matrix (rotation and translation) for each dynamic scan relative to the first frame. Loss Function: Negative log of Normalized Cross-Correlation (NCC). Optimization: 200 epochs, Learning Rate = $10^{-4}$, Batch Size = 1.

2. MD-S2S (Multidimensional-Self2Self)
A self-supervised denoising network based on a Residual Block architecture. It employs Bernoulli masking and data augmentation to learn noise-free representations from the noisy input itself. Strategy: Optimization-based denoising (Train set = Test set). Optimization: 10,000 epochs, Learning Rate = $10^{-4}$, Masking probability = 0.3.

---

## Citation
If you use this code for your research, please cite:

@article{Kang2026,
  title={Physics-informed optimization of saturation-transfer MRI protocols using nondifferentiable Bloch models},
  author={Kang, Beomgu and others},
  journal={Physics in Medicine and Biology},
  year={2026},
  publisher={IOP Publishing}
}

@article{kang2024self,
  title={Self-supervised learning for denoising of multidimensional MRI data},
  author={Kang, Beomgu and Lee, Wonil and Seo, Hyunseok and Heo, Hye-Young and Park, HyunWook},
  journal={Magnetic resonance in medicine},
  volume={92},
  number={5},
  pages={1980--1994},
  year={2024},
  publisher={Wiley Online Library}
}
