# DataQuality_IDERHA
This repository contains a data quality methodology to be used in IDERHA.
This file contains explanation on each step within the methodology and how to conduct the data quality assessment.

**1. Uniqueness Assessment**
1.1. Identifying completely duplicated rows
This section will assess the number of completely duplicated data rows in the dataset.
The code will:
  - Identify all rows in the dataset that are complete duplicates.
  - Visualize the duplicates to understand their distribution.
  - Will remove the complete duplicates.

**2. Completeness Assessment**
2.1. Missing essential variables
This section first assesses the completeness of some essential variables by counting missing values in each column, specific for the PATIENTS data set.
The code will:
  - Assess completeness of defined essential variables.
  - Visualize level of completeness.
  - Mark all missing data as _"NA"_.

2.2. Missing variables in general
This section secondly assesses the completeness of all variables. 
The code will:
  - Assess completeness of all variables.
  - Visualize level of completeness.
  - Mark all missing data as _"NA"_.

2.3. Conditional completeness
This section will assess conditional completeness, which refers to the adequacy of data completeness based on specific conditions or criteria. 
For example, if a patient record shows that they are taking an allergy medicaiotn, then there should be a corresponding entry indicating an allergy. 
The current code focuse on the PATIENTS data set. 
The code will:
  - Assess conditional completeness.
  - Visualize level of conditional completeness.
  - Mark all errors as _"NA"_.

To note, other data quality checks are possible for this dimension, but will depend on the data from the data source.
Other categories:
  - Drug and lab results:
          Ensures that if a patient is prescribed certain medications, there shold be corresponding lab results that justify or monitor the effects of the medication.
          For example, suppose a patient is prescribed a medication like Warfarin, a blood thinner used to prevent blood clots. Conditioal completeness would require that lab results
          for International Normalized Ratio (INR), a test used to monitor the effectiveness of Warfarin, are also present in the patient's record. 
  - Drug and diagnosis:
          Ensures that if a patient is prescribed a specific drug, there must be a relevant diagnosis recorded in their health records. This helps in validating that the prescriptions
          are medically justified and tailored to treat specific conditions the patient has been diagnosed with.
          For example, if a patient is prescribed insulin, conditional completeness would dictate that there is a diagnosis of diabetes recorded in the patient's medical history.
  - Diagnosis and lab results:
          Ensures that for certain diagnosis, there are corresponding lab results to confirm or monitor the condition.
          For example, if a patient is diagnosed with hyperthyroidism, conditional completeness would require the presence of lab results for thyroid function tests, such as TSH,
          Free T4, and Free T3 levels.

**3. Consistency**
3.1. Data type unit
This section examines whether all data values are in the right format, as defined in the data dictionary. 
When no restrictions are formulated regarding value format, errors and score are left blank ( _"NA"_).
The code will focus on the PATIENTS data set, but can be adjusted towards other data sets. 
The code will:
  - Compare actual data types to the expected ones.
  - Visualize level of data type unit consistency.
  - Convert all erroneus columns to the demanded data type.

3.2. Out of range
This section examines whether numerical values fall within prespecified ranges and whether categorical/character variables have values that comply with predifined options as described in the data dictionary. 
To note, if no ranges are formulated in the data dictionary, _'is life possible'_ ranges are used. 
The code provided will focus on the PATIENTS data set for which two data quality rules are defined:
  - age: > 1 and < 150
  - gender: M/F

To note, other data quality checks are possible for this dimension, but will depend on the data from the data source.
Examples:
  - Total cholesterol: within the range of 5,00 mg/dL to 200,00 mg/dL
  - High-density lipoprotein (HDL): within the range of 5,00 mg/dL to 200,00 mg/dL
  - Low-density lipoprotein (LDL): within the range of 0,00 mg/dL to 999,00 mg/dL
  - Troponin I (TnI): within the range of 0,03 ng/mL to 80,00 mg/dL
  - C-Reactive protein: within the range of 5,00 mg/L to 600,00 mg/L
  - Triglycerides: within the range of 10 mg/dL to 5000 mg/dL
  - Blood pressure systolic: within the range of 20 mmHg to 350 mmHg
  - Blood pressure diastolic: within the range of 20 mmHg to 350 mmHg
  - Weight: within the range of 1 kg to 300 kg
  - Height: within the range of 0,1 meter to 3 meter
  - BMI: within the range of 5 kg/m² to 70 kg/m²
  - Heart rate: within the range of 20 beats/min to 200 beats/min
  - Albumin: within the range of 1 g/dL to 14 g/dL
  - Creatinine: within the range of 0,1 mg/dL to 40 mg/dL
  - Alanine transaminase (ALT): within the range of 5 IU/L to 26000 IU/L
  - Aspartate transaminase (AST): within the range of 5 IU/L to 26000 IU/L
  - Gamma-glutamyl transferase (GGT): within the range of 5 IU/L to 30000 IU/L

3.3. Conflicting information
This step examines for violations to data quality by applying interdependency relationships that have been defined by using different variables. 
The code will:
   - Implement data quality rules specific towards received data.
   - Apply data quality rules to check for violations.
   - Visualize level of conflicting information for consistency

This contains several categories:
  - Age and procedure:
          Ensures that the procedures performed are appropriate for the patient's age.
          For example, performing a colonscopy on a healthy child of 2 years would be a violations, as this procedure is generally recommended for adults.
  - Data and time error
          Ensures for plausible and accurate recording of dates and times related to patient care events.
          For example, if a patient's record shows a discharge date from the hospital that is earlier than the admission date.
  - Gender and diagnosis
          Ensures that diagnosis are consistent with the patient's gender, as certain health conditions are gender-specific.
          For example, prostate cancer in a female patient's medical record would be a violation of this category.
  - Gender and procedure
          Ensures that medical procedures recorded are appropriate for the patient's gender.
          For example, recording a hysterectomy (a surgical procedure to remove the uterus) for a male patient would be a data quality error for this category. `

**4. Correctness**
This dimensions will assess a subset of data variables by combining information across variables (i.e., multivariate correctness).
Assessing this dimension depends on the availability of data. Currently, we will focus on height and weight assuming these variables are complete. 

**5. Stability**
This dimension will assess how the data in a data set changes over time. The objective is to assess any shifts or changes in data that occur at different times.
This is done through the estimation of data statistical distributions over time and their projection in non-parametric statistical manifolds, uncovering the patterns of the data latent temporal variability.

This R package is build toward EHR data, but can be used on an OMOP dataset, but you will need to adjust the data structure to fit the requirements of the package. OMOP has a standardized data model that includes various tables such as 'person', 'observation_period', 'measurement', and others that contain time-stamped data which is essential for temporal stability analysis. 

The code provides a step-by-step approach on how you might use the R package with an OMOP dataset, with as example focusing on a variable like weight, which is typically stored in the 'measurement' table. 








