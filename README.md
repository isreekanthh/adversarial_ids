# Adversarial Attacks on ML-Based Intrusion Detection Systems


> **Author:** Sreekanth | Cybersecurity Researcher |
> 
> **Research Project** | Cybersecurity + Adversarial Machine Learning

> **Dataset:** NSL-KDD |

>**Attack:** FGSM |

>**Defense:** Adversarial Training

---

## Abstract

This research investigates the vulnerability of machine learning-based
Intrusion Detection Systems (IDS) to adversarial examples. A Random Forest
classifier trained on the NSL-KDD dataset achieves 77.31% accuracy
on clean data but is completely compromised under Fast Gradient Sign Method
(FGSM) adversarial attack, achieving 100.0% evasion rate at epsilon=0.05.
The attack primarily manipulates TCP error rate features and connection flags.
Adversarial training recovers 62.0% of evaded attacks at a cost of only 0.92% clean accuracy.

---

## Project Structure

    adversarial-ids/
    ├── notebooks/
    │   ├── train_ids_model.ipynb          # IDS model training
    │   ├── adversarial_attacks.ipynb      # FGSM attack implementation
    │   ├── evasion_analysis.ipynb         # Attack analysis and metrics
    │   └── defense_layer.ipynb            # Defense mechanisms
    ├── data/
    │   ├── KDDTrain+.txt                  # NSL-KDD training set
    │   ├── KDDTest+.txt                   # NSL-KDD test set
    │   └── *.npy                          # Processed numpy arrays
    ├── models/
    │   ├── rf_ids_model.pkl               # Original trained model
    │   └── rf_robust_model.pkl            # Adversarially trained model
    └── results/
        ├── attack_distribution.png
        ├── confusion_matrix_baseline.png
        ├── fgsm_epsilon_vs_evasion.png
        ├── confusion_before_after_fgsm.png
        ├── top15_perturbed_features.png
        ├── feature_distribution_shift.png
        ├── confidence_shift.png
        ├── roc_curve_degradation.png
        ├── defense_comparison.png
        └── roc_defense_comparison.png

---

## Key Findings

| Metric | Value |
|--------|-------|
| Baseline IDS Accuracy | 77.31% |
| Baseline Attack Recall | 62% |
| Attacks Evading Naturally | 38% |
| FGSM Evasion Rate | 100.0% |
| Minimum Epsilon for Full Evasion | 0.05 |
| Model Confidence Drop | 0.6667 |
| Top Attacked Feature | TCP Flag + Error Rate features |
| Adversarial Training Recovery | 62.0% |
| Clean Accuracy Cost of Defense | 0.92% |

---

## Methodology

### 1. Target Model
- **Algorithm:** Random Forest (100 estimators, max depth 20)
- **Dataset:** NSL-KDD (125,973 train / 22,544 test samples)
- **Task:** Binary classification — Normal vs Attack traffic
- **Features:** 41 network traffic features

### 2. Adversarial Attack — FGSM
Fast Gradient Sign Method estimates the gradient of the model's
decision boundary with respect to each input feature, then perturbs
features in the direction that maximally reduces attack confidence.

**Feature Validity Constraints Applied:**
- Binary features (land, logged_in, root_shell): locked, never perturbed
- Rate features (serror_rate, rerror_rate, etc.): clipped to [0.0, 1.0]
- Count features (src_bytes, dst_bytes, etc.): clipped to >= 0

### 3. Defense Mechanisms

**Feature Squeezing (bit_depth=4):**
Reduces feature precision to remove adversarial perturbations.
Result: 0% recovery — insufficient against strong FGSM.

**Adversarial Training:**
Augments training data with adversarially perturbed samples.
Result: 62.0% attack recovery at 0.92% clean accuracy cost.

---

## MITRE ATT&CK Mapping

| ATT&CK Technique | Relevance |
|-----------------|-----------|
| T1562.001 — Impair Defenses | Adversarial examples impair IDS detection |
| T1040 — Network Sniffing | Feature manipulation mimics legitimate traffic |
| T1036 — Masquerading | Attack traffic disguised as normal connections |

---

## References

- Goodfellow et al. (2014) — Explaining and Harnessing Adversarial Examples
- Tavallaee et al. (2009) — A Detailed Analysis of the KDD CUP 99 Dataset
- Carlini & Wagner (2017) — Towards Evaluating the Robustness of Neural Networks
- Xu et al. (2017) — Feature Squeezing: Detecting Adversarial Examples in DNNs
