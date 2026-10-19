# 🌍 TourSights — Tourism Intelligence

> **From Tourist Volume to Visitor Experience: Turning Public Reviews into Actionable Tourism Insights.**

TourSights is an academic Business Intelligence (BI) proof of concept that analyzes publicly available visitor reviews of selected Egyptian museums and archaeological sites.

By combining structured data preparation, sentiment analysis, visitor-experience categorization, and interactive Power BI dashboards, TourSights aims to help tourism decision-makers understand what visitors appreciate, what frustrates them, and which recurring issues deserve further investigation.

The project focuses on **the quality of visitor experiences, not just the number of tourists or their overall star ratings.**

---

## 📌 Project Overview

Tourists share detailed experiences on platforms such as Tripadvisor and Google Maps. These reviews contain valuable information about queues, pricing, cleanliness, accessibility, staff behavior, facilities, and the overall historical and cultural experience.

However, this information is unstructured and distributed across different platforms and destinations. Overall ratings alone cannot explain why visitors are satisfied or dissatisfied.

**TourSights transforms public visitor reviews into a structured analytical dataset and presents the results through an interactive Power BI Desktop report.**

The primary intended stakeholder is the **Egyptian Ministry of Tourism and Antiquities**, with destination managers and tourism analysts as secondary beneficiaries.

TourSights is currently an academic prototype, not a deployed national monitoring platform or a commercial product.

---

## 🎯 Problem Statement

Tourism performance cannot be fully understood through visitor numbers and average ratings alone.

Recurring problems may remain hidden within thousands of individual reviews, making it difficult to:

* Identify frequently mentioned visitor complaints.
* Understand which aspects of a destination are associated with negative experiences.
* Recognize positive aspects that should be maintained or enhanced.
* Compare destinations fairly when their review volumes differ.
* Examine changes in visitor feedback over time.
* Support decisions with traceable evidence rather than isolated comments.

TourSights addresses this analytical gap by organizing review data and providing comparable indicators of visitor experience.

---

## 💡 Proposed Solution

TourSights follows a data pipeline that transforms public reviews into structured, interpretable insights.

### 1. Data Collection

Collect visitor reviews from supported public platforms using data extraction tools.

Initial collection uses Outscraper, with Apify Actors planned for additional feasibility testing.

### 2. Data Preparation

Use Power Query to standardize column names, data types, dates, ratings, destination names, and source labels.

Identify missing values, inspect data quality, and distinguish technical duplicates from independent reviews that happen to contain similar complaints.

### 3. Sentiment Analysis and Experience Categorization

As an analytical extension, evaluate a pretrained sentiment model and combine it with transparent keyword-based rules to classify visitor feedback.

The proposed sentiment labels are:

* Positive
* Negative
* Neutral
* Mixed, where supported

Reviews may also be categorized into visitor-experience aspects such as pricing, cleanliness, queues, transportation, staff, facilities, and safety.

The classification approach will be validated against a manually labeled sample. If the NLP component proves unreliable or impractical, the core Power BI report will proceed using descriptive analytics and a simpler documented approach.

### 4. Business Intelligence and Visualization

Build an interactive Power BI Desktop report using a structured data model, DAX measures, filters, and destination-specific pages.

The report will help users explore visitor feedback, compare destinations using appropriately normalized indicators, and investigate the evidence behind aggregated results.

---

## 📊 Key Analytical Capabilities

The following capabilities describe the planned analytical scope. Their final availability depends on implementation, data coverage, and validation.

### 🗺️ Destination Comparison

Compare selected Egyptian museums and archaeological sites using review volumes, ratings, sentiment distributions, and visitor-experience indicators.

Comparisons will account for differences in sample sizes rather than relying on raw complaint counts alone.

### 🧠 Sentiment Analysis

Examine the distribution of positive, negative, and neutral feedback, with mixed sentiment included if the selected approach supports it.

Model performance will be evaluated using a manually labeled sample before accuracy claims are made.

### 🔎 Visitor-Experience Categorization

Organize reviews into predefined aspects of the visitor experience, including:

* Price and Value for Money
* Cleanliness
* Queues and Crowding
* Accessibility and Transportation
* Staff and Tour Guides
* Vendor Behavior, Harassment, and Scams
* Facilities and Visitor Services
* Signage and Visitor Information
* Safety and Security
* Historical and Cultural Experience
* Museum Exhibitions and Organization

Categories will be refined according to the actual collected data.

### 📈 Trend Analysis

Examine changes in review sentiment and recurring complaints over time where publication dates and data coverage are sufficient.

### ⭐ Positive Experience Analysis

Identify aspects frequently associated with positive visitor feedback, helping ensure that analysis considers destination strengths as well as problems.

### 📋 Evidence-Based Prioritization

Explore frequently mentioned issues using explicit counts, denominators, and normalized indicators.

Any proposed priority indicator will be documented as an analytical aid, not an official tourism risk rating or an automatically generated operational decision.

### 🔍 Review-Level Investigation

Where the available fields and report implementation permit, users will be able to navigate from summary visuals to selected underlying reviews.

---

## 🏛️ Initial Destination Scope

The project targets approximately five Egyptian museums and archaeological sites.

The following destinations are candidates, not a confirmed final selection:

| Destination                         | Current Status                     |
| ----------------------------------- | ---------------------------------- |
| The Pyramids of Giza and the Sphinx | Pilot data collected               |
| Grand Egyptian Museum               | Candidate; data collection pending |
| Karnak Temple Complex               | Candidate; data collection pending |
| Valley of the Kings                 | Candidate; data collection pending |
| Abu Simbel Temples                  | Candidate; data collection pending |

The final destinations will be selected according to data availability, data quality, analytical relevance, and the remaining implementation time.

The project will first assess a broader pool of approximately 8–10 candidate destinations and conduct feasibility tests on a smaller subset.

---

## 📂 Data Sources and Current Progress

Two initial Outscraper exports were available as of **19 October 2026**.

| Review Platform | Destination             | Raw Reviews Extracted | Collection Tool                        |
| --------------- | ----------------------- | --------------------: | -------------------------------------- |
| Tripadvisor     | The Pyramids of Giza    |                   500 | Outscraper                             |
| Google Maps     | Giza Necropolis         |                   500 | Outscraper                             |
| Tripadvisor     | Additional destinations |               Pending | Outscraper / Apify feasibility testing |
| Google Maps     | Additional destinations |               Pending | Subject to feasibility                 |

**Important:** The initial figures represent raw extraction counts, not the final number of usable reviews. Data cleaning, quality checks, and duplicate handling remain necessary.

Apify is planned for small feasibility tests, particularly its Tripadvisor Reviews Actor. No Apify collection run had been completed at the time of the initial project report.

Additional collection depends on source availability, tool limitations, and available free usage allowances.

### Data Preparation Principles

The project follows several data-quality principles:

* Preserve untouched copies of the original source files.
* Standardize fields across datasets where possible.
* Document missing fields and source-specific differences.
* Remove or flag demonstrable technical duplicates.
* Retain independent reviews even when their wording is similar.
* Report actual usable sample sizes and relevant limitations.
* Avoid making unsupported claims when dates, ratings, or other fields are unavailable.

---

## 🛠️ Technology Stack

| Technology                | Purpose                                                           |
| ------------------------- | ----------------------------------------------------------------- |
| Outscraper                | Initial collection of Tripadvisor and Google Maps reviews         |
| Apify                     | Planned additional source and collection-tool feasibility testing |
| Microsoft Excel           | Data inspection, annotation, and intermediate analysis            |
| Power Query               | Primary tool for structured data cleaning and transformation      |
| Python                    | Optional supplementary processing and NLP                         |
| Hugging Face Transformers | Candidate framework for pretrained sentiment models               |
| scikit-learn              | Evaluation metrics and model validation                           |
| Power BI Desktop          | Data modeling, interactive reports, and visualization             |
| DAX                       | Measures and analytical calculations                              |
| CSV / Excel               | Data exchange between processing stages                           |
| Google Colab or similar   | Optional environment for NLP experiments                          |

The project prioritizes free tools and available free usage allowances. Third-party collection services may impose usage limits or charges beyond their free allowances.

---

## ⚙️ System Architecture

The proposed analytical workflow is:

```text
Public Visitor Reviews
        |
        v
Outscraper Exports
(CSV / Excel)
        |
        v
Raw Data Storage
        |
        v
Power Query
Cleaning & Standardization
        |
        v
Data Quality Validation
        |
        +----------------------------+
        |                            |
        v                            v
Cleaned Review Dataset       Optional Python NLP
                                    |
                                    v
                           Sentiment Classification
                           & Aspect Categorization
                                    |
                                    v
                           Enriched Review Dataset
        |                            |
        +-------------+--------------+
                      |
                      v
               Power BI Data Model
                      |
                      v
             DAX Measures & KPIs
                      |
                      v
             Interactive Dashboard
                      |
                      v
          Evidence-Based Tourism Insights
```

The Python/NLP stage is optional and will be included in the final workflow only to the extent that it can be implemented and validated reliably.

Power Query handles structured table transformations, while advanced language processing is performed separately.

---

## 🗃️ Proposed Data Model

The Power BI model is planned around review-level and aspect-level data.

### Fact Tables

**FactReviews**

Contains review-level information, such as:

* Review ID
* Destination
* Review platform
* Review text
* Publication date
* Rating
* Language, where available
* Overall sentiment, if implemented

**FactReviewAspects**

Contains aspect-level records associated with reviews, where categorization is implemented.

Potential fields include:

* Review ID
* Aspect category
* Aspect sentiment, where supported

A review may mention several aspects. The model must distinguish review counts from aspect-mention counts to avoid double-counting.

### Dimension Tables

The proposed dimensions include:

* `DimDestination`
* `DimSource`
* `DimDate`
* `DimAspect`
* `DimLanguage`

The final schema will be adapted to the fields actually available in the collected datasets.

---

## 📊 Planned Power BI Report

The report is designed around an overview page and destination-specific pages.

### Overview and Destination Comparison

Proposed elements include:

* Total usable reviews
* Number of destinations represented
* Sentiment distribution
* Most frequently mentioned negative aspects
* Normalized negative rates by destination
* Positive visitor-experience aspects
* Trends where date coverage permits
* Destination, period, source, and language filters where supported

### Destination Pages

Each finalized destination will have a dedicated page containing relevant indicators, including:

* Review count and sample-size information
* Sentiment distribution
* Aspect mentions
* Negative rates by aspect
* Positive experience indicators
* Rating summaries
* Trends where data permits
* Issue-prioritization indicators
* Navigation to underlying reviews where feasible

### Data Transparency

The report will document relevant sources, date coverage, metric definitions, and limitations.

The dashboard will be tested to ensure that totals reconcile with the underlying data, percentages use explicit denominators, and comparisons do not rely solely on raw counts.

The dashboard design remains a proposal until implemented and tested.

---

## 🧪 Testing and Validation

TourSights will evaluate both data quality and analytical reliability.

### Data Quality Checks

* Missing and empty review text
* Date validity and coverage
* Rating ranges
* Field completeness
* Destination and source mapping
* Technical duplicates
* Relevant versus unusable records
* Actual usable sample sizes

### NLP Validation

If NLP is implemented, model predictions will be compared against a manually labeled sample.

Evaluation may include:

* Precision
* Recall
* F1-score
* Macro F1-score
* Confusion matrix

The selected metrics will depend on the implemented task and available validation data.

Errors involving negation, sarcasm, mixed sentiment, language variation, and incorrect aspect assignments will be documented where observed.

### Power BI Validation

* Reconcile dashboard totals with source tables.
* Verify DAX calculations and percentage denominators.
* Test filters and navigation.
* Check for double-counting across review and aspect tables.
* Confirm that missing data is handled transparently.
* Record actual test outcomes rather than assuming the report is correct.

No model accuracy, final sentiment distribution, or dashboard performance result is claimed before measurement.

---

## 🚧 Scope and Limitations

The current project is an academic proof of concept with a limited implementation window and a constrained data-collection budget.

### Current Scope

* Approximately five selected Egyptian museums and archaeological sites.
* Public online review data from feasible sources.
* Structured cleaning and preparation with Power Query.
* Optional sentiment and aspect categorization.
* An interactive Power BI Desktop report.
* Data-quality checks, validation, testing, and documentation.

### Out of Scope for the Current Version

* Continuous production monitoring.
* Automatic scheduled data collection and refresh.
* A fully deployed public web application.
* Comprehensive coverage of all Egyptian tourist destinations.
* Training a large language model from scratch.
* Guaranteed access to every review platform.
* Automatic prescription of tourism interventions.
* Precise identification of a physical problem location when the review does not provide sufficient evidence.

### Important Analytical Limitations

**Review representativeness:** Online reviewers are self-selected. Their opinions cannot automatically be generalized to all tourists.

**Platform differences:** Review platforms may differ in their user populations, rating distributions, and available fields.

**NLP uncertainty:** Sentiment and aspect classifications may be wrong, particularly for sarcasm, negation, ambiguous comments, and unsupported languages.

**Data availability:** Some destinations may not provide sufficient usable reviews or reliable dates for trend analysis.

**Geographical precision:** A review about a destination does not necessarily identify the exact physical location where an issue occurred. Geographic claims must remain within what the available evidence supports.

TourSights is intended to support informed investigation, not replace expert judgment or establish causation.

---

## 🗓️ Project Timeline

The initial plan covers approximately six weeks, beginning on 19 October 2026.

| Phase                            | Planned Period | Main Deliverable                             |
| -------------------------------- | -------------- | -------------------------------------------- |
| Project Planning & Requirements  | Week 1         | Scope, requirements, and source assessment   |
| Data Collection & Preparation    | Weeks 1–3      | Standardized dataset and quality report      |
| NLP & Analytical Modeling        | Weeks 3–4      | Validated analytical outputs, if feasible    |
| Power BI Dashboard & Integration | Weeks 4–6      | Interactive `.pbix` prototype                |
| Testing & Final Documentation    | Week 6         | Test results, final report, and presentation |

The provisional finalization date is 30 November 2026 and must be confirmed against the official institutional deadline.

---

## 🚀 Future Work

Potential improvements beyond the current prototype include:

* Expanding coverage to additional Egyptian destinations.
* Integrating more verified review sources.
* Improving multilingual sentiment and aspect classification.
* Increasing the size of the manually labeled validation dataset.
* Improving aspect-level classification quality.
* Introducing scheduled data refresh.
* Developing more advanced trend and change-detection methods.
* Validating findings with tourism experts and intended institutional users.
* Improving dashboard navigation and usability.
* Integrating verified operational tourism data where available.

These are future possibilities, not completed features.

---

## 👥 Project Team

**Program:** Digital Egypt Youth Initiative
**Learning Provider:** CLS Learning Solutions
**Group:** GIZ5_DAT1_S3
**Project Supervisor:** Eng. Moataz Badran

TourSights is developed by a four-member engineering and data-focused student team.

The work is organized into four main phases:

1. Project Planning, Research, and Requirements
2. Data Collection and Data Preparation
3. NLP, Sentiment Analysis, and Analytical Modeling
4. Power BI Dashboard, Testing, and Integration

All team members contribute to integration, peer review, testing, and final delivery.

---

## 📌 Project Status

**Status as of 19 October 2026: Initial planning and pilot data collection completed; implementation in progress.**

| Component                                 | Status                               |
| ----------------------------------------- | ------------------------------------ |
| Project proposal and initial requirements | Documented                           |
| Initial destination shortlist             | In progress                          |
| Outscraper pilot collection               | Completed for two Giza-area listings |
| Expanded data collection                  | Planned                              |
| Power Query cleaning                      | Planned                              |
| Data-quality validation                   | Planned                              |
| Sentiment and aspect categorization       | Planned; subject to validation       |
| Power BI data model                       | Planned                              |
| Interactive dashboard                     | Planned                              |
| Testing and final validation              | Planned                              |

The current status reflects the initial project report. Future updates should describe actual implementation progress and measured results.

---

## 🤝 Contributions

TourSights is currently an academic project in its MVP development phase.

Potential contributions include:

* Improving data-quality checks and review standardization.
* Evaluating pretrained sentiment models on tourism reviews.
* Refining visitor-experience categories.
* Improving multilingual text classification.
* Testing analytical measures and Power BI visualizations.
* Strengthening validation, documentation, and reproducibility.

Any new functionality should be evaluated against the project's scope, data availability, and validation requirements.

---

## 📄 License and Data Usage

No project software license has been specified yet.

Review collection and use must respect the relevant platforms' terms, applicable usage restrictions, and the licenses of any third-party tools or models.

The project should retain source attribution and document collection methods and limitations. Publicly accessible reviews should not automatically be assumed to be unrestricted for every form of reuse or redistribution.

---

**TourSights — Understanding visitor experiences to support better tourism decisions.**
