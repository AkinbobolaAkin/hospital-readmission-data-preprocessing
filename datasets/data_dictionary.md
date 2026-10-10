# Data dictionary (as documented by the source systems)

> Documentation is nominal. Real extracts do not always follow their documentation.

## patients.csv  (registration system)
| column | description |
|---|---|
| patient_id | Registration record ID (`P` + 6 digits) |
| first_name, last_name | Patient name as registered |
| sex | Sex recorded at registration |
| date_of_birth | Date of birth |
| race | Self-reported race / ethnicity |
| weight, weight_unit | Weight at registration and its unit |
| height | Height in **cm** |
| postal_code | 5-digit ZIP code of residence |

## admissions.csv  (hospital information system) - one row per stay
| column | description |
|---|---|
| admission_id | Admission identifier |
| pat_id | Patient identifier (links to patients.patient_id) |
| admit_date, discharge_date | Admission / discharge dates |
| age | Age in years at admission |
| gender | Patient gender |
| admission_type_id, discharge_disposition_id, admission_source_id, ward_code | Coded administrative fields |
| payer_code | Insurance payer |
| medical_specialty | Specialty of the admitting physician |
| time_in_hospital | Length of stay in days |
| los_hours | Length of stay in hours |
| num_lab_procedures, num_procedures, num_medications | Counts during the stay |
| number_outpatient, number_emergency, number_inpatient | Visits in the 12 months before admission |
| diag_1, diag_2, diag_3 | Primary / secondary / tertiary diagnosis (ICD-9) |
| number_diagnoses | Number of diagnoses entered |
| dx_group | Diagnosis group of diag_1 |
| A1C_result | HbA1c category (`None` = test not performed) |
| days_to_next_encounter | Days until the patient's next recorded encounter in the health system |
| readmitted | Readmission status: `<30` days, `>30` days, `NO` |

## labs.csv  (laboratory system) - long format, several draws per test possible
| column | description |
|---|---|
| lab_id | Result identifier |
| admission_id | Admission the sample belongs to |
| test_name | Test performed |
| result_value | Reported result |
| unit | Unit of the reported result |
| collected_at | Collection timestamp |

## medications.json  (pharmacy system)
List of records, one per admission: `admission_id`, `prescriptions` (list of orders with `drug_name`, `dose`,
`frequency`, `route`, `dose_change`), `insulin` (nested object or null), `allergies`, `discharge_notes`.
