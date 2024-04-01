# Healthcare - Project1

### Dashboard Link : 

## Problem Statement and Overall Objectives

The main purpose with this healthcare project is to track current status of patient waiting list by analyzing the historical monthly trend of waiting lists in inpatient and outpatient categories. A detailed speciality-level and age-profile analysis based on those groups will also be performed. 

NB! Inpatients are individuals who stay in a hospital under treatment, while outpatient only receive medical treatment whithout being admitted to a hospital. 

Data Scope: The data scope for this analysis will be between 2018 and 2021. 
Metrics Required: The required metrics is average & median waiting list, and finally the current total waitlist. 
View Required: A summary page presenting the above requirements and a detailed page for granular/detailed analysis. 


### Steps followed 

- Step1: Requirements Gathering
    1. Identify stakeholders and establish a point of contact. 
    2. Understanding Business Objectives through meeting & communication. 
    3. Conduct a High Level Data Study (Data Sources, Colum Description,
       Data Type, volume/frequency & Data Quality). 
    4. Define Scope (KPIs, timelines, Expectations, etc.)

- Step2: Data Collection    
- Step3: Transformation & Modeling
- Step4: Data Visualisation Blueprint 
- Step5: Dashboard Layout & Design 
- Steg6: Interactivity & Navigation
- Step7: Testing 
- Step8: Sharing
- Step9: Maintenance & Refresh

### Step2: Data Collection

Load data into Power BI, the inpatient´s and outpatients´s data are stored as xlsx files representing each year in respectives folders. The speciality group dataset is stored as CSV file. The first two large datasets have been uploaded as Folders in Power BI while the last one has been uploaded as a CSV file.
Since there are multiple files, before loading data, I checked some critical quality factors such as column count and headers to ensure that the data matches. Then, I combined and loaded the files into Power BI for the respective Inpatient and outpatient folders. 

### Step3: Transformation & Modeling

In the transformation view page: 
- The data type for all columns was checked, and the wrong ones were corrected.
- The total number of rows for each dataset was checked and compared with the original xlsx or CSV files to ensure that my uploading was done correctly.
- Since the output dataset did not have a "Case_type" column, a new custom column was created with the value "Output".
- Before appending the two tables, datasets were checked to ensure that the number of columns were equal and that the column names and positions were consistent throughout.
- The created table was appended as new, with "Impatient" as the first table and "Outpatient" as the second one. Then the new table was also renamed (e.g All_Data).
- The new table was closed and applied for the next step (Data visualisation).

NB! Since the tranformation & modeling phase is iterative, this step has been done several times when different changes were needed to correct our data or put it in a format that enables the visualizations goals. 

- Once the tranformed data is uploaded, in the modeling view, I ensure that the desired model/relationship created between the data (All_data and Mapping_Specialty) is correct. Finally, tables that will not be used are deleted or hidden from the report view to avoid any confusion.

### Step4: Data Visualisation Blueprint
