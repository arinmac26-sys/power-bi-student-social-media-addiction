# 📊 Student Social Media Addiction — Power BI Data Analytics Project

> **Portfolio-ready Power BI project** focused on understanding how social-media usage relates to academic performance, sleep, mental health, relationships, and addiction scores among students.

![Power BI](https://img.shields.io/badge/Power%20BI-Analytics-F2C811?logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-Measures-512BD4)
![Excel](https://img.shields.io/badge/Source-Excel-217346?logo=microsoft-excel&logoColor=white)
![Status](https://img.shields.io/badge/Status-Portfolio%20Ready-brightgreen)

## 1. Project Overview

This project converts a student social-media dataset into an interactive Power BI analytical solution.

### Business objective

The dashboard is designed to answer:

- How large is the student population represented in the dataset?
- How much time do students spend on social media each day?
- What percentage report an academic-performance impact?
- How does social-media usage vary by age, gender, and academic level?
- Which platforms are most commonly used?
- Is higher addiction associated with mental-health outcomes?
- How are sleep, relationships, and social-media conflicts distributed?
- Which student segments may require deeper investigation?

## 2. Dataset

Source workbook: `data/raw/Students Social Media Addiction.xlsx`

The workbook contains two source tables:

| Table | Rows | Purpose |
|---|---:|---|
| Student Details | 705 | Student demographics, lifestyle, mental health, relationship and addiction attributes |
| Platform Details | 705 | Daily usage, most-used platform and academic-performance impact |

### Core fields

**Student Details**
- `Student_ID`
- `Age`
- `Gender`
- `Academic_Level`
- `Country`
- `Sleep_Hours_Per_Night`
- `Mental_Health_Score`
- `Relationship_Status`
- `Conflicts_Over_Social_Media`
- `Addicted_Score`

**Platform Details**
- `Student_ID`
- `Avg_Daily_Usage_Hours`
- `Most_Used_Platform`
- `Affects_Academic_Performance`

## 3. Data Model / ER Diagram

The PBIX model contains `Student Details`, `Platform Details`, and a `DateTable` used in the model layout.

![ER Diagram](docs/erd/student_social_media_erd.svg)

Editable Mermaid version: [`student_social_media_erd.mmd`](docs/erd/student_social_media_erd.mmd)

> **Model note:** `Student_ID` is the business key connecting the two supplied source tables. The date table is documented separately because the provided source workbook does not contain a transaction/date field.

## 4. Power BI Report Pages

The supplied PBIX contains these report pages:

1. **Executive Overview**
   - Total Students
   - Average Usage
   - % Affected Academically
   - Average Sleep Hours
   - Addiction by Academic Level
   - Usage by Age
   - Student distribution by Gender

2. **Mental Health & Lifestyle**
   - Country vs Health Band
   - Addiction Score vs Mental Health Score
   - Sleep Hours trend/analysis
   - Gender slicer

3. **Academic Impact**
   - Average Daily Usage by Academic Level
   - Academic Performance Impact by Platform
   - Age slicer

4. **Relationships and Conflicts**
   - Conflict Level by Relationship Status
   - Student-wise Addiction Score
   - Relationship Status Distribution
   - Country and Academic Level slicers

5. **Interactive Story View**
   - Usage by Gender
   - Most-used platform by Gender
   - Usage by Academic Level
   - Most-used platform by Academic Level
   - Navigation buttons and slicers

6. **Student Details**
   - Student-level table
   - Sleep Hours
   - Usage Hours
   - Addiction Score
   - Most-used Platform
   - Conflicts
   - Mental Health Rating

## 5. KPI / DAX Documentation

The report uses measures including:

### Total Student Counts
```DAX
Total Student Counts =
DISTINCTCOUNT('Student Details'[Student_ID])
```

### Average Sleep Hours
```DAX
Avg Sleep Hours =
AVERAGE('Student Details'[Sleep_Hours_Per_Night])
```

### Average Usage Hours
```DAX
Avg Usage Hours =
AVERAGE('Platform Details'[Avg_Daily_Usage_Hours])
```

### % Affected Academically
```DAX
% Affected Academically =
DIVIDE(
    CALCULATE(
        COUNTROWS('Platform Details'),
        'Platform Details'[Affects_Academic_Performance] = "Yes"
    ),
    COUNTROWS('Platform Details')
)
```

> The formulas above are portfolio documentation/recommended equivalents based on the fields and measures observed in the supplied PBIX. If you later edit the PBIX, keep the documented DAX synchronized with the model.

Full DAX notes: [`dax/dax_measures.md`](dax/dax_measures.md)

## 6. Data Analytics Workflow

```text
Excel Source
    ↓
Data Profiling
    ↓
Power Query / Data Preparation
    ↓
Data Model & Relationships
    ↓
DAX Measures / Calculated Columns
    ↓
Interactive Visualizations
    ↓
Business Insights
    ↓
Power BI Service / Portfolio
```

## 7. Recommended Data Quality Checks

Before publishing:

- Check duplicate `Student_ID` values.
- Confirm one-to-one key integrity between source tables.
- Check null values in critical fields.
- Validate numeric ranges:
  - Age
  - Sleep hours
  - Mental health score
  - Addiction score
  - Conflict count
- Standardize platform, country and academic-level labels.
- Confirm `Affects_Academic_Performance` contains only expected categories.
- Hide technical/helper columns from report users where appropriate.
- Mark the date table as a date table if it is used for time intelligence.

See [`docs/data_quality_checklist.md`](docs/data_quality_checklist.md).

## 8. Suggested Business Insights

Use the dashboard to communicate findings rather than only showing charts.

Examples of questions to investigate:

- Which academic level has the highest average daily usage?
- Which platforms are associated with the largest academic-impact share?
- Does addiction score increase as mental-health score changes?
- Which relationship-status groups report more conflicts?
- Are lower sleep-hour groups associated with higher addiction scores?
- Which countries have the highest concentration of students in each health band?

> Do not state an insight as fact in the portfolio README until it has been validated from the final Power BI model.

## 9. Repository Structure

```text
power-bi-student-social-media-addiction/
│
├── README.md
├── LICENSE
├── .gitignore
│
├── powerbi/
│   └── Powe_BI_mini_projects_Arindam_Das_Biswas.pbix
│
├── data/
│   └── raw/
│       └── Students Social Media Addiction.xlsx
│
├── docs/
│   ├── erd/
│   │   ├── student_social_media_erd.mmd
│   │   ├── student_social_media_erd.svg
│   │   └── erd.dot
│   ├── screenshots/
│   │   └── README.md
│   ├── data_dictionary.md
│   ├── data_model.md
│   ├── data_quality_checklist.md
│   ├── business_questions.md
│   └── project_walkthrough.md
│
├── dax/
│   └── dax_measures.md
│
├── power-query/
│   └── README.md
│
└── sql/
    └── README.md
```

## 10. GitHub Setup — Step by Step

### Step 1 — Create a GitHub repository

On GitHub:

1. Click **New repository**.
2. Repository name:
   `power-bi-student-social-media-addiction`
3. Description:
   `Power BI data analytics project exploring student social media usage, addiction, academic impact, sleep and mental health.`
4. Select **Public** if this is for your portfolio.
5. Add a README only if you are starting from an empty local folder. If using this package, leave it unchecked.
6. Click **Create repository**.

### Step 2 — Open Terminal

```bash
cd /path/to/power-bi-student-social-media-addiction
```

### Step 3 — Initialize Git

```bash
git init
git branch -M main
```

### Step 4 — Review files

```bash
git status
```

### Step 5 — Add files

```bash
git add .
```

### Step 6 — Commit

```bash
git commit -m "Initial commit - Power BI student social media analytics project"
```

### Step 7 — Connect GitHub

Replace the URL with your own repository URL:

```bash
git remote add origin https://github.com/<YOUR_USERNAME>/power-bi-student-social-media-addiction.git
```

### Step 8 — Push

```bash
git push -u origin main
```

### Step 9 — Verify

Refresh the GitHub repository and confirm that the following are visible:

- README
- PBIX file
- Excel source
- ERD
- DAX documentation
- data dictionary
- project documentation

## 11. Git Best Practices

For a portfolio repository:

- Keep raw data clearly separated under `data/raw/`.
- Do not commit passwords, API keys, tokens or credentials.
- Keep PBIX as a versioned binary artifact.
- Use meaningful commit messages.
- Use screenshots in `docs/screenshots/` to make the project understandable without opening Power BI.
- Keep the README business-focused.
- Add a Power BI Service link if the report is published publicly.
- Add your LinkedIn and portfolio links to the README.

## 12. Portfolio Presentation

Recommended GitHub project title:

**Student Social Media Addiction Analytics | Power BI**

Recommended one-line resume description:

> Built an interactive Power BI analytics solution using 705 student records to analyze social-media usage, addiction, academic impact, sleep, mental health, relationships and platform behavior through KPI-driven dashboards and interactive segmentation.

## 13. Future Enhancements

- Add a dedicated Date dimension with proper time intelligence.
- Add a star-schema layer if the dataset grows.
- Add RLS if the report becomes multi-user.
- Add Power BI Service deployment documentation.
- Add automated data-refresh documentation.
- Add a formal executive insights page.
- Add drill-through from segment → student detail.
- Add tooltip pages for deeper analysis.
- Add a data dictionary and metric glossary.
- Add a published Power BI report link.

---

### Author

**Arindam Das Biswas**

Power BI | Data Analytics | SQL | Python | Data Visualization

> This repository is structured as a professional Data Analyst portfolio project and can be extended with screenshots, published dashboard links, and validated business findings.
