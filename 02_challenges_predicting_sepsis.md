# Challenges predicting Sepsis - although sepsis is extremely serious, it's hard to predict. Some reasons are as follows:
  
## 1. Project Context 
  - Builds on *Sepsis Basics* notes (please also review the next notebook that shares the current SOTA models). 
  - Goal: multi-modal early warning - labs + clinician notes (multi-modal because just labs predict very little).

## 2. Label Ambiguity (if sepsis labels are not accurate, the models will not be either)
  - Fair to say that (though I'm no sepsis  expert) the sepsis LABELS are difficult to define and often not accurate. 
  - Defining sepsis is difficult i.e., there are different definitions (SIRS alerts, Sepsis-2 or 3, SOFA ↑ ≥2)
  - Furthermore, question is do administrative labels lag clinical reality?
  - For ML we need an onset timestamp rule; definition choice affects labels & prevalence.
  - Clinician judgment is essentially subjective and takes into account several things - all of which may not be captured.

## 3. Onset Time Definition
  - True biologic onset unknown; we proxy with first antibiotics + cultures + vitals?
  - Charting delay (documented time ≠ physiologic time).
  - Lead time calculation depends on this anchor.
  - Data issues: missingness, irregular sampling, delayed charting(?)
    - For at least one dataset, there are 40 - 50 features which seems like a rich source
    - But most of these are missing values (90% missing data)
    - Only 5 features have data for 88% - 93%
    - Clinicians and hospitals use these 5 to predict sepsis, but models based on these 5 don't predict sepsis well (in fact, very badly).

## 4. Data Quality & Missingness
  - Irregular sampling; vitals not charted at fixed intervals.
  - Informative missingness (tests ordered when concern is high - how would we know?).
  - Backfilled chart times (entered later) distort time series.
  - Prevalence drift (suspecting this is an issue, but not sure).

## 5. Treatment Leakage (important distinction - were the labs ordered because clinician suspected sepsis?)
  - Labs (e.g., lactate draw) often triggered *because* clinician suspects sepsis.
  - Models may “predict” sepsis by learning post-suspicion orders.
  - Need causal strategy: censor post‑suspicion actions or encode them separately.

## 6. Class Imbalance & Prevalence Drift
  - Sepsis cases are much less than total admissions which leads to imbalance.
  - Prevalence shifts over years. Definitions have changed. 
  - Calibration (at each hospital) required for deployment.

## 7. Lead-Time Target
  - Clinical utility: alert ≥6h before shock? Maybe 12h window? Question for domain expert.
  - Earlier alerts = noisier signals = expensive to follow-up if wrong.

## 8. External Validity 
  - Data I used is from a variety of centers in US and doesn't mean it's representative of say LMIC hospitals (labs availability, etc).
  - Domain shift in measurement frequency & antibiotic usage.
  - Need minimal-feature models for transfer.
  - External validity (site differences, LMIC transfer)
    - Hugely important issue
    - Site differences and hospital differences

## 9. Overall Modelling & Evaluation Implications
  - Time-series features + clinician's notes + accurate sepsis flags are critical.
  - Train/test split by hospital stay time period to test drift.
  - Report usual metrics, but also consider the impact of false alerts which is a burden on hospitals.

#
