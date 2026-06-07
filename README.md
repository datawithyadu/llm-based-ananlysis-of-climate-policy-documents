# 🌍 LLM-Based Analysis of Climate Policy Documents

> **Module:** AI, Power & Responsibility – Governing Intelligent Systems for Sustainability  
> **Dataset:** Real UNFCCC NDC 3.0 documents (10 countries) · ClimateBERT (HuggingFace)  
> **Model:** Claude Sonnet (`claude-sonnet-4-20250514`) via Anthropic API

---

## 📌 Overview

This project uses Large Language Models to analyse **Nationally Determined Contributions (NDCs)** — the official climate pledges submitted by countries under the Paris Agreement to the UNFCCC. Five research questions are investigated across dimensions of ambiguity, semantic alignment, commitment tracking, greenwashing risk, and climate justice language.

---

## 🗂️ Repository Structure

```
├── llm-based-analysis-of-climate-policy-documents.ipynb  # Main notebook
├── README.md
├── LICENSE
├── .gitignore
├── data/
│   └── ndc_urls.json              # All dataset sources + direct NDC PDF download links
├── figures/
│   ├── RQ1_Figure_1.pdf           # Ambiguity by region (bar chart)
│   ├── RQ2_Figure_2.pdf           # Semantic alignment radar chart
│   ├── RQ3_Figure_3.pdf           # Commitments by year (grouped bar)
│   ├── RQ4_Figure_4.pdf           # Greenwashing risk scatter plot
│   └── RQ5_Figure_5.pdf           # Climate justice by bloc (bar chart)
└── tables/
    ├── RQ1_Table_1.pdf            # Ambiguity data table
    ├── RQ2_Table_2.pdf            # Cosine similarity table
    ├── RQ3_Table_3.pdf            # Commitments count table
    ├── RQ4_Table_4.pdf            # Greenwashing scores table
    └── RQ5_Table_5.pdf            # Justice theme frequency table
```

---

## 🔬 Research Questions

### RQ1 — Policy Ambiguity Detection
**Can LLMs detect vague language in NDC climate policy documents?**

NDC paragraphs are classified as `SPECIFIC`, `VAGUE`, or `MIXED` using Claude zero-shot prompting with hedge phrase detection (e.g. *"shall endeavour"*, *"as appropriate"*, *"intends to"*).

| Region | Vague % | Specific % | Ambiguity Level |
|--------|---------|------------|-----------------|
| Europe | 22% | 78% | Low |
| East Asia | 45% | 55% | Moderate |
| South Asia | 55% | 45% | Moderate |
| Latin America | 60% | 40% | High |
| Sub-Saharan Africa | 70% | 30% | High |
| Middle East | 75% | 25% | Very High |

[📊 Figure 1](figures/RQ1_Figure_1.pdf) · [📋 Table 1](tables/RQ1_Table_1.pdf)

---

### RQ2 — Semantic Alignment Across Countries
**How semantically similar are NDC mitigation sections to the global mean?**

TF-IDF embeddings are computed on real NDC text, and cosine similarity is measured against the global mean mitigation vector. Reference: IGES NDC Database for country metadata.

| Code | Country | Cosine Similarity | Interpretation |
|------|---------|-------------------|----------------|
| WSM | Samoa | 1.00 | Highest alignment |
| ARM | Armenia | 0.98 | Very high |
| PLW | Palau | 0.98 | Very high |
| SAU | Saudi Arabia | 0.81 | High |
| GEO | Georgia | 0.75 | Moderate |
| SLE | Sierra Leone | 0.75 | Moderate |
| KOR | South Korea | 0.71 | Moderate |
| COL | Colombia | 0.00 | Lowest alignment |

[📊 Figure 2](figures/RQ2_Figure_2.pdf) · [📋 Table 2](tables/RQ2_Table_2.pdf)

---

### RQ3 — Time-Bound Commitment Extraction
**How do time-bound commitments evolve across NDC rounds?**

Claude extracts explicit time-bound commitments from NDC text across three submission rounds (NDC 1.0, 2.0, 3.0) for 7+7+9 countries. Cross-referenced with Climate Watch NDC Data.

| Target Year | NDC 1.0 | NDC 2.0 | NDC 3.0 |
|-------------|---------|---------|---------|
| 2025 | 2 | 2 | — |
| 2030 | 7 | 5 | 7 |
| 2035 | — | 3 | 8 |
| 2040 | — | 7 | 7 |
| 2050 | 5 | 4 | 6 |

[📊 Figure 3](figures/RQ3_Figure_3.pdf) · [📋 Table 3](tables/RQ3_Table_3.pdf)

---

### RQ4 — Greenwashing Risk Scoring
**Can LLMs identify performative vs. substantive climate commitments?**

Each NDC is scored on a 0–1 greenwashing risk scale (`0 = substantive`, `1 = performative`) and cross-referenced against verified emissions reduction targets (IEA). Pearson r = -0.03 (p = 0.938), indicating no significant correlation.

| Code | Country | Risk Score | Emissions Red. % | Risk Level |
|------|---------|------------|------------------|------------|
| GEO | Georgia | 0.45 | 41% | Medium |
| ARM | Armenia | 0.44 | 35% | Medium |
| KOR | South Korea | 0.52 | 31% | Medium |
| COL | Colombia | 0.57 | 28% | Medium |
| IND | India | 0.55 | 22% | Medium |
| SLE | Sierra Leone | 0.57 | 18% | Medium |
| WSM | Samoa | 0.41 | 12% | Medium |
| NRU | Nauru | 0.58 | 10% | Medium |

[📊 Figure 4](figures/RQ4_Figure_4.pdf) · [📋 Table 4](tables/RQ4_Table_4.pdf)

---

### RQ5 — Climate Justice Language by Negotiating Bloc
**Do climate justice themes appear differently across UNFCCC negotiating blocs?**

Lexicon tagging identifies four justice themes across NDC text: Loss & Damage, Intergenerational Equity, Gender Justice, and Indigenous Rights. Spearman rho vs World Bank GDP = -0.20 (p = 0.606).

| Negotiating Bloc | Loss & Damage | Intergenerational Equity | Gender Justice | Indigenous Rights |
|------------------|--------------|--------------------------|----------------|-------------------|
| G77+China | 3.0 | 3.0 | 1.0 | 1.0 |
| BASIC | 4.0 | 2.0 | 1.0 | 1.0 |
| East Asia | 3.0 | 50.0 | 96.0 | 8.0 |
| African Group | 23.0 | 12.5 | 20.0 | 5.0 |
| Europe/Umbrella | 5.5 | 4.5 | 27.5 | 4.0 |
| AOSIS/SIDS | 25.5 | 1.0 | 19.5 | — |

[📊 Figure 5](figures/RQ5_Figure_5.pdf) · [📋 Table 5](tables/RQ5_Table_5.pdf)

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| `anthropic` | Claude API for LLM classification & scoring |
| `pdfplumber` | PDF text extraction from NDC documents |
| `scikit-learn` | TF-IDF vectorisation, cosine similarity, F1 scoring |
| `scipy` | Pearson r, Spearman rho, Kruskal-Wallis tests |
| `matplotlib` | All figures and tables |
| `HuggingFace datasets` | ClimateBERT `climate_specificity` few-shot examples |
| `pandas / numpy` | Data processing |

---

## 📂 Datasets

> Raw NDC PDFs are not included due to copyright and file size. Use `data/ndc_urls.json` for direct download links.

| Dataset | Source | Used In |
|---------|--------|---------|
| UNFCCC NDC Registry | [unfccc.int/NDCREG](https://unfccc.int/NDCREG) | RQ1–RQ5 |
| ClimateBERT `climate_specificity` | [HuggingFace](https://huggingface.co/datasets/climatebert/climate_specificity) | RQ1 |
| IGES NDC Database | [iges.or.jp](https://www.iges.or.jp/en/pub/iges-ndc-database/en) | RQ2 |
| Climate Watch NDC Data | [climatewatchdata.org](https://www.climatewatchdata.org/ndcs) | RQ3 |
| IEA Emissions Data | [iea.org](https://www.iea.org/data-and-statistics) | RQ4 |
| World Bank GDP | [data.worldbank.org](https://data.worldbank.org/indicator/NY.GDP.MKTP.CD) | RQ5 |

**Countries analysed (NDC 3.0):** India (IND), Saudi Arabia (SAU), South Korea (KOR), Colombia (COL), Sierra Leone (SLE), Armenia (ARM), Georgia (GEO), Palau (PLW), Samoa (WSM), Nauru (NRU)

---

## ⚙️ Setup & Usage

### On Kaggle
1. Add your Anthropic API key as a Kaggle Secret named `ANTHROPIC_API_KEY`
2. Run all cells — PDFs are downloaded automatically from UNFCCC

### Locally
```bash
pip install -r requirements.txt
export ANTHROPIC_API_KEY=your_key_here
jupyter notebook llm-based-analysis-of-climate-policy-documents.ipynb
```

---

## 📄 License

MIT License — see [LICENSE](LICENSE) for details.
