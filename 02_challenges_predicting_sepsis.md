# Challenges predicting sepsis

- Setup (import config)
  
- Defining “sepsis”: label ambiguity (SIRS vs Sepsis‑3, onset time)
  - Sepsis labels have tremendous ambiguity
  - Clinician judgment
    
- Data issues: missingness, irregular sampling, delayed charting
  - For at least one main dataset, there are 40 - 50 features
  - But most of these are missing values
  - Only 5 have data for 90%
    
- Treatment leakage (labs ordered because patient is sick)
  - Not sure I understand Treatment leakage
    
- Class imbalance / prevalence drift
  - Definite class imbalance
    
- Lead time definitions (predict @6h? @12h?)
  - Not clear at what time point to predict on?
    
- External validity (site differences, LMIC transfer)
  - Hugely important issue
  - Site differences and hospital differences
  - What happens in different countries etc?
    
- Implications for modelling strategy
  - Everything above has modeling implications

#
