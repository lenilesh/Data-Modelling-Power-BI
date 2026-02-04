# Data-Modelling-Power-BI
##Introduction: Where Dashboards Go to Live… or Die
![Power BI](https://www.ackama.com/wp-content/uploads/2025/09/dd221adb-b6e3-46dd-8111-9bdfbb196676-scaled.jpg)
You can clean your data perfectly.  
You can build flashy visuals.  
You can even write clever DAX.

And yet… your Power BI report is **slow**, **confusing**, or worse — **wrong**.

Why?

Because behind every great Power BI dashboard is an unsung hero (or villain):  
👉 **the data model**.

Think of data modelling as the **plumbing of Power BI**. When it’s done right, everything flows smoothly. When it’s done badly, nothing works the way you expect. This article breaks down Power BI data modelling in plain language, covering schemas, fact and dimension tables, relationships, and why good modelling is critical for performance and accurate reporting — especially when working with real-world datasets like hospital records or Kenya Crops data.

---

## What Is Data Modelling in Power BI?

Data modelling is how you **structure tables and define how they connect** inside Power BI.

A good model determines:
- How filters move across tables
- How measures calculate values
- How fast your report runs
- Whether your numbers can be trusted


---

## Fact Tables vs Dimension Tables

At the heart of Power BI modelling are two table types.

---

### Fact Tables 📊

Fact tables store **events and measurements** things you want to analyse.

Examples:
- Hospital admissions
- Crop harvest volumes
- Patient visits
- Sales transactions

Typical characteristics:
- Many rows
- Numeric values (counts, totals, averages)
- Foreign keys linking to dimensions

FACT_Admissions
AdmissionID
PatientID
DepartmentID
DateID
LengthOfStay
Cost


---

### Dimension Tables 🧭

Dimension tables add **context and meaning** to facts.

Examples:
- Date
- Department
- Crop type
- Region

Typical characteristics:
- Fewer rows
- Descriptive columns
- One unique key per row

DIM_Department
DepartmentID
DepartmentName
HospitalWing


---

## Star Schema ⭐ (Power BI’s Best Friend)

The **star schema** is the gold standard for Power BI.

### Structure

- One central **fact table**
- Multiple **dimension tables**
- All dimensions connect directly to the fact table

        DIM_Date
           |
DIM_Patient — FACT_Admissions — DIM_Department
|
DIM_Doctor
![Power BI Star Schemer](https://learn.microsoft.com/en-us/power-bi/guidance/media/star-schema/star-schema-example1.png)

### Why Star Schema Works So Well

- Faster performance
- Simple relationships
- Cleaner filter flow
- Easier DAX calculations
- Easy to understand and maintain

---

## Snowflake Schema ❄️ (Looks Fancy, Works Harder)

Snowflake schema is a **normalised** version of the star schema.

### Structure

- Dimension tables are split into multiple related tables
- Creates extra joins and relationship chains

FACT_Admissions
|
DIM_Department
|
DIM_HospitalWing
![snowf flakes schemer](https://community.fabric.microsoft.com/t5/image/serverpage/image-id/42556iCD0D3F9E98807DA6?v=v2)

### Pros
- Reduces data duplication
- Can save storage

### Cons (in Power BI)
- Slower performance
- More complex relationships
- Harder DAX
- Filters can behave unexpectedly

📌
Snowflake schemas belong in databases — **star schemas belong in Power BI**.

---

## Relationships in Power BI 🔗

Relationships define **how tables talk to each other**.

### Best Practice Relationship Setup

- One-to-many (1:*)
- Many to one
- Many to many

### What Can Go Wrong?

Bad relationships can:
- Inflate totals
- Break slicers
- Cause ambiguous paths
- Slow down reports


## Why Good Data Modelling Is Critical 🚨

### 1. Performance
Star schemas reduce joins and memory usage, making reports faster.

### 2. Accuracy
Correct relationships ensure filters behave logically.

### 3. Simpler DAX
Good models reduce the need for complex CALCULATE and FILTER logic.

### 4. Scalability
Adding new KPIs or dimensions becomes easy instead of painful.

### 5. Trust
Decision-makers rely on reports — wrong numbers destroy confidence.

---

## Power BI Data Modelling Best Practices ✅

- Use **star schema whenever possible**
- Keep fact tables narrow
- Create a proper **Date table**
- Use numeric surrogate keys
- Avoid many-to-many relationships
- Avoid bi-directional filters
- Clean data in **Power Query**, not DAX

---

## Conclusion: Model First, Visualise Second 🎯

Data modelling is not optional in Power BI — it’s foundational. A well-designed model ensures performance, accuracy, and clarity, turning raw datasets into reliable insights.

Before adding visuals or writing DAX, always ask:  
**Does my model make sense?**

Because in Power BI, great dashboards don’t start with charts —  
**They start with the model.**
