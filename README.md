# 🎯 IT Support Ticket Desk Dashboard -  FP20 Analytics

### 📊 [Dashboard Link](https://app.powerbi.com/view?r=eyJrIjoiOTU4YmU1NGItODcyOC00MjE2LTk3MGQtNDNlMTA5YTI1ZTU0IiwidCI6IjQ2NTRiNmYxLTBlNDctNDU3OS1hOGExLTAyZmU5ZDk0M2M3YiIsImMiOjl9)

## 📌 Problem Statement

This Power BI dashboard analyzes customer support operations across ticket volume, resolution times, SLA compliance, and tag-based insights. It helps support teams identify operational bottlenecks, monitor high-priority cases, and make data-driven decisions to improve service quality.

---

### 📷 Dashboard Snapshots

Page 1:

![image](https://github.com/user-attachments/assets/767f0df8-4b40-4ba8-8e0d-b346587eec1c)

Page 2:

![image](https://github.com/user-attachments/assets/fc0c3cdd-4576-4b4c-a3a7-b6c92c59b4eb)

Tooltip: Page 1

![image](https://github.com/user-attachments/assets/13659ecd-99a5-4013-ac1d-f4c17982c5c7)

Tooltip: Page 2

![image](https://github.com/user-attachments/assets/8c3c0082-6e27-411b-8209-50815db0c34a)

---

## 📄 Pages Included

| Page No. | Page Name                        |
|----------|----------------------------------|
| 1        | Ticket Operations Overview       |
| 2        | Tag Insights & Regional Analysis |

---

## 🧩 Key Visuals and Features

### ✅ IT Support Operations Overview
- **KPI Cards**: Total Tickets, Avg. Resolution Time, High Priority %, SLA Breach %
- **Ribbon Chart**: Tickets by Type & Queue
- **Line and bar combo Chart**: Ticket Volume Over Time
- **Table**: Breakdown by Primary Tag (volumes, resolution time, SLA status)
- **Slicers**: Type, Country, Priority, Queue

### ✅ Tag Insights & Regional Analysis
- **Map**: Ticket Volumes by Country
- **Word Cloud**: Top 50 Tags by Frequency
- **Bar Chart**: Co-tag Frequency
- **Tree Map**: SLA Breach % by Queue
- **Interactive Slicers** for deeper insights

---

## ⚙️ DAX Measures & Expressions

```DAX
Resolution Time (Days) = DATEDIFF('TicketData'[Date], 'TicketData'[Resolution Date], DAY)

Avg. Resolution Time (Days) = 
AVERAGEX(
    CALCULATETABLE(
        TicketData,
        TREATAS(VALUES(AllTagsTable[Ticket ID]), TicketData[Ticket ID])
    ),
    DATEDIFF(TicketData[Date], TicketData[Resolution Date], DAY)
)

High Priority Tickets = CALCULATE(COUNTROWS('TicketData'), 'TicketData'[Priority] = "High")

% High Priority Tickets = DIVIDE([High Priority Tickets], [Total Tickets (Filtered by Tag)], 0)

SLA Breach = IF([Avg. Resolution Time (Days)] > 3, "Breach", "Within SLA")

SLA Breach % = 
DIVIDE(
    CALCULATE(
        COUNTROWS(TicketData),
        DATEDIFF(TicketData[Date], TicketData[Resolution Date], DAY) > 3
    ),
    COUNTROWS(TicketData),
    0
)

Total Tickets (Filtered by Tag) = CALCULATE(DISTINCTCOUNT(AllTagsTable[Ticket ID]))

Longest Resolution Time (Max) = MAX('TicketData'[Resolution Time (Days)])
Shortest Resolution Time (Min) = MIN('TicketData'[Resolution Time (Days)])
```

---

## 📊 Tables & Relationships

- **Main Tables Used:**
  - `TicketData` (main fact table)
  - `AllTagsTable` (tag-level data)
  - `Dates` (time intelligence)
  - `Key Measures` (for metrics)
  - `Tags 2 Parameter` (filter control)
  - `CoTagKey Table` (tag pairing frequency)

- **Relationships:**
  - Date → TicketData[Date] (1:*)
  - TicketData[Ticket ID] → AllTagsTable[Ticket ID] (1:*)
  - CoTagKey Table relates tag pairs

## 📊 Data Model
![image](https://github.com/user-attachments/assets/f203518a-1fa4-47f4-9b1f-71fd34e7a097)


---

## 🔍 Insights Uncovered

- High volumes were observed in queues like **Tech Support** and **Product Support**.
- Co-tagging patterns like **“IT | Tech Support”** and **“Performance | Tech Support”** appeared frequently, helping to identify recurring issue clusters.
- **Belgium** and **Sweden** emerged as top countries by ticket volume.
- Co-tagging reveals frequent overlaps in **technical** categories
---

## 🚀 Tech Stack

- Power BI Desktop & Service
- DAX for data modeling
- Power Query for ETL
- ZoomCharts Custom Visuals
- Excel for source files
- Bookmark Navigator & Tooltip Pages

---

Feel free to reach out if you'd like to collaborate, explore insights, or know more about building dashboards like this! 😊

