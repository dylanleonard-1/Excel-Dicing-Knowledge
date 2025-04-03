# Excel Dicing Knowledge  
_Interactive Lookups, Logic, and Enrichment for Vendor Risk Simulation_

This module is designed to simulate the real-world process of transforming raw vendor vulnerability data into actionable, enriched information using Microsoft Excel. You'll practice lookups, logic-based analysis, conditional formatting, SLA tracking, and dynamic filtering—skills essential to third-party risk analysts.

---

## **Section 1: XLOOKUP / VLOOKUP Breakdown**

### **Use Case:**  
You receive a second file with `Patch_Status` and `Exploit_Published` for each CVE. You need to bring that into your main inject file.

### **Modern Approach – `XLOOKUP`**
```excel
=XLOOKUP([@CVE_ID], PatchList!A:A, PatchList!B:B, "Not Found")
```

| Component              | Meaning                                               |
|------------------------|-------------------------------------------------------|
| `[@CVE_ID]`            | CVE you're matching from your main sheet             |
| `PatchList!A:A`        | Column in patch sheet with the CVE IDs               |
| `PatchList!B:B`        | The value to return (e.g. Patch Status)              |
| `"Not Found"`          | Value to return if no match is found                 |

---

### **Legacy Approach – `VLOOKUP`**
```excel
=VLOOKUP([@CVE_ID], PatchList!$A$2:$C$100, 2, FALSE)
```

- `2` means “return from 2nd column”
- `FALSE` enforces exact match only

---

## **Section 2: SLA Breach Tracking**

Track if a vendor failed to respond in time based on `Days_Since_Last_Contact`.

### **Basic Example:**
```excel
=IF(Days_Since_Last_Contact > 10, "Breach", "On Time")
```

### **Advanced Logic:**
```excel
=IF(AND(Exposure_Confirmed="Yes", Days_Since_Last_Contact>7), "SLA Breach", "OK")
```

---

## **Section 3: Risk Tiering by CVSS**

Automatically assign a severity based on CVSS score.

```excel
=IF(CVSS_Score>=9, "Critical",
 IF(CVSS_Score>=7, "High",
 IF(CVSS_Score>=5, "Medium", "Low")))
```

---

## **Section 4: Conditional Formatting for Fast Triaging**

### **Highlight Critical Vendors:**
- Rule: Highlight if `CVSS_Score >= 8` and `Patch_Available = "No"`

#### **Formula to Use:**
```excel
=AND($CVSS_Score>=8, $Patch_Available="No")
```

> Use: `Home > Conditional Formatting > New Rule > Use a formula`

---

## **Section 5: Filters and Pivot Tables**

### **Filter Examples:**
- `Region = Asia`  
- `Patch_Available = No AND Exposure_Confirmed = Yes`

### **Pivot Table Suggestions:**
- **Rows:** Risk_Level, Region  
- **Values:** Count of CVEs, Avg. MTTR  
- **Filters:** Patch Availability, SLA Breach

> Use Pivot Tables to generate summaries used in your dashboards or outreach reports.

---

## **Section 6: Practice Lab Suggestions**

Use real generated injects to:
- Enrich fields using lookups
- Flag vendors with overdue response timelines
- Track remediation efforts by region or LOB
- Build manual dashboards in Excel or Power BI

---

## **Coming Soon to This Module**
- Excel file with formulas pre-applied
- Visual overlays explaining each function
- Training-mode scenario injects + grading key

---

### **This section prepares you to be the Excel brain of your team.**  
When you master dicing data like this, the rest of the process becomes automatic.
