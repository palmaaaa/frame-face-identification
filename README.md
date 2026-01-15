# 🧠 F.R.A.M.E.
**Facial Representation Averaging for Matching Efficiency**

Open-set face identification using lightweight embeddings and temporal aggregation.  
Biometrics course project - *Sapienza University of Rome (Fall 2024)*.

---

## 📌 Overview

This repository contains a **student project** developed for a Biometrics course, focused on **open set face identification** under real time constraints.

The project explores a simple but effective idea:

> Instead of relying on a single image, **aggregate facial embeddings across multiple frames** to obtain a more stable and discriminative identity representation.

The resulting system, called **F.R.A.M.E.**, shows that strong open set performance can be achieved with a **compact model** and minimal computational overhead.

---

## 🎯 Problem Setting

Unlike closed set face recognition, **open set identification** requires a system to:

- correctly identify known identities when present in the gallery
- **reject unknown identities** that do not belong to any enrolled subject

This makes the task significantly more challenging and closer to real-world deployment scenarios.

---

## 🧩 Core Idea

Given multiple frames of the same subject (e.g. from a video stream):

1. Compute a facial embedding for each frame
2. Average the embeddings over a sliding temporal window
3. L2-normalize the result
4. Perform matching using cosine similarity

This simple aggregation:
- reduces noise
- improves robustness to pose and illumination
- significantly boosts open set performance

---

## 🏗️ Model Summary

- Backbone: **TinyViT-inspired Vision Transformer**
- Input resolution: `224 × 224`
- Embedding dimension: `512`
- Training loss: **ArcFace**
- Parameter count: **~0.8M**

The classification head is used **only during training**.  
At inference time, the model acts purely as an **embedding extractor**.

---

## ⏱️ Real-Time Perspective

F.R.A.M.E. is designed with streaming scenarios in mind:

- embeddings are computed per frame
- a fixed size sliding window is maintained
- aggregation is updated incrementally

This makes the approach suitable for **low-latency applications**, assuming a face detector is available upstream.

---

## 📊 Dataset

- **VGGFace2**
  - large scale, public research dataset
  - faces captured “in the wild”
  - high variability in pose, lighting, age and occlusions
  - pre aligned face crops with identity labels

---

## 📈 Evaluation

The system is evaluated using standard **biometric metrics for open-set identification**, including:

- ROC curves
- TAR @ FAR
- FPIR / TPLR
- Detection & Identification Rate (DIR)
- Equal Error Rate (EER)

Performance is analyzed as a function of the number of frames used for embedding aggregation.

---

## 🔍 Key Observations

- With **1 frame** performance is unstable and close to random
- With **10–20 frames** identification becomes highly reliable
- Beyond ~20 frames improvements saturate
- Open-set rejection improves dramatically as more frames are aggregated

**Practical takeaway:**  
📌 averaging a moderate number of frames (≈10–20) is enough to achieve near perfect identification while keeping false acceptances very low.

---

## ⚠️ Limitations

- This project **does not propose a new face recognition architecture**
- Performance depends on having multiple frames per identity
- No comparison against modern mobile scale SOTA models
- The focus is on experimental analysis, not production deployment

---

## 📂 Repository Contents

- `report.pdf` – Full project report, including methodology, experiments, and results  
- `FRAME.ipynb` – Notebook used for experiments and analysis

This repository primarily serves as **documentation of the project work**.

---

## 👥 Authors

- **Paolo Cursi**  
- **Michele Palma**

Computer Science  
Sapienza University of Rome

---

## 📚 References

- Deng et al., *ArcFace: Additive Angular Margin Loss for Deep Face Recognition*, CVPR 2019  
- Wu et al., *TinyViT: Fast Pretraining Distillation for Small Vision Transformers*, ECCV 2022

---

## 📝 License

Released for **educational and research purposes**.
