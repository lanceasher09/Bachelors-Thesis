# Forest Fire Detection: Cross-Sensor Transfer Learning with DenseNet-121 from Landsat-8 to Sentinel-2 Satellite Imagery in Benguet, Philippines


![License](https://img.shields.io/badge/license-CC--BY--4.0-green)
![Python](https://img.shields.io/badge/python-3%2B-blue)
![Model](https://img.shields.io/badge/Model-DenseNet121-orange)
![Remote Sensing](https://img.shields.io/badge/Domain-Remote%20Sensing-blueviolet)
![GIS](https://img.shields.io/badge/Tool-GIS-darkgreen)
![Status](https://img.shields.io/badge/Status-Pending%20Publication-green)

## 📄 Abstract
**[Click here to read the full Publication PDF](https://github.com/lanceasher09/Bachelors-Thesis/blob/main/EGM_ForestFire_JOIG-template_Revised_FINAL.pdf)**

This project addresses the critical lack of labeled forest fire datasets in developing nations, specifically the Philippines. We propose a cost-effective, **cross-sensor transfer learning framework** using **DenseNet-121**.

The model is pre-trained on a large-scale global **Landsat-8** dataset and fine-tuned on a limited, locally curated **Sentinel-2** dataset from Benguet, Philippines. This method overcomes data scarcity and sensor-specific limitations, achieving superior detection accuracy compared to direct transfer learning. Furthermore, we integrated **Grad-CAM** to provide interpretable heatmaps for spatial severity estimation (hectares), bridging the gap between binary classification and operational situational awareness.

## Key Features
* **Cross-Sensor Domain Adaptation:** Successfully transfers spectral features from Landsat-8 (30m resolution) to Sentinel-2 (10m resolution).
* **High Accuracy:** Achieved **94.44% Accuracy** and **89.47% F1-Score** on unseen Sentinel-2 imagery.
* **False Positive Reduction:** Reduced false positives by over **28%** compared to standard training baselines.
* **Explainable AI (XAI):** Uses Gradient-weighted Class Activation Mapping (Grad-CAM) to visualize fire severity.
* **Severity Estimation:** Automatically calculates the estimated fire area in hectares (Low, Moderate, High, Extreme).

## 📊 Performance Metrics

The model was evaluated on an independent, unseen Sentinel-2 test set. The cross-sensor fine-tuning approach significantly outperformed the baseline direct transfer method.

| Metric | Direct Transfer (Sentinel-2) | **Proposed Method (Transfer Learning)** | Improvement |
| :--- | :---: | :---: | :---: |
| **Accuracy** | 91.67% | **94.44%** | +2.77% |
| **Precision** | 84.21% | **89.47%** | +5.26% |
| **Recall** | 84.21% | **89.47%** | +5.26% |
| **F1-Score** | 84.21% | **89.47%** | +5.26% |

## Methodology

### 1. Data Preprocessing
* **Bands Used:** SWIR2, SWIR1, and Blue (Optimal for smoke/thermal anomaly detection).
* **Harmonization:** Sentinel-2 bands resampled to 10m resolution; images segmented into 256x256 patches.
* **Augmentation:** Horizontal and vertical flips were applied to the training set to expand the dataset by 4x.

### 2. Model Architecture
* **Backbone:** DenseNet-121 (Pre-trained on ImageNet).
* **Training Strategy:**
    1.  **Phase 1:** Pre-training on global Landsat-8 Active Fire dataset.
    2.  **Phase 2:** Fine-tuning on local Sentinel-2 dataset (Benguet).
* **Optimization:** Adam optimizer, Binary Cross-Entropy loss, Class Weights for imbalance handling.

### 3. Severity Estimation
Using Grad-CAM, we generate heatmaps to identify activated fire regions. The area is calculated based on pixel resolution ($10m \times 10m = 100m^2$ per pixel).

$$\text{Fire Area (ha)} = \frac{\text{NFirePixels} \times 100 m^2}{10,000 m^2}$$

## Visual Results (Grad-CAM)
*Below is an example of the model detecting fire patterns and estimating severity (as detailed in the paper).*

> ![Sample Output](Sample%20Output.png)


## 📜 Citation 
If you use this work, please cite:
```bibtex
@article{ForestFire,
  title={Forest Fire Detection: Cross-Sensor Transfer Learning with DenseNet-121 from Landsat-8 to Sentinel-2 Satellite Imagery in Benguet, Philippines},
  author={[Lance Asher M. Elloso] and [Estefanee Ashley N. Garcia] [Khristine F. Mecija] [John Paul Q. Tomas]},
  journal={[JOIG-Journal of Image and Graphics]},
  year={2026}
}
```

## ⚖️ License
This work is distributed under the **Creative Commons Attribution 4.0 International License (CC-BY 4.0)**.
