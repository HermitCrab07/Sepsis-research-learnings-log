## Boring-but-Essentials MUST-DOs in Sepsis before beginning any Sepsis Agent Development Project:

1. **Encode a sepsis definition**
   What do we want to work with? SIRS, Sepsis‑3, or SEP‑1. How do we obtain a Timestamp of exactly when sepsis starts? How many datasets provide this information? How good is it?

2. **Normalize raw vitals/labs**
   Normalize units, naming, time zones, remove duplicates/outliers, and handle missing values. 

3. **Events must be on a single timeline**
   Orders, labs, vitals, notes — so “within 3 hrs / 6 hrs” comparisons are accurate.

4. **Build tables that track...**
   * Antibiotics
   * Fluids
   * Vasopressors
   * Culture orders

5. **Make sure encounters and transfers make sense (time wise)**
   Combine ED → floor → ICU into one continuous patient event history.

6. **Choose top 5-7 fields and Backfill missing context fields**
   Lactate redrawn? MAP <65? Use deterministic rules before any ML (obviously).

7. **Set up audit files - if we can get clinician data/notes from the MIMIC-IV files (to be seen)**
   Track alerts recorded, clinician responses at appropriate moments, and ground-truth outcomes for later evaluation.

---

## 1. Question: “Workflow Issues” = Are there Gaps where Care Falls Apart for whatever reason?

**Not *“Can we detect sepsis?”* but *“Where do teams miss steps after detection?”**

* Lactate not drawn (or not repeated)
* Blood cultures drawn after antibiotics
* Broad‑spectrum antibiotics delayed >3 hrs
* 30 mL/kg fluids never ordered or under-dosed
* No documented reassessment after fluids/pressors

> Would it be possible to define a Sepsis Agent to watch timestamps/orders and flag “missing/late” items - not sure if it's practical but can check.

---

## 2. Question: “Bundle Adherence” = Checking the Sepsis Bundle Boxes

**Typically refers to CMS SEP‑1 / Surviving Sepsis Campaign bundles**:

* **Initial (within 3 hrs):**

  * Lactate
  * Blood cultures before antibiotics
  * Broad‑spectrum antibiotics
  * Fluids (if hypotension or lactate ≥4)

* **Within 6 hrs:**

  * Vasopressors (if MAP <65)
  * Repeat lactate
  * Hemodynamic reassessment

> **Adherence** = % of patients who got each required element on time.

---

## 3. Question: How to Learn What Tools Hospitals Already Use

* **Literature & conference posters**:
  Search terms: `"electronic sepsis alert"`, `"sepsis bundle compliance tool"`, `"Epic Sepsis Model"`, `"Cerner St. John Sepsis Agent"`
* **Regulatory/quality reports**:
  CMS SEP‑1 public data, hospital QI abstracts
* **Vendor docs / press releases**:
  Epic, Oracle Cerner, MEDITECH, Philips, GE
* **Clinician communities**:
  r/medicine, r/criticalcare, ACP/HIMSS talks, LinkedIn groups
* **FOIA / 510(k) database**:
  Check for FDA-cleared CDS tools

---
---

# Is Sepsis a Good Project to Do? **Potentially yes** — but only if:

* We’re clear on the **pain point** we’re solving (beyond “just another alert”)
* We’ve accounted for **data quality, evaluation, and workflow**

Otherwise, we are building **another high–false-positive buzzer**.

---

## Why It *Can Be* a Good Project

* **High-impact**: Common, lethal, time-critical
* **Measurable**: Time-to-antibiotics, bundle compliance, mortality
* **Rich data**: Vitals, labs, notes, orders — esp. in ICUs/EDs

---

## Why It’s Tricky

* **Definition drift**: SIRS vs. Sepsis-3 vs. local 
* **Alert fatigue**: Existing popups already flood clinicians
* **Generalizability issues**: Models don’t port well across hospitals
* **Regulatory/Legal**: SaMD territory if recommending therapy
* **Data access/governance**: PHI, IRBs, audit trails (complex)

---

## Why We should Try

* We can **improve precision/recall** over current rules and explain why
* We **target a workflow gap**, not just detection
* We plan to **validate prospectively** (silent mode)
* We monitor model **drift**, trust, and adoption

---

## Quick Checklist

| Area                    | Question                                                           |
| ----------------------- | ------------------------------------------------------------------ |
| **Problem Clarity**     | Is it detection, adherence, or explanation?                        |
| **Baseline Comparison** | Do you know current system performance + pain points?              |
| **Data & Labels**       | Do you have clean, time-stamped events to train/test on?           |
| **Evaluation Plan**     | Offline metrics + silent trial + care impact?                      |
| **Adoption Path**       | Who uses it, how do they interact with it, how do you build trust? |
| **Reg/QA Plan**         | Documentation, monitoring, fallback, bias checks?                  |

---



