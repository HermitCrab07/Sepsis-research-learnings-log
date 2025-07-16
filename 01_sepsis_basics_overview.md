# Sepsis Basics Overview  
*A concise clinical primer based on “Early Prediction of Sepsis From Clinical Data: The PhysioNet/Computing in Cardiology Challenge 2019” and related sources.*

---

## 1. What Is Sepsis & Why It Matters
> **Sepsis** is a life‑threatening organ‑dysfunction syndrome triggered by an infection and the host’s dysregulated immune response.  
>
> *United States*: ~ 1.7 M cases / yr → 270 K deaths; > ⅓ of all in‑hospital deaths.  
> *Global*: ~ 30 M cases / yr → 6 M deaths.  
> *Cost*: US hospital spend ≈ \$24 B / yr (13 % of national inpatient costs).  
> *Burden*: highest for patients who *develop* sepsis during admission and in low‑resource settings.

---

## 2. Typical Infection Sources → Sepsis

| Body system | Common focus of infection |
|-------------|---------------------------|
| **Lungs** | Pneumonia *(most frequent sepsis trigger)* |
| **Urinary tract** | Pyelonephritis, complicated UTIs |
| **Abdomen** | Appendicitis, perforated bowel, peritonitis |
| **Skin / soft tissue** | Cellulitis, infected wounds, pressure ulcers |
| **Bloodstream** | Catheter or IV‑line infections |
| **Reproductive** | Infected miscarriage, postpartum endometritis |

**High‑risk situations:** recent surgery, indwelling devices, immunosuppression (chemo, HIV, diabetes), chronic organ disease, extremes of age.

---

## 3. Pathophysiology in a Nutshell
1. **Infection detected** → immune mediators released.  
2. **Cytokine cascade** → widespread inflammation.  
3. **Capillary leak + vasodilation** → hypotension.  
4. **Poor perfusion (↑ lactate)** → organ injury.  
5. **Progression**: Sepsis → Septic shock if fluids + vasopressors fail to restore pressure.

Early IV fluids + broad‑spectrum antibiotics are critical; every hour of delay increases mortality risk.

---

## 4. Sepsis‑3 (2016) Definitions & Core Markers

*Sepsis =* suspected/confirmed infection **plus** increase in SOFA ≥ 2.  
*Septic shock =* sepsis **plus** persisting hypotension requiring vasopressors **and** lactate ≥ 2 mmol/L.

### Systemic signs

- Temp ≥ 38 °C or < 36 °C  
- HR > 90 bpm  
- RR > 22 /min  
- Altered mental status  
- SBP < 100 mmHg  
- WBC > 12 K or < 4 K  
- Lactate ≥ 2 mmol/L  
- Evidence of organ dysfunction (low urine, high creatinine, ↑ bilirubin, thrombocytopenia)

### Site‑specific early clues
| Likely source | Early lab / imaging pattern |
|---------------|----------------------------|
| Urinary | ↑ creatinine (kidney stress) |
| Pulmonary | ↓ SpO₂, abnormal CXR |
| Abdominal | ↑ AST / ALT, amylase |
| Skin | ↑ CRP / ESR without organ‑specific labs |

---

## 5. Step‑by‑Step Diagnostic Workflow

1. **Suspect infection** (Pneumonia? UTI? Cellulitis? …)  
2. **Check systemic symptoms** — fever/low temp, tachycardia, tachypnea, hypotension, confusion.  
3. **Order labs**  
   - CBC (WBC count)  
   - Lactate, procalcitonin, CRP/ESR  
   - Blood cultures  
   - Organ panels: creatinine, LFTs, platelets, urine output  
4. **Assess organ dysfunction**  
   - Persisting low BP despite fluids  
   - Oliguria, hypoxemia, altered GCS  
5. **Calculate a score** (qSOFA at bedside; full SOFA in ICU).  

Sepsis remains a **clinical judgement**: infection + systemic response + organ stress.

---

## 6. Algorithmic Detection: Clinical Scores vs ML

### Established bedside/ICU scores
| Tool | Sensitivity | Specificity | Practicality | Notes |
|------|-------------|-------------|--------------|-------|
| **SIRS** | High | Low | Very easy | Many false positives |
| **qSOFA** | Low–Mod | High | Bedside 3‑variable | Better mortality flag than early detector |
| **SOFA (full)** | Mod–High | High | Needs labs | Standard in Sepsis‑3 |

### Machine‑learning approaches
| Model type | Inputs | Example studies |
|------------|--------|-----------------|
| Proprietary EHR (Epic Sepsis Model) | Vitals, labs, demographics | Widely deployed |
| Random Forest / XGBoost | MIMIC‑III, eICU vitals/labs | Desautels 2016; TREWScore (Henry 2015) |
| LSTM / time‑series deep nets | Hourly vitals & nursing notes | PhysioNet Sepsis 2019 Challenge top entries |

**Choosing “best” depends on context**

| Setting | Recommended approach |
|---------|----------------------|
| Bedside, low‑resource | SIRS or qSOFA |
| ICU with full labs | SOFA + Sepsis‑3 |
| Research / advanced EHR | Locally trained ML model validated 6–12 h pre‑onset |

---

## 7. Key Take‑aways

* Sepsis = **systemic** response; infection site mainly guides source control.  
* Early, accurate detection drives lives saved & cost reduction.  
* Robust prediction models blend **clinical insight** + high‑quality multivariate data + rigorous validation.  
* Choice of algorithm must balance sensitivity, specificity, and practical deployability for the target setting.


## 8. How Sepsis Is Diagnosed — A Step‑by‑Step Pattern

> **No single “sepsis test” exists.**  
> Clinicians combine (1) infection evidence + (2) systemic response + (3) organ dysfunction markers.

### 8.1 Suspect or Confirm Infection
* Ask: Does the patient have **pneumonia, UTI, skin, abdominal, or other infection?**

---

### 8.2 Systemic Symptoms  
| Vital / Symptom | Typical threshold |
|-----------------|-------------------|
| **Fever / hypothermia** | ≥ 38 °C or < 36 °C |
| **Heart rate** | > 90 bpm |
| **Respiratory rate** | > 20 /min (SIRS) or > 22 /min (qSOFA) |
| **Blood pressure** | SBP < 100 mmHg |
| **Neurologic status** | Confusion, altered mental state |
| **Other** | Chills, fatigue |

---

### 8.3 Laboratory Tests  
| Test | Rationale |
|------|-----------|
| **WBC count** | High or very low = immune stress |
| **Lactate** | Elevated → tissue hypoxia / poor perfusion |
| **Procalcitonin** | Often ↑ in bacterial sepsis |
| **CRP / ESR** | Non‑specific inflammation markers |
| **Blood cultures** | Identify causative organism |
| **Organ panels** | Creatinine (kidney), AST/ALT (liver), platelets, urine output |

---

### 8.4 Organ Dysfunction Red‑Flags
* Persisting **hypotension** despite fluids  
* **Hypoxemia** (low PaO₂/FiO₂)  
* **Oliguria** or anuria  
* **Confusion / GCS drop**  

---

### 8.5 Scoring Tools
| Score | Quick criteria | Usage |
|-------|----------------|-------|
| **qSOFA** | SBP ≤ 100 mmHg • RR ≥ 22 • GCS < 15 (≥ 2/3) | Bedside triage, mortality predictor |
| **SOFA (full)** | 6‑organ score (lungs, liver, kidneys, CNS, coag, CVS) | ICU; Sepsis‑3 gold standard |

*Patients meeting infection + ↑ SOFA ≥ 2 → **Sepsis**; add refractory hypotension + lactate ≥ 2 → **Septic shock**.*

---

## 9. Algorithmic Detection Landscape

### 9.1 Established Clinical Criteria

| Approach | Sensitivity | Specificity | Practicality | Notes |
|----------|-------------|-------------|--------------|-------|
| **SIRS** | High | Low | Very high | Over‑alerts |
| **qSOFA** | Low‑Mod | High | Extremely easy | Better at mortality than early detection |
| **SOFA** | Mod‑High | High | Medium (needs labs) | Current gold standard |

### 9.2 Machine‑Learning Models

| Model | Inputs | Dataset / Citation |
|-------|--------|--------------------|
| **Epic Sepsis Model** | Vitals, labs, demographics | Proprietary (multiple US hospitals) |
| **Random Forest / XGBoost** | Vitals + labs | *Desautels 2016* (MIMIC‑II) |
| **TREWScore** | Real‑time vitals | *Henry 2015* |
| **PhysioNet 2019 Challenge** | Time‑series vitals, meds | Benchmarked LSTMs, GBMs |

*Sensitivity/specificity vary by site & tuning; require local validation.*

---

### 9.3 Which Algorithm to Choose?

| Setting | Recommended tool |
|---------|------------------|
| **Bedside / low‑resource** | **SIRS** or **qSOFA** |
| **ED / General ward with labs** | **qSOFA + lactate** trigger |
| **ICU / EHR‑integrated** | **SOFA** or Sepsis‑3 definition |
| **Data‑rich health system** | Locally trained **ML model** validated 6–12 h pre‑onset |

---

## 10. Bottom Line

*Confirmed sepsis requires:*

1. Clear **infection source**  
2. **Systemic response** (vitals, labs)  
3. **Organ dysfunction** evidence  

> Sepsis remains a clinical judgement—algorithms assist but do not replace bedside evaluation.

---
*Last updated : 2025‑07‑16*
