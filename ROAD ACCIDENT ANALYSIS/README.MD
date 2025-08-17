# EXCEL-ROAD-SAFETY-ANALYSIS
Excel-based dashboard project analyzing UK road accident data (2021–2022) with KPI tracking, trend analysis, and VBA automation to open the Home page first. Covers severity, vehicle type, road type, and day/night casualty insights to deliver key road safety findings.
## 📊 Project Requirements
The dashboard was designed to provide insights into the following requirements:
1. **Primary KPI** – Total casualties after the accident
2. **Primary KPI's** – Total casualties & percentage of total with respect to accident severity, and maximum casualties by type of vehicle
3. **Secondary KPI's** – Total casualties with respect to vehicle type
4. **Monthly trend** – Comparison of casualties for Current Year (CY) vs Previous Year (PY)
5. **Maximum casualties** – By road type
6. **Distribution** – Total casualties by road surface
7. **Relation analysis** – Casualties by area/location & by day/night

## 📂 Contents
- `Road Accident Data.xlsx` — Raw data and pivot table-based analysis
- **Excel Dashboards** showcasing:
  - Severity vs. Casualties
  - Percentage breakdowns
  - Max casualties in each category
  - Year-over-year casualty comparison
  - Casualties by road type, surface, and time

## 🖥 VBA Automation
To enhance usability, the following VBA code ensures the **"Home"** sheet is displayed first when the workbook is opened:

```vba
Private Sub Workbook_Open()
    Worksheets("Home").Activate
End Sub
Note: Enable macros in Excel to allow this automation to run.

## 🚀 Key Insights
- Majority of cases fall under "Slight" severity  
- Fatal accidents are less frequent but critical  
- Casualty trends vary by road type and time of day  
- Dashboards provide actionable insights for road safety measures  

## 📸 Sample Visuals
*(Add screenshots of your Excel dashboards here)*

## 🔧 How to Use
1. Download the `.xlsx` file.  
2. Open in Microsoft Excel (enable macros for VBA functionality).  
3. Explore pivot tables, charts, and dashboards for interactive analysis.  

## 📥 Download Project File
Due to GitHub file size limits, the Excel file is hosted on Google Drive.  
[Click here to download the Road Accident Data Excel file]
https://drive.google.com/drive/folders/1D7fBrEsY5BwwYUyWhr_20yNqXZx4ku6b

[https://drive.google.com/drive/folders/1D7fBrEsY5BwwYUyWhr_20yNqXZx4ku6b](https://drive.google.com/file/d/1R9RAw_dH5CBawuy8aLeCgJAgFn35e7pn/view?usp=sharing)
---

**Author:** Kajal Panigrahi  
