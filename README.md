#  Segmentation du Ventricule Gauche en IRM Cardiaque 3D+t

This project implements a custom pipeline for **automatic segmentation of the left ventricle (LV)** in short-axis **cardiac MRI sequences**. The work is inspired by the paper:

> **"Automatic Left Ventricle Segmentation Using Iterative Thresholding and an Active Contour Model With Adaptation on Short-Axis Cardiac MRI"**  
> by FATNASSI & et BEN EL GHALI.

📄 Final Report: [`Rapport BEN EL GHALI_FATNASSI.pdf`](./Rapport%20BEN%20EL%20GHALI_FATNASSI.pdf)  
👥 Collaborators: **Rayan FATNASSI** & **Amir Loris BEN EL GHALI**

---

## 🎯 Project Objective

The goal of this project is to develop a **multi-step 3D+t segmentation algorithm** tailored to the **geometry and motion of the left ventricle**, as seen in cine-MRI sequences.

The proposed pipeline includes:
1. **Initial Point Detection** — find center candidates based on image intensity and shape heuristics
2. **Region Growing** — apply intensity-driven expansion from the detected seed point
3. **Spatio-Temporal Propagation** — propagate segmentation mask across time frames for consistency

---

## 🗂️ Dataset
> 📂 Dataset source: [ACDC Challenge – Cardiac MRI Database](https://www.creatis.insa-lyon.fr/Challenge/acdc/databases.html)


- **Data Type**: Cine-MRI sequences of the heart
- **Format**: 2D slices over multiple time frames (`.png` or `.nii.gz`)
- **Preprocessing**: intensity normalization, morphological cleaning

> ℹ️ The dataset was provided by the course and is not publicly redistributed in this repository.

---

## ⚙️ Method Overview

### 🔹 1. Point of Interest Detection
- Intensity thresholding to isolate high-contrast regions
- Selection of candidate seed points based on shape criteria (roundness, size)

### 🔹 2. Region Growing Segmentation
- Expansion of regions from the seed using adaptive intensity thresholds
- Stopping criteria: intensity variance, boundary shape

### 🔹 3. Spatio-Temporal Propagation
- Use previous segmentation masks as priors for adjacent time frames
- Employ motion continuity and slice similarity for stability

---

## 📊 Results

- The segmentation achieved a **Dice Similarity Coefficient (DSC)** of **0.87**, indicating strong spatial overlap with the ground truth masks.
- Best parameters are saved in: `best_parameters.json`
- Visual evaluations confirm stable segmentations across time frames.

> 📈 The Dice score was computed on manually segmented masks provided in the dataset.

---

<h2>📁 Repository Structure</h2>
<pre>
lv-segmentation-3dt/
├── Notebook du projet IMA01 BEN EL GHALI_FATNASSI.ipynb            # Main implementation notebook
├── best_parameters.txt                                             # Optimal hyperparameters for the region growing step
├── report/                                                         # Final project report (PDF)
└── README.md                                                       # This file
</pre>
<h2>📚 References</h2>
<ul>
  <li>Vray, F. et al., <i>"Automatic Left Ventricle Segmentation Using Iterative Thresholding and an Active Contour Model"</i>, IEEE Transactions on Medical Imaging</li>
  <li>Course: 4IM01 – Télécom Paris</li>
</ul>
<h2>🙏 Acknowledgments</h2>
<p>This project was conducted as part of the <strong>4IM01</strong> course at <strong>Télécom Paris</strong>, under the guidance and materials provided by the teaching staff.</p>
<p>Special thanks to:</p>
<ul>
  <li>The course instructors for their structured support</li>
  <li>The original authors of the referenced article for their valuable contributions to cardiac imaging</li>
  <li>Our academic peers for their helpful discussions</li>
</ul>

