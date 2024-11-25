# Healthcare Analytics

## Table of Contents

- [Problem Statement and Overall Objectives](#problem-statement-and-overall-objectives)
- [Data Sources](#data-sources)
- [Tools](#tools)
- [Data Cleaning/Preparation](#data-cleaningpreparation)
- [Exploratory Data Analysis](#exploratoty-data-analysis)
- [Data Analysis](#data-analysis)
- [Results/Findings](#resultsfindings)
- [Recommendations](#recommendations)
- [Limitations](#limitations)

### Problem Statement and Overall Objectives

The main purpose with this healthcare project is to track current status of patient waiting list by analyzing the historical monthly trend of waiting lists in inpatient and outpatient categories. A detailed speciality-level and age-profile analysis based on those groups will also be performed. 

NB! Inpatients are individuals who stay in a hospital under treatment, while outpatient only receive medical treatment whithout being admitted to a hospital. 

Data Scope: The data scope for this analysis will be between 2018 and 2021. 
Metrics Required: The required metrics is average & median waiting list, and finally the current total waitlist. 
View Required: A summary page presenting the above requirements and a detailed page for granular/detailed analysis. 

### Data Sources

The primary data used for this analysis are the inpatient and outpatients data, which are stored as xlsx files representing each year in respectives folders. The speciality group dataset is stored as CSV file. The first two large datasets have been uploaded as folders in Power BI, while the last one has been uploaded as a CSV file.

### Tools

- Microsoft Power BI: The tool is used to create comprehensive, interactive data visualizations and share important business insights. 
      [Learn more](https://www.microsoft.com/sv-se/power-platform/products/power-bi?ef_id=_k_cb76b16ddc2510de7ad4d7779827f495_k_&OCID=AIDcmmc1fckbp7_SEM__k_cb76b16ddc2510de7ad4d7779827f495_k_&msclkid=cb76b16ddc2510de7ad4d7779827f495&market=se)

- Adobe Stock [Find here](https://stock.adobe.com/search?k=dashboard&search_type=recentsearch)
- Color Adobe [Find here](https://color.adobe.com/sv/)
- PowerPoint
  
### Data Cleaning/preparation

In the initial data preparation phase, the following taks was performed: 

1. Data Collection/loading and inspection
Since there are multiple files, before loading data, some critical quality factors were checked such as column count and headers to ensure the data consistency. Then, the files were combined and loaded into Power BI.

2. Transformation & Modeling
- Handling of missing values
- Verifying and correcting data type
- Verifying dataset rows and columns between the orinigal and uploaded files
- Creating missing/needed columns
- Appending tables to create a new one

NB! Since the tranformation & modeling phase is iterative, this step was performed several times when different changes were needed to correct our data or format it visualization goals. 

- Once the tranformed data was uploaded, in the modeling view, the desired model/relationship was created between the datasets (All_data and Mapping_Specialty). Finally, unwanted/unusable tables were deleted or hidden from the report view to avoid confusion.

### Exploratory Data Analysis

EDA involved exploring the healthcare data to answer key questions, such as: 

- What is the total wait list of the current month, respective for the previous year's same month?
- What is the average and median values of the waitlist?
- What is the distribution of case types in terms of their average/median across the dataset?
- What is the distribution of the top 5 specialities in terms of their average/median across the dataset?
- What is the total amount of waitlist for each case type over time?  

### Data Analysis

- Before starting with the designing process, in the view module, the "Gridlines" and "Snap to grid" functions were enabled so the dashboard layout could be done easily and efficiently.

#### 1. Summary Page 

- Total waitlist of the current month:

The DAX option was used (Data Analysis Expression) by creating a new measure and entering both the name and the formula of that measure.

```DAX

Last Month Wait List = CALCULATE (SUM(all_Data[Total]), All_Data[Archive_Date] = Max(All_Data[Archive_Date])) + 0
```
NB! The new measure has been represented on a card at the top left of screen. 
0 is added to the formula to avoid a blank value in the visualization. 
  
- Total waitlist of the previous year's same month:
This is important for comparison with the current month/situation.

```DAX

PY Latest Month Wait List = CALCULATE(SUM(All_Data[Total]), All_Data[Archive_Date]=EDATE(MAX(All_Data[Archive_Date]), -12)) + 0
```
NB! To move to the previous month, the EDATE function was used. Since it represents the previous month of the last year, the formula has been substracted by -12 (12 month before the current month). 

- Average and median metrics to enable the statistical visualization of the waiting list

Since the interaction between the Average and Median metrics is necessary, a "dynamic measure" was created to enable this interactions whithin the entire visualization. 

Dynamic measure: - create a new table/rename/enter names of actual measure/Load
                 - Then, a slicer (filter) has been created with the new dynamic measure. 
                 - The average and median waiting list have been created

Average waiting list formula: 
```
Average Wait List = AVERAGE (All_Data[Total])
```
Median Waiting List formula: 
```
Median Wait List = MEDIAN (All_Data [Total])
```

Avg/Med Wait List formula: 
```
Avg/Med Wait List = SWITCH(VALUES('Calc Method'[Calc Method]), "Average", [Average Wait List], "Median", [Median Wait List])
```
NB! The "SWITCH" and "VALUES" functions was used to enable interection with the different buttons or measures (Average vs. Median). 

- Different filters to enable the filtration/interaction of the data/table:
      1. Archive date
      2. Case_Type (filtered as a drop-down)
      3. Speciality (filtered as a drop-down). 
 
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
- Return button: This enables the user to easily navigate back to the main summary page. 

#### Image of the Detailed Page

<img width="837" alt="Detailed_view" src="https://github.com/JeanBonheur01/PowerBI_Health_Care_P1/assets/131664311/4abd9b2e-fb33-4c05-99e1-6461d66f8926"> 

#### 3. Drilldown page
This was used to provide intuitive navigation and detailed view of information when visualizing the line chart. 
#### Image of Drilldown page

<img width="446" alt="Screenshot 2024-04-01 at 17 27 38" src="https://github.com/JeanBonheur01/PowerBI_Health_Care_P1/assets/131664311/679a7fd9-bd6c-4a23-a224-827fd417aca4">

#### Image of interaction between the summary page and drilldown page

<img width="851" alt="Screenshot 2024-04-01 at 17 34 03" src="https://github.com/JeanBonheur01/PowerBI_Health_Care_P1/assets/131664311/992dbcfa-00e9-4f4b-b2e6-30073509e769">

NB! When interacting with the line charts, a pop-up window of the created drilldown appears to show more detailed information about the total wait list and speciality wait list, filtered by time and case type. 

### Results/Findings

- The average waitlist of the current year was higher compared to the previous year's same month, possibly due to increased demand for healthcare services driven by factors like population growth, changing healthcare needs, etc.
  
- The current month's inpatient waitlist was lower than in the the same month of the previous year, suggesting potential improvements in inpatient services efficiency or a decreased demand for certain types of inpatient care.
  
- Outpatient represent approximately 70%, followed by day cases at approximately 15%, with inpatient cases making up he remaining percentage. Line charts also illustrate a significant increase in outpatient cases over the years, while inpatient and day cases remain stable with smooth fluctuations.
  
- In various time periods, there are more patients aged 16-64 on the waitlist, followed by those aged 0-15, and finally seniors aged 65 and older. This could indicate that middle-aged adults require more medical attention or are seeking healthcare services more frequently for various reasons. 
  
### Recommendations

- Implications for Healthcare Planning: The findings from the waitlist findings hightlight the importance of monitoring such data in healthcare planning and resource allocation. A higher average wait list overall suggests a potential need for additional resources or capacity expansion to meet growing demand. Conversely, a lower inpatient waitlist may indicate successful intervations to improve access to inpatient care or optimize resource utilization.
  
- Resource Allocation: With the majority of cases falling under outpatient case, the hospital could consider optimizing resources such as staff, equiment, clinics to accommodate this higher volume. This could involve extending clinic hours, improving appointment scheduling, and other efficiency measures.
  
- Efficiency improvement: While day cases represent a significant portion, they are relatively lower than outpatient cases. The hospital can strealine processes for day case procedures, such as enhancing pre-operative assessments and reducing waiting times.
  
- Speciality Considerations: Understanding the top 5 affected specialities is crucial for identifying causes and implementing effective solutions to decrease patient wait times and increase satisfaction.
  
- Inpatient Management: Although smaller percentage, inpatient cases require more resources and longer lenghts of stay. The hospital should ensure adequate resource capacities and implement strategies to reduce unnecessary hospitalizations.
  
- Regular monitoring: Continuous monitoring of case distribution trends allows for adapting strategies to changing patient demographics, healthcare needs, and resource availability. Implementing data_driven decision-making processes enables informed adjustements to optimize service delivery continually, enhancing efficiency and patient satisfaction while optimizing resuource utilization across different categories.
  
### Limitations

- Data collected from the internet may be biased or skewed, leading to biased results or conclusions.
  
- Statistical analysis and further investigation are needed to assess and determine wheter the observed differences are meaningful or simply due to random variation.

💻🖱️💻🖱️🤖🖱️🤖
