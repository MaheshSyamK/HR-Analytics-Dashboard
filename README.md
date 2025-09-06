# HR Analytics Dashboard – Power BI

## Project Overview
This project is an **interactive HR Analytics Dashboard** built in **Power BI** to visualize and analyze employee attendance, work-from-home trends, and sick leaves.  
It helps HR teams and management quickly understand workforce presence and absenteeism patterns over time.

---

## Features
- **KPI Cards**: Summary of employee presence, WFH %, and Sick Leave %.  
- **Trend Analysis**: Stacked area charts showing monthly trends in attendance.  
- **Detailed Tables**:  
  - Employee-wise day-of-week attendance breakdown  
  - Presence, WFH, and Sick Leave details  
- **Interactive Filtering**:  
  - Month filter to view data for specific periods  
  - Department filter (optional)  
- **Drill-through and Cross-filtering**: Click on tables or charts to view detailed insights.

---

## Data Used
- **Dummy HR dataset** containing:  
  - Employee names  
  - Dates (attendance records)  
  - Status values: P (Present), WFH, HWFH (Half WFH), SL (Sick Leave), WO/HO (Non-working days)  

> ⚠️ All data is anonymized for privacy.

---

## Visuals
- KPI cards for overall presence, WFH, SL percentages  
- Stacked area charts for attendance trends  
- Heatmap-style table for day-of-week attendance  
- Employee-level tables with detailed attendance

![Dashboard Screenshot](./screenshots/dashboard.png)

---

## DAX Measures Used
```DAX
-- Example: Count of Sick Leave
SickLeaveCount = SUMX(
    'Final Data',
    SWITCH(
        TRUE(),
        'Final Data'[Value] = "SL", 1,
        'Final Data'[Value] = "HSL", 0.5,
        0
    )
)

-- Working Days
TotalDays = COUNTROWS('Final Data')
NonWorkingDays = CALCULATE(
    COUNTROWS('Final Data'),
    FILTER('Final Data', 'Final Data'[Value] IN {"WO", "HO"})
)
WorkingDays = [TotalDays] - [NonWorkingDays]
