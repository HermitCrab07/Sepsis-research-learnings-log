# Challenges predicting Sepsis - although sepsis is extremely serious, it's hard to predict. Some reasons are as follows:
  
## 1. Project Context 
  - Builds on *Sepsis Basics* notes (please also review the next notebook that shares the current SOTA models). 
  - Goal: multi-modal early warning - labs + clinician notes (multi-modal because just labs predict very little).

## 2. Label Ambiguity (if sepsis labels are not accurate, the models will not be either) - so here are some challenges with Sepsis Label Accuracy
  - Sepsis LABELS are difficult to define and often not accurate. To begin with, defining sepsis is difficult i.e., there are different definitions (SIRS, Sepsis-2 or 3, SOFA ≥2). There is a lack of a Gold Standard: Sepsis lacks a definitive diagnostic test, making its identification heavily reliant on clinical judgment and consensus definitions like Sepsis-3. This reliance can introduce variability and subjectivity into labeling.
  - Circular Reasoning in Labeling: Many machine learning models use features such as SOFA scores or vital signs to predict sepsis, yet these features are often part of the criteria used to label sepsis cases. This overlap can lead to models that merely replicate the labeling criteria rather than uncovering new predictive patterns. This is a serious issue.
  - Variability Across Institutions: Differences in clinical practices, documentation standards, and patient populations across hospitals lead to inconsistencies in sepsis labeling. This affects the generalizability of predictive models and will not have good external validation, which is why some sepsis prediction models have demonstrated poor performance when validated outside their development settings. This raises concerns about the robustness of the underlying labels and models. 
  - Second, the question is do the labels lag clinical reality? In other words, are the labs ordered BECAUSE the clinician suspects sepsis? Clinician judgment is essentially subjective and takes into account several things over the history of the patient - all of which may not be captured in the labs and this makes complete clinician notes essential to good sepsis prediction.


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

# 10. Final Thoughts
  - Machine learning models for early sepsis detection often achieve high accuracy retrospectively but can fail or mislead in practice because they learn features that directly encode the label definition rather than genuine early warning signals. 
  - Research has demonstrates that when ground-truth sepsis labels derive from consensus clinical criteria (e.g., certain vital sign thresholds), and those same measurements appear as input features, models simply reconstruct the definitional criteria instead of capturing causal precursors.
  - Such models may show excellent retrospective AUROC yet perform poorly when deployed in settings where some measurements are delayed or missing, or when clinical workflows differ. 
  - Without a causal framing—explicitly mapping which features causally precede sepsis onset versus which are artifacts of the diagnostic criteria—developers risk building systems that “predict” sepsis only at or after onset rather than enabling true early intervention. 
  - A causal-inference approach would start by building a structural model of how physiological processes lead to sepsis, then identify interventions or surrogate markers that precede the consensus criteria, guiding data collection and validation in prospective studies.

# 11. Efforts to Improve Labeling Accuracy
- Expert Consensus Labeling: Initiatives like the Ground Truth for Sepsis Questionnaire (GTSQ) involve daily assessments by experienced clinicians to provide more reliable sepsis labels, aiming to reduce subjectivity and enhance consistency. ([BioMed Central][1])
- Harmonized Multi-Center Datasets: Projects that integrate data from multiple international centers, applying standardized definitions and rigorous validation protocols, are working towards creating more reliable and generalizable sepsis datasets. ([PMC][2])

# 12. Recommendations for Researchers and Clinicians
- Critical Evaluation of Labels: When developing or utilizing predictive models, it's essential to scrutinize the origin and criteria of sepsis labels to ensure they align with the intended clinical application.
- Incorporate Clinical Expertise: Engaging clinicians in the labeling process can enhance the accuracy and relevance of sepsis annotations, especially in complex or ambiguous cases.
- Prioritize External Validation: Testing models across diverse patient populations and healthcare settings can help assess their robustness and adaptability, ensuring they perform reliably in real-world scenarios.

In summary, while sepsis labels in existing datasets provide a foundation for research and model development, their accuracy is not absolute. Ongoing efforts to refine labeling practices and validate models externally are crucial for advancing sepsis prediction and improving patient outcomes.

[1]:https://translational-medicine.biomedcentral.com/articles/10.1186/s12967-022-03228-7?utm_source=chatgpt.com "Ground truth labels challenge the validity of sepsis consensus ..."
[2]: https://pmc.ncbi.nlm.nih.gov/articles/PMC10425671/?utm_source=chatgpt.com "Predicting sepsis using deep learning across international sites"

