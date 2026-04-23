Overview
This dataset is a subset of Training Data Ltd.'s full customer database, provided as a proof-of-concept for building a more efficient data storage solution. The ultimate goal is to train a machine learning model that predicts whether a student is actively looking for a new job, enabling the company to connect job-seeking students with prospective recruiters.
Because the full dataset is extremely large — large enough that model training and inference can take days — efficient storage and data typing are critical to reducing compute time without sacrificing dataset size or quality.

File
FileDescriptioncustomer_train.csvAnonymized student records with job-seeking labels

Dataset Columns
ColumnTypeDescriptionstudent_idIntegerA unique identifier for each studentcityString (categorical)A code representing the city the student lives incity_development_indexFloatA scaled development index for the student's citygenderString (categorical)The student's genderrelevant_experienceString (categorical)Whether the student has relevant work experienceenrolled_universityString (categorical)Type of university course currently enrolled in, if anyeducation_levelString (categorical)The student's highest level of educationmajor_disciplineString (categorical)The student's educational discipline or field of studyexperienceString / IntegerTotal years of professional work experiencecompany_sizeString (categorical)The size (employee count range) of the student's current employercompany_typeString (categorical)The type of company the student currently works forlast_new_jobString / IntegerNumber of years between the student's current and previous jobstraining_hoursIntegerTotal number of training hours completed on the platformjob_changeInteger (binary)Target variable: 1 = looking for a new job, 0 = not looking

Target Variable
The target variable is job_change:

1 — The student is looking for a new job
0 — The student is not looking for a new job

This is a binary classification problem.

Storage Efficiency Goals
A key objective of this project is to optimize the dataset's storage footprint. Recommended steps include:

Downcasting numeric types — Use the smallest appropriate integer or float type (e.g., int8, float32) where precision allows.
Converting categoricals — Columns with a limited set of repeated string values (e.g., city, gender, company_type) should be stored as category dtype in pandas rather than object.
Handling ordinal columns — Columns like experience, company_size, and last_new_job may benefit from being encoded as ordered categoricals or mapped to integers.
Binary encoding — The job_change target and binary indicator columns can be stored as int8 or bool.

These changes can reduce memory usage dramatically and allow models to run in a fraction of the time on the full dataset.

Notes

Student data has been anonymized — no personally identifiable information is included.
Some columns may contain missing values that should be addressed during preprocessing.
This CSV is a proof-of-concept subset and is not the complete production dataset.


Usage
This dataset is intended for internal use by data scientists at Training Data Ltd. for:

Exploratory data analysis (EDA)
Storage optimization and dtype conversion
Feature engineering and preprocessing
Training binary classification models
