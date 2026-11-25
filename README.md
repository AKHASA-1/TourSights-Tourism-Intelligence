# 🌍 TourSights — Tourism Intelligence

> **Shifting the Focus from Tourist Volume to Tourist Value through Data-Driven Micro-Experience Analytics.**

TourSights is an academic **Business Intelligence and Natural Language Processing proof of concept** that turns publicly available Google Maps visitor reviews of selected Egyptian museums and archaeological sites into structured, comparable tourism insights.

The project combines data collection, Python-based data preparation, multilingual sentiment analysis, aspect-based experience categorization, and an interactive Power BI Desktop report. Its goal is to help decision-makers explore what visitors appreciate, what frustrates them, and which recurring experience issues may deserve further investigation.

**TourSights focuses on the quality of individual visitor experiences—not only tourist volume or overall star ratings.**

> **Project status:** Academic prototype. It is not a deployed national monitoring platform, an official government system, or a commercial product.

---

## 📌 Project Overview

Online reviews contain detailed accounts of visitor experiences: ticket prices, queues, cleanliness, accessibility, staff and vendor behaviour, facilities, and the historical or cultural experience. However, this information is unstructured, multilingual, and difficult to compare manually across destinations.

TourSights processes Google Maps reviews into an analytical data model and makes the resulting information explorable through Power BI Desktop.

The **primary intended stakeholder** is the Egyptian Ministry of Tourism and Antiquities. Destination managers, tourism analysts, and researchers are potential secondary beneficiaries. This identifies the project's intended audience; it does not imply institutional adoption, approval, or endorsement.

---

## 🎯 Problem Statement

Visitor numbers and average ratings do not fully explain the quality of a destination experience. Recurring friction points can remain hidden in thousands of individual reviews.

TourSights addresses this analytical gap by helping users:

- Explore recurring positive and negative visitor experiences.
- Identify which experience aspects are discussed in reviews.
- Compare destinations using clearly defined measures and denominators.
- Examine sentiment and aspect patterns over time where dates allow.
- Trace aggregated findings back to review-level evidence.
- Distinguish observed review patterns from assumptions or unsupported claims.

The analysis is intended to support investigation and informed discussion—not to replace expert judgment or automatically prescribe interventions.

---

## 🏛️ Destination Scope

The current analytical dataset covers five Egyptian destinations:

| Destination | Dataset label | Destination type |
|---|---|---|
| Abu Simbel Temples | Abu Simbel | Temple complex |
| Karnak Temple Complex | Karnak | Temple complex |
| Giza Pyramids Complex (Pyramids of Giza & Sphinx) | Giza | Pyramids and necropolis |
| Valley of the Kings | Valley of Kings | Royal necropolis |
| Grand Egyptian Museum | GEM | Museum |

The dataset's destination dimension contains five destination records. Other locations appearing in archived or backup source files are not part of the current five-destination analytical scope.

---

## 📊 Dataset Snapshot

The current `Main Dataset.xlsx` contains the consolidated analytical model and supporting documentation/validation sheets.

| Measure | Current value |
|---|---:|
| Destinations | 5 |
| Review records (`FactReviews`) | 25,398 |
| Reviews containing text | 11,418 |
| Reviews without text | 13,980 |
| Review-aspect records (`FactReviewAspects`) | 25,979 |
| Distinct reviews represented in the aspect table | 11,023 |
| Defined experience aspects | 14 |
| Arabic-language text reviews | 1,612 |

**How to read these figures**

- A review can be associated with more than one aspect. Therefore, aspect-record counts are not unique-review counts.
- Not every text review receives an aspect assignment. Reviews without a detected specific aspect remain in the review-level fact table.
- Star-only reviews are retained as review records but do not provide text for sentiment or aspect analysis.
- These are dataset snapshot counts, not estimates of all visitors or all reviews published about the destinations.

---

## 🗺️ Data Source and Collection

**Current review platform: Google Maps only.**

The project uses Google Maps visitor reviews to focus on individual visitor experiences, including visits that may not be part of an organized tour or packaged activity.

The source workbooks were collected using the **Apify Google Maps Reviews Scraper**. The Python processing pipeline consumes five destination-specific Excel workbooks. The archive may also contain backup or unused location files; those should not be confused with the five destinations in the current analytical model.

Collection tools and platform access are subject to their respective terms, technical limits, and usage allowances. The project does not claim complete coverage of all reviews or all visitors.

---

## 🔄 Analytical Workflow

```text
Google Maps Public Reviews
          |
          v
Apify Google Maps Reviews Scraper
          |
          v
Destination-Specific Excel Workbooks
          |
          v
Python Processing Pipeline
  - Load and standardize source fields
  - Clean and normalize review text
  - Build destination and date dimensions
  - Detect review language
  - Apply sentiment classification
  - Apply aspect-based categorization
  - Generate data-quality flags
  - Run integrity checks
          |
          v
Structured Analytical Tables
          |
          v
Main Dataset.xlsx
          |
          v
Power BI Desktop
  - Data model and relationships
  - DAX measures
  - Interactive report pages
          |
          v
Exploration of Visitor-Experience Insights
```

The Python pipeline is implemented in the repository's `.py` source file and Jupyter notebook. The Excel workbook also contains supporting documentation, validation, gold-label, and insights sheets. Not every workbook sheet is generated by the Python export step.

---

## 🧠 NLP and Aspect-Based Analysis

TourSights uses a rule-based and hybrid text-analysis pipeline designed for the review data available in the project.

### Sentiment Analysis

The pipeline assigns review-level and text-level sentiment information. The current analytical labels include:

- Positive
- Negative
- Neutral
- Mixed, where applicable in the validation/reference material
- No Text for reviews without review text

The implementation includes English sentiment vocabulary and decision rules, as well as a dedicated Arabic hybrid layer. Sentiment outputs are analytical classifications and may contain errors; they should not be treated as ground truth.

### Aspect-Based Experience Categorization

The current model defines 14 visitor-experience aspects. They cover themes such as:

- Crowding and Queues
- Pricing and Value
- Staff and Guides
- Cleanliness
- Accessibility
- Historical Experience
- Ticketing and Booking
- Other defined experience categories documented in `DimAspect`

A single review may mention multiple aspects. The aspect table therefore stores review–aspect records rather than one row per review.

### Validation

The workbook includes manually labelled reference samples and validation sheets for sentiment and aspect analysis. The current gold-label material documents **360 sentiment-labelled reviews** and **192 aspect labels**. Consult the `NLP_Accuracy`, `Gold_Sentiment`, and `Gold_Aspects` sheets for the evaluation setup and measured results.

The Arabic hybrid comparison sheet records changes between pipeline versions for Arabic-language reviews. These comparisons are documented separately from the general gold-sample evaluation.

---

## 🗃️ Data Model

The analytical model is organized around two fact tables and three dimensions.

### Fact Tables

**`FactReviews`** — one record per review. It includes review identifiers, destination and date keys, rating, original and English review text where available, sentiment fields, language, and data-quality attributes.

**`FactReviewAspects`** — review–aspect associations. A review can have multiple rows when multiple aspects are detected. It includes the review reference, aspect key, aspect sentiment, and supporting evidence fields.

### Dimension Tables

- **`DimDestination`** — destination names, types, and geographic attributes.
- **`DimDate`** — calendar attributes for date-based analysis.
- **`DimAspect`** — aspect definitions, groups, and detection-rule descriptions.

The model contains five core analytical tables. The workbook additionally includes documentation and QA sheets. See `Data_Dictionary` and `PowerBI_Guide` in `Main Dataset.xlsx` for field definitions and model guidance.

---

## 📈 Power BI Report

Power BI Desktop is the reporting and exploration layer. The analytical model is designed to support:

- Overall review and destination summaries.
- Sentiment distribution and comparison.
- Aspect-level positive and negative experience analysis.
- Destination-specific exploration.
- Time-based analysis where date coverage is sufficient.
- Review-level investigation and supporting evidence, where enabled in the report.

Interpretation must account for review sample sizes, missing text, platform bias, and the distinction between review counts and aspect-mention counts.

> The `.pbix` report is a separate artifact from the Python pipeline and Excel dataset. Dashboard visuals, interactions, and DAX measures should be assessed from the actual Power BI file.

---

## 🛠️ Technology Stack

| Technology | Role |
|---|---|
| Google Maps | Public review source |
| Apify Google Maps Reviews Scraper | Review collection |
| Python | Data processing and NLP pipeline |
| pandas / NumPy | Data manipulation |
| scikit-learn | Supporting analytical and evaluation utilities |
| openpyxl | Excel workbook input/output |
| Jupyter Notebook | Interactive pipeline development and review |
| Microsoft Excel | Analytical dataset, validation, and documentation workbook |
| Power BI Desktop | Data model, DAX measures, and interactive reporting |

The pipeline uses Python libraries listed in its import statements. See the source file for the exact implementation and configuration.

---

## 🚀 Running the Python Pipeline

### 1. Requirements

- Python 3.x
- The five destination source workbooks
- Required Python packages: `pandas`, `numpy`, `scikit-learn`, and `openpyxl`

Install the core dependencies:

```bash
pip install pandas numpy scikit-learn openpyxl
```

### 2. Prepare the Input Files

The script expects the following filenames in the input data directory:

```text
abu_simbel.xlsx
karnak.xlsx
giza.xlsx
valley_of_kings.xlsx
gem.xlsx
```

Place the five corresponding Google Maps source workbooks in one directory and use these expected filenames. The names in the supplied archive may differ, so check the source files carefully before renaming them.

### 3. Configure Paths

The pipeline supports these environment variables:

- `TOURSIGHTS_DATA_DIR` — directory containing the five input workbooks.
- `TOURSIGHTS_OUTPUT` — output Excel file path.

Example on Windows PowerShell:

```powershell
$env:TOURSIGHTS_DATA_DIR="C:\TourSights\data"
$env:TOURSIGHTS_OUTPUT="C:\TourSights\output\TourSights_NLP_Output.xlsx"
python TourSights_Full_Source_Code_v4.py
```

If these variables are not set, the script uses the default paths defined in its configuration section. Review that section before running the pipeline.

### 4. Expected Output

The Python export step creates an Excel workbook containing these six sheets:

1. `FactReviews`
2. `DimDestination`
3. `DimDate`
4. `DimAspect`
5. `FactReviewAspects`
6. `Run_Info`

`Main Dataset.xlsx` is the expanded project workbook. It also contains supporting validation, gold-label, findings, insights, recommendations, guide, dictionary, and change-log sheets. Those additional sheets are not all generated by the current Python export step.

---

## 🧪 Data Quality and Integrity Checks

The pipeline includes integrity checks for key relationships and analytical outputs, including:

- Date-dimension continuity and ordering.
- Valid review and aspect references.
- Duplicate review–aspect pair detection.
- Allowed aspect-sentiment labels.
- Non-empty evidence for aspect records.
- Expected aspect-dimension size.
- Aspect assignment coverage and text-review constraints.

The Excel workbook provides additional validation and documentation sheets. For the actual results and statuses, inspect `Validation_Report`, `Findings`, `NLP_Accuracy`, and `Arabic_Hybrid_Check`.

---

## ⚠️ Limitations

- **Review bias:** People who post public reviews are not necessarily representative of all visitors.
- **Platform scope:** The current dataset uses Google Maps only; results should not be generalized to other platforms without further data.
- **Language and NLP errors:** Multilingual text, sarcasm, context, spelling variation, negation, and ambiguous wording can affect classification quality.
- **Aspect coverage:** A review may contain useful feedback without matching any of the predefined aspect rules.
- **Date coverage:** Trend analysis depends on the dates available and the consistency of the collected data.
- **Geographical precision:** A review about a destination does not necessarily identify the exact physical location of an issue.
- **Collection constraints:** Public availability, scraper behaviour, platform changes, and usage limits can affect collection completeness.
- **Academic scope:** This is a proof of concept, not a production monitoring or decision-automation system.

Findings should be interpreted as patterns in the collected reviews, not as definitive measurements of every visitor's experience.

---

## 🔮 Future Work

Potential extensions include:

- Improving multilingual sentiment and aspect classification.
- Expanding and independently reviewing the manually labelled evaluation sample.
- Comparing automated labels with additional human annotators.
- Adding further destinations or review sources after feasibility and data-quality checks.
- Improving review-level evidence navigation and dashboard usability.
- Establishing a documented refresh and collection process.
- Validating analytical findings with tourism-domain specialists.

These items are proposed extensions, not claims about completed functionality.

---

## 👥 Project Team

**Program:** Digital Egypt Youth Initiative (DEPI)  
**Learning Provider:** CLS Learning Solutions  
**Group ID:** GIZ5_DAT1_S3  
**Supervisor:** Eng. Moataz Badran

| Student | Student ID |
|---|---:|
| Ahmed Khaled Ahmed Sayed | 21163471 |
| Ganna Adel Mahmoud Ibrahim | 21075562 |
| Mohamed Ashraf Hassan Abdulhamid | 21168429 |
| Malak Mohamed Mohamed Abdelmoneam | 21125342 |

---

## 📄 Project Documents

The repository may include the following project artifacts, depending on what is published:

- `TourSights_Full_Source_Code_v4.py` — main Python processing pipeline.
- `TourSights_Full_Source_Code_v4.ipynb` — notebook version of the pipeline.
- `Main Dataset.xlsx` — analytical model and supporting validation/documentation workbook.
- Power BI `.pbix` file — interactive report, if included in the repository.
- Technical project report — implementation, methodology, testing, results, and limitations.

Do not publish raw review exports or personal information unless their use and redistribution are permitted by the relevant platform terms and project requirements.

---

## 📜 Data Use and Attribution

TourSights processes publicly accessible Google Maps reviews for academic analysis. Public accessibility does not automatically grant unrestricted rights to redistribute review content or derived datasets.

Users of this repository should review the applicable platform terms, scraper/tool terms, and relevant privacy and data-protection requirements. Avoid republishing personal information or raw review text without an appropriate basis.

No software license has been specified for this project. Unless a license is added to the repository, reuse and redistribution permissions should not be assumed.

---

**TourSights — Understanding visitor experiences to support better tourism decisions.**
