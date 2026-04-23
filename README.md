# Training Data Ltd. Customer Dataset Cleaning Project

## Overview

This project is a proof-of-concept for a more efficient storage solution for Training Data Ltd.'s customer dataset. The goal is to clean and optimize `customer_train.csv` a subset of the company's full customer database so that downstream machine learning models can generate predictions faster and at scale, without sacrificing data quality or reducing dataset size.

The dataset contains anonymized student information collected during training, and will ultimately be used to predict whether a student is actively seeking new employment  intelligence that Training Data Ltd. uses to connect students with prospective recruiters.

---

## Dataset

**File:** `customer_train.csv`

**Purpose:** Predict job-seeking behavior (`job_change`) among students enrolled in data science training.

### Columns

| Column | Type | Description |
|---|---|---|
| `student_id` | Integer | Unique identifier for each student |
| `city` | String | Code representing the city where the student lives |
| `city_development_index` | Float | Scaled development index for the student's city |
| `gender` | String (categorical) | The student's gender |
| `relevant_experience` | String (categorical) | Whether the student has relevant work experience |
| `enrolled_university` | String (categorical) | Type of university course enrolled in, if any |
| `education_level` | String (categorical) | Highest education level attained |
| `major_discipline` | String (categorical) | Educational discipline / field of study |
| `experience` | String / Integer | Total years of work experience |
| `company_size` | String (categorical) | Number of employees at the student's current employer |
| `company_type` | String (categorical) | Type of company currently employing the student |
| `last_new_job` | String / Integer | Years between the student's current and previous job |
| `training_hours` | Integer | Total training hours completed on the platform |
| `job_change` | Integer (binary) | Target variable: `1` = looking for a new job, `0` = not looking |

---

## Project Goal

The primary challenge motivating this project is **storage inefficiency**. When datasets are not stored in optimized formats, model training and inference pipelines can take days to complete even on powerful hardware.

This project demonstrates how to:

- Audit column data types and downcast where appropriate (e.g., `int64` → `int32`, `float64` → `float32`)
- Convert high-cardinality string columns to memory-efficient `category` dtype
- Identify and handle missing values consistently
- Produce a cleaned, type-optimized version of the dataset that reduces memory footprint without any loss of information

---

## Getting Started

### Prerequisites

- Python 3.8+
- pandas
- numpy

Install dependencies:

```bash
pip install pandas numpy
```

### Running the Cleaning Script

```bash
python clean_dataset.py
```

This will read `customer_train.csv`, apply all cleaning and type optimization steps, and output the result to `customer_train_clean.csv` (or a compressed `.parquet` equivalent).

---

## Output

The cleaned dataset retains all original rows and columns but uses efficient storage types throughout. Expected outcomes include:

- Significant reduction in in-memory size (often 50–80% for mixed-type datasets like this one)
- Faster read/write times when used in model training pipelines
- Consistent handling of null/missing values across all columns

---

## Notes

- `student_id` is a unique key and should never be used as a model feature.
- `job_change` is the **target variable** for prediction tasks.
- Several columns (`experience`, `last_new_job`, `company_size`) use string representations of numeric ranges (e.g., `">20"`, `"50-99"`) and may require additional preprocessing before being used in a model.
- This dataset is a **subset** of the full Training Data Ltd. customer database and is intended for proof-of-concept purposes only.

---

## Contact

For questions about this dataset or the cleaning methodology, please contact the data engineering team at Training Data Ltd.
