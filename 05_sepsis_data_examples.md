Here are several well-known, publicly accessible ICU/EHR datasets we can tap for sepsis research beyond the PhysioNet/CinC 2019 (Kaggle) set:

1. **MIMIC-III (Medical Information Mart for Intensive Care, v1.4)**

   * \~60,000 ICU stays (2001–2012) from Beth Israel Deaconess Medical Center
   * Rich time-stamped vitals, labs, interventions, notes—widely used for Sepsis-2 and Sepsis-3 studies
   * Access via PhysioNet after CITI training and data use agreement

2. **MIMIC-IV (v1.0+)**

   * Successor to MIMIC-III, extends through 2019 with enhanced data model
   * Includes ICU and hospital-wide encounters plus more granular lab and device data
   * Ideal for updated Sepsis-3 labeling and algorithmic benchmarking

3. **eICU Collaborative Research Database**

   * \~200,000 ICU admissions (2014–2015) across 335 U.S. ICUs
   * Multi-center diversity helps test generalizability and transportability of sepsis models
   * Similar access process via PhysioNet

4. **HiRID (High-Resolution ICU Dataset)**

   * \~33,000 ICU stays from Bern University Hospital (2008–2016)
   * 1-minute resolution vitals and interventions—excellent for modeling time-varying treatments and confounders
   * Available through PhysioNet under a research license

5. **AmsterdamUMCdb**

   * \~23,000 ICU admissions (2003–2016) from Amsterdam UMC
   * Covers ICU and high-dependency units with detailed physiology and medication data
   * Accessible via Data Use Agreement with the Amsterdam Medical Data Science group

6. **Pediatric ICU Datasets** (e.g., PICqDP)

   * Various children’s hospital databases with sepsis cases in pediatric populations
   * Useful if you need to study age‐specific presentations or interventions

7. **Emory Critical Care Dataset (Emory CRD)**

   * Regional U.S. health-system ICU data with diverse patient demographics
   * Includes structured EHR plus some waveform data for advanced modeling

Follow each repository’s governance process (CITI training, DUAs) to gain access.

