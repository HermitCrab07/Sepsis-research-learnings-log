## COMPOSER (COnformal Multidimensional Prediction Of SEpsis Risk)

| Aspect | Summary |
|--------|---------|
| **Goal** | Build a *deep‐learning early‑warning system* that not only predicts sepsis but also detects when incoming data look unfamiliar and safely outputs “indeterminate” instead of a spurious alert. |
| **Key idea** | Couples a standard sepsis‑risk network with a **conformal out‑of‑distribution detector**. If the patient’s feature vector doesn’t conform to the model’s training distribution (e.g., new device artefacts, missing values, drift), COMPOSER withholds a prediction—reducing false alarms. |
| **Inputs** | Real‑time EHR vitals, labs and demographics from multi‑hospital adult ICU/ward cohorts. |
| **Performance** | AUROC ≈ 0.95 at 4 h before clinical recognition; *indeterminate* flag rate ~12 %, cutting false‑positive alerts ~50 % compared with a baseline LSTM.|
| **Impact study** | 2024 deployment (Npj Digital Medicine): COMPOSER alerts were linked to **↓ mortality** and **↑ sepsis‑bundle compliance** in prospective hospital use.|
| **Take‑away** | COMPOSER shows that pairing prediction with **uncertainty awareness** can make hospital AI safer and more trusted by clinicians. |

---

## SERA (Sepsis Early Risk Assessment)

| Aspect | Summary |
|--------|---------|
| **Goal** | Create an AI model that fuses **structured EHR data and unstructured clinical notes** to improve early sepsis detection in the ward/ICU. |
| **Architecture** | Two‑branch network: <br>• tabular branch (vitals, labs, meds) <br>• NLP branch that embeds nursing + physician notes; branches are concatenated and passed to gradient‑boosted trees. |
| **Key findings** | Adding text features lifted AUROC by ~0.04 and caught sepsis a median 5 h earlier versus structured‑only baselines in a multi‑centre validation. |
| **Data** | 200 k encounters across several US academic hospitals; note vocabulary ~30 k tokens; training uses ICU and ward data. |
| **Clinical position** | Authors argue SERA augments—rather than replaces—bedside scoring tools, surfacing “high‑risk” patients for focused review. |
| **Paper** | Nature Communications (2021): *Artificial intelligence in sepsis early prediction and diagnosis using structured and unstructured data*. |
| **Take‑away** | Free‑text progress notes carry additive signal; hybrid models like SERA capture it without sacrificing real‑time deployability. |

---

### References  

1. Reyna, M. et al. “Artificial intelligence sepsis prediction algorithm learns to say ‘I don’t know.’” *NPJ Digital Medicine* (2021).   
2. Finlay, A. et al. “Impact of a deep learning sepsis prediction model on quality of care: prospective evaluation of COMPOSER.” *NPJ Digital Medicine* (2023).  
3. Zhang, Y. et al. “Artificial intelligence in sepsis early prediction and diagnosis using structured and unstructured data (SERA).” *Nature Communications* (2021).  
