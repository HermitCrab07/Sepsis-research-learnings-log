# Sepsis-research-learnings-log
Research, literature reviews, and Kaggle‑based learnings toward a multi‑modal sepsis detection pipeline

# Sepsis Research Log

Early‑stage, open notebook of everything I’m learning on the road to a **multi‑modal (clinician notes + lab values) sepsis‑detection pipeline**.  
This repo is public and **contains no patient‑level MIMIC data**—only literature notes, Kaggle‑based experiments, and reproducible code stubs.

---

## ✨ Why this repo exists
* Track key papers and implementation take‑aways in one place.  
* Feature‑engineering code on fully public datasets before touching restricted MIMIC notes.  
* Foundation that I can **later mirror (private)** when sensitive data i.e., MIMIC-IV enters the workflow.

---

## 📁 Repository layout
```text
sepsis-research-log/
├── README.md            ← you are here
├── LICENSE              ← MIT
├── .gitignore           ← excludes data/ & large files
│
├── literature/          ← one Markdown summary per paper
│   ├── 2025-07-15_composer.md
│   └── 2024-12-01_sera.md
│
├── notebooks/           ← exploratory Jupyter notebooks
│   └── kaggle_eda.ipynb
│
├── data/                ← _git‑ignored_ local CSV / Parquet
│   └── kaggle/          ← place downloaded Kaggle files here
│
└── misc/
    └── lessons_learned.md
