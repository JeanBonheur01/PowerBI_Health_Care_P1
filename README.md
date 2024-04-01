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

### Step4 & 5: Data Visualisation Blueprint & Dashboard Layout/Design

- Firsly, a discussion of the entire visualisation with the team or relevant stakeholders and finalizing a structure.
- Before starting with the designing process, in the view module, I enable the "Gridlines" and "Snap to grid" functions so the dashboard layout can be done easily and efficiently.

#### 1. Summary Page 

- Total waitlist of the current month:

We use the DAX option (Data Analysis Expression) by creating a new measure and entering the name and the formula of that measure.

Formula: Last Month Wait List = CALCULATE(SUM(All_Data[Total]), All_Data[Archive_Date] = Max(All_Data[Archive_Date])) + 0
![image](https://github.com/JeanBonheur01/PowerBI_Health_Care_P1/assets/131664311/883ee3aa-267c-41f8-87fb-623845bc38d1)

NB! The new measure has been represented on a card at the top left of screen. 
0 is added to the formula to avoid a blank value in the visualization. 
  
- Total waitlist of the previous year´s same month:
This is important so we can compare it with the current month/situation.

Formula: PY Latest Month Wait List = CALCULATE(SUM(All_Data[Total]), All_Data[Archive_Date]= EDATE(MAX(All_Data[Archive_Date]), -12)) +0
![image](https://github.com/JeanBonheur01/PowerBI_Health_Care_P1/assets/131664311/5b4158db-71a0-4149-88dd-d22f49739dcb)

NB! To move to the previous month, the EDATE function has been used. Since it represents the previous month of the last year, the formula has been substracted by -12 (12 month before the current month). 

- Average and median metrics to enable the statistical visualization of the waiting list

Since the interaction between the Average and Median metrics will be necessary, it is critical to create a "dynamic measure" that will enables this interactions whithin the entire visualization. 

Dynamic measure: - create a new table/rename/enter names of actual measure/Load
                 - Then, a slicer (filter) has been created with the new dynamic                        measure. 
                 - The average and median waiting list have been created

Average waiting list formula: Average Wait List = AVERAGE (All_Data[Total])
![image](https://github.com/JeanBonheur01/PowerBI_Health_Care_P1/assets/131664311/7c38fce3-b2d3-4b39-8e27-d4fc371d1346)

Median Waiting List formula: Median Wait List = MEDIAN (All_Data [Total])
![image](https://github.com/JeanBonheur01/PowerBI_Health_Care_P1/assets/131664311/cf095299-7dbd-4c64-98d0-e6bacab5e3b6)

Avg/Med Wait List: The "SWITCH" and "VALUES" functions have been used to enable interection with the different buttons or measures (Average vs. Median). 
Formula: Avg/Med Wait List = SWITCH(VALUES('Calc Method'[Calc Method]), "Average", [Average Wait List], "Median", [Median Wait List])
![image](https://github.com/JeanBonheur01/PowerBI_Health_Care_P1/assets/131664311/af87c7b1-a32e-43d2-a02d-7c8bf786ee54)

- Different filters to enable the filtration/interaction of the data/table:
1. Archive date; 2. Case_Type (filtered as a drop-down), Speciality (filtered as a drop-down). 
 
- Donut chart: the donut chart is dynamic thanks to the created dynamic measure. 
Average/Median of Case_type visualized in donut chart, and showing the procentage of the inpatient, day_case and outpatient waiting lists.

- Stacked column chart: shows the relationship between the time bands and age profile. Age profil in the legende section, Time bands in the X-axis, and the Avg/Med waiting List dynamic measure on the Y-axis.
  
- Multi-row card: the table showing the filtered top 5 waiting List (By value: Avg/Med Waiting List) by speciality (field/area).
  
- Two line charts: shows the monthly trend Inpatient/Day_case vs. OutPatient. Archive date on the X-axis and Sum [Total] in the Y-axis. One chart is filtered for visualizing only Impatient/Day_case data and another chart only shows the outpatient data.
  
- Navigation button to the next page (Detailed page)
  This is the small information button on the image, when putting the mouse on it the following information appears: "click to view detailed page"

#### Image of the summary page: 

<img width="852" alt="Summary_view" src="https://github.com/JeanBonheur01/PowerBI_Health_Care_P1/assets/131664311/0b97fec4-657c-4954-a576-9cfdfc86d0e4">

#### 2. Detailed Page

- Different filters to enables the filtration/interaction have been implemented.

Desired filters has been created to interact with the detailed matrix table that displays various informations. 

- The metrix view displays different forms of detailed data.

Case_type is shown in the column function, Sum of total in the Vlue functions, and other relevant values on the rows-side (e.g Archive date).

- Return button: This enables the user to easily navigate back to the main summary page. 

#### Image of the Detailed Page

<img width="837" alt="Detailed_view" src="https://github.com/JeanBonheur01/PowerBI_Health_Care_P1/assets/131664311/4abd9b2e-fb33-4c05-99e1-6461d66f8926"> 

#### 3. Drilldown page

#### Image of Drilldown page

### Conclusion 

The Dashboard has undergone an aesthetically pleasing process to enhance its beauty and improve the overall user experience. For example avoiding null value data or blank values when filtering. In this project, the visualisation design/format was adopted from an extern plattform "stocked.adobe.com", and colors were extracted in another plattform "color.adobe.com". The extracted colors were then used in the PowerPoint platform to design bakgrounds, which were ultimately implemented in my Power BI dashboard. 
