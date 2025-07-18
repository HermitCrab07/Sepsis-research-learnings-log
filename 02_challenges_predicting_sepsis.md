# Challenges predicting Sepsis - although sepsis is extremely serious, it's hard to predict. Some reasons are as follows:
  
## 1. Project Context 
  - Builds on *Sepsis Basics* notes (please also review the next notebook that shares the current SOTA models). 
  - Goal: multi-modal early warning - labs + clinician notes (multi-modal because just labs predict very little).

## 2. Label Ambiguity (if sepsis labels are not accurate, the models will not be either)
  - Fair to say that (although I'm no sepsis  expert) sepsis LABELS are difficult to define and (I suspect) often not accurate. There is research on this issue.
  - Say this because first of all - defining sepsis is difficult i.e., there are different definitions (SIRS, Sepsis-2 or 3, SOFA ≥2)
  - Second, the question is do the labels lag clinical reality? In other words, are the labs ordered BECAUSE the clinician suspects sepsis?
  - Third, clinician judgment is essentially subjective and takes into account several things over the history of the patient - all of which may not be captured.

## 3. Onset Time Definition
  - True biologic onset time is often very hard to know even for the clinicians. Predicting sepsis is a challenge for various reasons.
  - How well is this captured on the charts? What if the documented time ≠ actual onset or the physiologic time?
  - For example, there are a bunch of data issues: missingness, irregular sampling, delayed charting in the dataset I worked with:
    - There are 40 - 50 features which seems like a rich source
    - But most of these are missing values (90% missing data)
    - Only 5 features have data for 88% - 93%
    - Clinicians and hospitals use these 5 to predict sepsis
    - Models based on these 5 don't predict sepsis well (in fact, very badly).
    - Furthermore, as mentioned before, we don't know if a lab was ordered BECAUSE the clinician suspected sepsis.

## 4. Data Quality & INFORMATIVE Missingness (i.e., missingness is not at random, I don't think. It's more likely than not Missing Not at Random)
  - Informative missingness (tests are ordered when concern is high)
  - Impossible to know the reason behind the tests (unless the data is pulled in from clinician's notes?).
  - Irregular sampling; vitals not charted at fixed intervals.
  - Backfilled chart times (entered later) distort time series.
  - Prevalence drift (suspecting this is an issue, but not sure). Example would be definitions shift over time and therefore prevalance changes. 

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
