# Healthcare-analysis-dashboard
# 🏥 Healthcare Analytics Dashboard
### Power BI Report · `PROJECT.pbix`

> A multi-page, dark-themed Power BI dashboard built on a single `HealthcareData` entity, delivering end-to-end visibility into patient volumes, financial performance, clinical outcomes, and demographic segmentation — all with cross-page filtering via Blood Group and Doctor Department slicers.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Data Model](#data-model)
- [KPI Cards](#kpi-cards)
- [Report Pages](#report-pages)
  - [1 · Overview](#1--overview)
  - [2 · Financial Analysis](#2--financial-analysis)
  - [3 · Outcome](#3--outcome)
  - [4 · Demographs](#4--demographs)
- [Filters & Slicers](#filters--slicers)
- [Design & Theme](#design--theme)
- [Technical Details](#technical-details)

---

## Overview

| Property | Value |
|---|---|
| **Tool** | Microsoft Power BI (Fluent2-CY26SU04 theme) |
| **Pages** | 4 |
| **Canvas Size** | 1280 × 720 px (Fit to Page) |
| **Data Source** | `HealthcareData` table |
| **Date Range** | 2023 – 2024 (Admission Date) |
| **Navigation** | Page Navigator widget on every page |

---

## Data Model

All visuals draw from a single table: **`HealthcareData`**.

### 📊 Key Columns

| Column | Description |
|---|---|
| `Disease` | Diagnosis category (Fever, Heart Disease, Fracture, Stroke, Cancer, Diabetes) |
| `Severity_Level` | Mild · Moderate · Severe |
| `Age_Group` | Patient age bracket (e.g. 19–35, 36–60, …) |
| `Doctor_Department` | Cardiology · Neurology · Oncology · General Medicine |
| `Hospital_Name` | Name of the treating hospital |
| `Hospital_Type` | Govt / Private |
| `Admission_Type` | Type of admission |
| `Admission_Date` | Date hierarchy (Year → Month) |
| `Discharge_Status` | Discharged · Referred · Expired |
| `Blood_Group` | Patient blood group (slicer filter) |
| `Test_Name` | Diagnostic test performed |
| `Payment_Status` | Insurance / Patient payment status |
| `City` | Patient city |
| `Physician_Name` | Attending physician |
| `Physician_Specialization` | Physician specialty |
| `Readmission_Flag` | Readmission indicator |
| `Total_Cost` | Total treatment cost |

### 🔢 Calculated Measures

| Measure | Description |
|---|---|
| `TOTAL PATIENTS` | Count of all patient records |
| `Total Revenue` | Sum of revenue across all patients |
| `Total Medication Cost` | Aggregated medication spend |
| `Avg Length of Stay` | Average inpatient days |
| `Avg Cost per Patient` | Average treatment cost per patient |
| `Readmission Rate %` | Percentage of patients readmitted |
| `Pending Payment Rate %` | Percentage of payments still pending |
| `Severe Cases` | Count of Severity_Level = 'Severe' |
| `Total Readmissions` | Total readmission count |
| `Total Insurance Payment` | Sum of insurance-covered payments |
| `Total Patient Payment` | Sum of out-of-pocket payments |
| `Govt Patients` | Count of government hospital patients |
| `Private Patients` | Count of private hospital patients |
| `test count` | Count of diagnostic tests |

---

## KPI Cards

These **5 KPI cards** appear identically on **every page**, providing a persistent summary header across the report.

| 🃏 KPI Card | Measure | Colour Accent |
|---|---|---|
| 👥 **Total Patients** | `TOTAL PATIENTS` | Theme Blue |
| 📊 **Readmission Rate %** | `Readmission Rate %` | Cyan / Teal |
| ⏱️ **Avg Length of Stay** | `Avg Length of Stay` | Red (`#F22C2C`) |
| 💰 **Total Revenue** | `Total Revenue` | Pink (`#F81BAA`) |
| ⏳ **Pending Payment Rate %** | `Pending Payment Rate %` | Purple-Blue |

> All cards use a dark navy background (`#141C35`) with white font and callout areas enabled.

---

## Report Pages

### 1 · 🏠 Overview

> **Purpose:** High-level snapshot of patient distribution, disease burden, medication spend, and admission trends.

| Visual | Type | Fields |
|---|---|---|
| 🍕 Disease Distribution | Pie Chart | `Disease` → `TOTAL PATIENTS` |
| 🔵 Severity Breakdown | Pie Chart | `Severity_Level` → `Severe Cases` |
| 📊 Medication Cost by Dept | Column Chart | `Doctor_Department` → `Total Medication Cost` |
| 📈 Avg LOS by Hospital | Area Line Chart | `Hospital_Name` → `Avg Length of Stay` |
| 📉 Patients by Month | Line Chart | `month num` → `TOTAL PATIENTS` |
| 📆 Patients by Month (YoY) | Multi-series Line | `Admission_Date Month` × `Year` → `TOTAL PATIENTS` (2023 vs 2024) |
| 📊 Patients by Age Group | Clustered Bar Chart | `Age_Group` → `TOTAL PATIENTS` |
| 🏁 Discharge Status | Clustered Column Chart | `Discharge_Status` → `TOTAL PATIENTS` |
| 🧪 Test Count by Name | Stacked Area Chart | `Test_Name` → `test count` |
| 📋 Disease Cost Table | Table | `Disease` · `Sum of Total_Cost` |

**Slicers:** Blood Group (tile) · Doctor Department (tile)

---

### 2 · 💵 Financial Analysis

> **Purpose:** Deep-dive into cost metrics, payment breakdowns, revenue by geography, and department-level financial performance.

| Visual | Type | Fields |
|---|---|---|
| 💳 Payment Split | Donut Chart | `Total Insurance Payment` vs `Total Patient Payment` |
| 📊 Avg Cost by Dept (H-bar) | Bar Chart | `Doctor_Department` → `Avg Cost per Patient` |
| 🏙️ Patients by City | Clustered Column | `City` → `TOTAL PATIENTS` |
| 💰 Cost by Dept & Payment Status | Clustered Column | `Doctor_Department` × `Payment_Status` → `Avg Cost per Patient` |

**Slicers:** Blood Group · Doctor Department

---

### 3 · 🩺 Outcome

> **Purpose:** Clinical outcome analysis — readmissions, severity-discharge relationships, and disease-level patient matrices.

| Visual | Type | Fields |
|---|---|---|
| 🔁 Readmissions by Disease | Clustered Column Chart | `Disease` → `Total Readmissions` |
| 📊 Severity vs Discharge | 100% Stacked Bar | `Severity_Level` × `Discharge_Status` → `TOTAL PATIENTS` |
| 🔢 Disease × Severity Matrix | Pivot Table | `Disease` (rows) × `Severity_Level` (columns) → `TOTAL PATIENTS` |

**Slicers:** Blood Group · Doctor Department

---

### 4 · 👥 Demographs

> **Purpose:** Patient demographic profiling — age distribution, hospital type, admission patterns, and physician-level summaries.

| Visual | Type | Fields |
|---|---|---|
| 🎂 Patients by Age Group | Pie Chart | `Age_Group` → `TOTAL PATIENTS` |
| 🏥 Hospital Type Distribution | Donut Chart | `Hospital_Type` → `Govt Patients` vs `Private Patients` |
| 🚑 Admission Type | Donut Chart | `Admission_Type` → `TOTAL PATIENTS` |
| 💊 Treatment Type | Donut Chart | `Treatment_Type` → `TOTAL PATIENTS` |
| 👨‍⚕️ Physician Summary Table | Table | `Physician_Name` · `Physician_Specialization` · `TOTAL PATIENTS` · `Total Revenue` · `Avg Cost per Patient` · `Readmission_Flag` |

**Slicers:** Blood Group · Doctor Department

---

## Filters & Slicers

Two global slicers appear on **all 4 pages** in the left sidebar panel, enabling cross-page drill filtering:

| 🎚️ Slicer | Field | Style |
|---|---|---|
| 🩸 **Blood Group** | `Blood_Group` | Tile |
| 🏥 **Doctor Department** | `Doctor_Department` | Tile |

> Both slicers have `drillFilterOtherVisuals: true` — selections propagate to all visuals on the page.

---

## Design & Theme

| Property | Value |
|---|---|
| **Theme** | Fluent2-CY26SU04 (Microsoft Fluent 2) |
| **Background** | `#0A0F1E` (near-black navy) |
| **Panel / Card BG** | `#141C35` (dark navy) |
| **Nav Bar** | `#0F172A` |
| **Font** | Segoe UI · Bold · 24pt (title) |
| **Font Color** | White (`#FFFFFF`) |
| **Accent Colors** | Cyan `#00E5FF` · Pink `#FF4D8D` · Green `#10B981` · Amber `#FBBF24` · Orange `#F97316` · Purple `#7C3AED` |
| **Navigation** | Rounded-rectangle Page Navigator (top-right) |

---

## Technical Details

```
File:        PROJECT.pbix
Size:        ~381 KB
Format:      Power BI PBIX (ZIP archive)
Schema:      fabric/item/report/definition v3.2.0
Pages:       4  (afe166…, cbcb5d…, b68b0d…, 8b3756…)
Visuals:     ~100 visual containers across all pages
Last saved:  2026-05-12
```

### Visual Types Used

| Icon | Visual | Usage |
|---|---|---|
| 🃏 | Card (new) | KPI headers |
| 🍕 | Pie Chart | Disease & severity share |
| 🍩 | Donut Chart | Payment & demographic splits |
| 📊 | Column / Bar Chart | Department & city comparisons |
| 📈 | Line Chart | Trend over time |
| 📉 | Area Line Chart | LOS by hospital |
| 🎭 | 100% Stacked Bar | Severity × discharge |
| 🔢 | Pivot Table | Disease × severity matrix |
| 🧪 | Stacked Area Chart | Test counts |
| 📋 | Table | Cost & physician details |
| 🎚️ | Slicer (Tile style) | Blood Group & Department filter |
| 🧭 | Page Navigator | Cross-page navigation |

---

> **Built with** Microsoft Power BI · Fluent2 Theme · HealthcareData single-table model
