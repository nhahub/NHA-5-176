# DermaVision

### Deep Learning-Based Skin Lesion Classification Using HAM10000

DermaVision is a **research and educational** deep learning project that classifies dermoscopic skin lesion images into seven categories. It compares a baseline convolutional neural network (CNN), ResNet50 and EfficientNet-B0 under a leakage-aware evaluation protocol.

> **Medical disclaimer:** DermaVision is not a medical device. Its predictions and Grad-CAM visualizations do not constitute a diagnosis or medical advice and must not be used for clinical decisions.

## Project Objectives

- Build a reproducible seven-class dermoscopic image classification pipeline.
- Prevent data leakage by splitting at the **lesion_id** level.
- Compare a baseline CNN, ResNet50 and EfficientNet-B0 using consistent data partitions.
- Investigate class weighting, focal loss and data augmentation for class imbalance.
- Report **balanced accuracy**, **macro-F1**, per-class recall and confusion matrices, with particular attention to melanoma (MEL).
- Use Grad-CAM to visualize model focus and provide a Streamlit research demo.

## Dataset: HAM10000

HAM10000 contains **10,015 dermoscopic images** in seven lesion categories.

| Label | Category |
| --- | --- |
| `akiec` | Actinic keratoses and intraepithelial carcinoma |
| `bcc` | Basal cell carcinoma |
| `bkl` | Benign keratosis-like lesions |
| `df` | Dermatofibroma |
| `mel` | Melanoma |
| `nv` | Melanocytic nevi |
| `vasc` | Vascular lesions |

**Dataset reference:** [Tschandl et al. (2018), Scientific Data](https://doi.org/10.1038/sdata.2018.161).

**Dataset limitation:** HAM10000 does not contain Fitzpatrick skin-type labels, so skin-tone subgroup coverage cannot be evaluated from this dataset alone.

## Planned Implementation

1. **Data preparation:** Validate HAM10000 image files, metadata, labels, missing values and class distribution.
2. **Split:** Create approximately 70/15/15 train/validation/test partitions, stratified by diagnosis where feasible and grouped by `lesion_id`. Verify zero lesion-ID overlap and all seven classes in each partition.
3. **Model training:** Train a simple baseline CNN, and fine-tune ResNet50 and EfficientNet-B0 with a shared training/evaluation pipeline.
4. **Imbalance experiments:** Compare augmentation, weighted losses and focal loss using validation metrics only.
5. **Selection and evaluation:** Select a model and melanoma decision threshold on validation, then conduct a single final evaluation on the untouched lesion-grouped test set.
6. **Explainability and demo:** Review Grad-CAM heatmaps and build a Streamlit interface for single-image dermoscopic inference.

## Evaluation Metrics and Targets

**All values below are planned targets, not achieved results.**

| Metric | Plan |
| --- | --- |
| Primary evaluation | Balanced accuracy and macro-F1 on the lesion-grouped test set |
| Macro-F1 target | At least **0.70** |
| MEL operating point | Recall ≥ **0.80** at precision ≥ **0.40**; fix threshold using validation data |
| Per-class reporting | Precision, recall, F1 and bootstrap confidence intervals for recall |
| Majority-class reference | Always predict `nv` (~67% accuracy); demonstrates why accuracy alone is insufficient |
| Model comparison | Baseline CNN vs. ResNet50 vs. EfficientNet-B0 |

These targets are research objectives, not clinical performance guarantees.

## Streamlit Demo (Planned)

The demo will accept **one dermoscopic PNG/JPEG image**, display seven class probabilities and a Grad-CAM map, and show a prominent research-only disclaimer. Invalid or oversized files will be rejected. Low-confidence and potentially out-of-distribution inputs will be flagged. **Ordinary smartphone photographs are outside the validated input domain.**

## Technology Stack

- **Language:** Python
- **Deep learning:** PyTorch, torchvision
- **Data and evaluation:** NumPy, pandas, scikit-learn
- **Explainability:** Grad-CAM
- **Application:** Streamlit
- **Collaboration:** GitHub and Google Sheets

## Project Documentation

- **Stage 1:** Project Planning & Management
- **Stage 2:** Literature Review
- **Stage 3:** Requirements Gathering
- **Stage 4 (planned):** System Analysis & Design
- **Stage 5 (planned):** Implementation
- **Stage 6 (planned):** Testing, Final Report & Presentation

## Team Members

| Member | Main Responsibility |
| --- | --- |
| Omar Ayman | Team lead, training pipeline, integration and reporting |
| Menna | Dataset, EDA, lesion-grouped splitting and dataloaders |
| Ahmed Khaled | Baseline CNN, ResNet50 and experiments |
| Arwa | EfficientNet-B0, imbalance handling and threshold analysis |
| Fatma Mahmoud | Evaluation, Grad-CAM and Streamlit app |

## Project Status

**In development.** Architecture comparisons, targets and application features described above are part of the project plan and should not be interpreted as completed or validated outcomes.

## Responsible Use

This project uses public research data subject to applicable licensing conditions. Uploads to the demo are intended for temporary inference only, without storing personal images. DermaVision must not be used for screening, diagnosis, treatment, or other patient-care decisions.

## Key References

1. Tschandl, P., Rosendahl, C., & Kittler, H. (2018). *The HAM10000 dataset*. Scientific Data. https://doi.org/10.1038/sdata.2018.161
2. Codella et al. (2019). *Skin Lesion Analysis Toward Melanoma Detection 2018: A Challenge Hosted by the International Skin Imaging Collaboration*. https://arxiv.org/abs/1902.03368
