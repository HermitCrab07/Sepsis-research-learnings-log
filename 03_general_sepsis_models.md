### Algorithms for Detecting or Declaring Sepsis

Below is a concise overview of widely used clinical criteria and emerging machine‑learning (ML) models, including their strengths, weaknesses, and ideal use cases.

---

## 1. Established Clinical Criteria / Algorithms

| Algorithm                                             | Core Criteria (abbreviated)                                                                                                         | Main Use                                      | **Pros**                        | **Cons**                                                      |
| ----------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------- | ------------------------------- | ------------------------------------------------------------- |
| **SIRS**<br>(Systemic Inflammatory Response Syndrome) | ≥ 2 of:<br>• Temp > 38 °C or < 36 °C<br>• HR > 90 bpm<br>• RR > 20 /min or PaCO₂ < 32 mmHg<br>• WBC > 12 k or < 4 k or > 10 % bands |  Screening with suspected/confirmed infection | Simple, widely adopted          | Very sensitive but **not specific** → many false positives    |
| **qSOFA**<br>(Quick SOFA)                             | Score ≥ 2 of:<br>• RR ≥ 22 /min<br>• SBP ≤ 100 mmHg<br>• GCS < 15                                                                   | Rapid bedside risk stratification             | Easy, no labs                   | Lower sensitivity; designed more for **mortality prediction** |
| **SOFA**<br>(Full SOFA)                               | 6 organ systems (resp, coag, liver, CV, CNS, renal); sepsis = suspected infection **+ SOFA ↑ ≥ 2**                                  | ICU & Sepsis‑3 gold standard                  | Captures true organ dysfunction | Needs labs, less practical in ED                              |

---

## 2. Machine‑Learning–Based Algorithms

| Model / Study                       | Data Inputs                               | ML Approach             | Notable Points                                                |
| ----------------------------------- | ----------------------------------------- | ----------------------- | ------------------------------------------------------------- |
| **Epic Sepsis Model (ESM)**         | Structured EHR vitals, labs, demographics | Proprietary (ensemble)  | Deployed in many US health systems; mixed performance reports |
| **Desautels et al., 2016**          | MIMIC‑II vitals & labs                    | Gradient boosting       | Early detection proof‑of‑concept                              |
| **Henry et al., 2015 – TREWScore**  | Real‑time EHR streams                     | Random forest           | Early warning for septic shock                                |
| **PhysioNet Sepsis Challenge 2019** | ICU time‑series data                      | LSTM, XGBoost, RF, etc. | Head‑to‑head benchmark of many ML models                      |

Typical ML pipeline:

```
Inputs:  Vitals + Labs + Demographics + Comorbidities
Models:  XGBoost, LSTM, Logistic Regression  
Datasets: MIMIC‑III, eICU, local EHR extracts
```

Performance is **site‑dependent**; requires local tuning and validation.

---

## 3. Quick Comparison

| Approach      | Sensitivity | Specificity | Practicality  | Comments                             |
| ------------- | ----------- | ----------- | ------------- | ------------------------------------ |
| **SIRS**      | High        | Low         | High          | Over‑alerts                          |
| **qSOFA**     | Low‑Mod     | High        | **Very** High | Good for triage, mortality predictor |
| **SOFA**      | Mod‑High    | High        | Medium        | Strong reference standard            |
| **ML Models** | Variable    | Variable    | Low–Medium    | Need continuous data & maintenance   |

---

## 4. Context‑Driven Recommendations

| Setting                     | Recommended Tool(s)                                               | Rationale                                                          |
| --------------------------- | ----------------------------------------------------------------- | ------------------------------------------------------------------ |
| **Low‑resource / bedside**  | **qSOFA** or **SIRS**                                             | No labs required; quick screen                                     |
| **ICU / EHR with labs**     | **SOFA** or Sepsis‑3 criteria                                     | Captures organ dysfunction; aligns with guidelines                 |
| **Advanced EHR / research** | Locally trained **ML model** (e.g., predicts 6–12 h before onset) | Potential for earlier detection but demands data science resources |

---
