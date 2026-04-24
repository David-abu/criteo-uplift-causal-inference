# Criteo Uplift v2.1 — Causal Inference & Uplift Modelling

## Overview
This project investigates the causal effect of digital advertising on user 
behaviour using the Criteo Uplift v2.1 dataset. The analysis addresses two 
research questions:

1. **What is the incremental effect of ad treatment on visits and conversions?**
2. **Who benefits most? (Heterogeneous Treatment Effects)**

---

## Dataset
- **Source:** [Criteo Uplift v2.1 — Kaggle](https://www.kaggle.com/datasets/evgeniypolin/criteo-uplift-v2-1)
- **Size:** 13.9 million users (200,000 sampled for analysis)
- **Features:** 12 anonymous float features (f0–f11)
- **Treatment:** Binary (85% treated / 15% control — randomised)
- **Outcomes:** `visit` (4.85%) and `conversion` (0.29%)

---

## Methods
| Method | Purpose |
|---|---|
| Difference-in-means + t-test | Average Treatment Effect (ATE) |
| Inverse Probability Weighting (IPW) | ATE robustness check |
| S-Learner (Logistic Regression) | Conservative CATE estimation |
| T-Learner (Logistic Regression) | Flexible CATE — finds negative effects |
| T-Learner (LightGBM) | Non-linear CATE — most accurate |
| 2×2 Segmentation | Classify users into 4 targeting groups |
| Uplift Curves + Qini | Model evaluation |

---

## Key Results

### Average Treatment Effect
| Outcome | ATE | Relative Lift | p-value |
|---|---|---|---|
| Website Visits | +0.0103 | +26.4% | < 0.001 |
| Conversions | +0.0017 | +93.0% | < 0.001 |

### CATE Heterogeneity (LightGBM T-Learner)
- CATE range: **−0.2724 to +0.5816**
- Outcome model AUC: **0.944** (treated) / **0.934** (control)

### Customer Segmentation
| Segment | Count | % | Action |
|---|---|---|---|
| Persuadables | 2,021 | 3.4% | TARGET |
| Sure Things | 7,203 | 12.0% | SKIP |
| Lost Causes | 50,507 | 84.2% | SKIP |
| Sleeping Dogs | 269 | 0.4% | SUPPRESS |

### Uplift Evaluation
- S-Learner Qini: **163.22**
- T-Learner Qini: **153.84**
- Top 20% by CATE captures **65–79%** of total campaign uplift

---

## Project Structure