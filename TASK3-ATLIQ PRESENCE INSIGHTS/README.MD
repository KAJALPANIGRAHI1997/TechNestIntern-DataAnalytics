# ATLIQ Presence Insights (Power BI)

A clean, interactive Power BI dashboard to monitor **Attendance %**, **Work From Home %**, and **Sick Leave %** across dates and weekdays for the ATLIQ workforce. Includes trend lines, KPI cards, slicers, and drill-through for employee-level details.

![Dashboard Preview](assets/atliq-presence-insights.png)

---

## 🔎 What this report answers
- What is the **overall Attendance% / WFH% / SL%** this period?
- How do these metrics **trend over time** (with dotted regression trend lines)?
- Which **day of week** performs better/worse?
- Which **employees** or dates need attention?

---

## 📂 Repository structure
atliq-presence-insights/
├─ /assets
│ └─ atliq-presence-insights.png # dashboard screenshot
├─ /data # (optional) anonymized sample CSVs
│ └─ final_data_sample.csv
├─ /sql # (optional) scripts used to prep data
│ └─ create_clean_tables.sql
├─ /pbix
│ └─ ATLIQ_Presence_Insights.pbix # main Power BI report
└─ README.md


> ⚠️ Real data is excluded for confidentiality. Add anonymized samples to `/data` if you want others to reproduce.

---

## 🧠 Data model (high level)
- **Fact table**: `Final Data` (Date, Employee ID, P (Present), WFH, SL, etc.)
- **Calendar table**: `Calendar` (Date, WeekNo, MMM YY, DayOfWeek, etc.)
- Relationship: `Final Data[Date]` → `Calendar[Date]` (Many-to-One, single direction)

---

## 📏 Measures (DAX)
> Adjust table/column names to match your model.

```DAX
-- Attendance %
[Attendance %] =
VAR PresentDays = SUM('Final Data'[P])
VAR WorkingDays = COUNTROWS('Final Data')
RETURN DIVIDE(PresentDays, WorkingDays)

-- WFH %
[WFH %] =
DIVIDE(SUM('Final Data'[WFH Count]), COUNTROWS('Final Data'))

-- SL %
[SL %] =
DIVIDE(SUM('Final Data'[SL Count]), COUNTROWS('Final Data'))

-- Month label (for visuals)
[MMM YY] = FORMAT(SELECTEDVALUE('Calendar'[Date]), "MMM yy")

📊 Key Visuals

- **KPI Cards:** Attendance %, WFH %, SL %
- **Small Multiples / Tiles:** % by day of week
- **Area Charts with Dotted Trend Lines:** Metric by Date
- **Slicers:** MMM YY, Date range
- **Table:** Employee ID, Attendance %, Present Days, WFH % (with totals)

▶️ How to Open

1. Install **Power BI Desktop** (July 2024 or later recommended).
2. Open `pbix/ATLIQ_Presence_Insights.pbix`.
3. If using your own data:
   - Replace the sample source in **Transform data → Data source settings**.
   - Ensure the date table is marked as **Date Table**.
   - Refresh.

⚙️ Optional SQL Prep

If you staged data in SQL first, include scripts in `/sql` and document any views used by the PBIX.

**Example Skeleton:**
```sql
CREATE VIEW vw_final_data AS
SELECT
  Date,
  EmployeeID,
  CASE WHEN Status = 'P' THEN 1 ELSE 0 END AS P,
  CASE WHEN Status = 'WFH' THEN 1 ELSE 0 END AS WFH_Count,
  CASE WHEN Status = 'SL' THEN 1 ELSE 0 END AS SL_Count
FROM raw_attendance;

🧽 Formatting & UX Choices

Rounded cards with soft shadows and a dark header band

Clear % data labels on area charts

Dotted regression trend line for quick direction sensing

Slicers for month grouping (MMM YY) and date navigation

🗂 Refresh / Maintenance

Verify calendar covers the entire reporting range

Check relationships after schema changes

Recalculate measures if business logic changes (e.g., exclude holidays)

📜 License

MIT — feel free to fork and adapt with attribution.

🙋‍♀️ Author / Contact

Kajal Panigrahi
For questions or collaboration, open a GitHub issue or reach out via LinkedIn / Email.
