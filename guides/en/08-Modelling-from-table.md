# 08 – Modelling from an Existing Table

## Why this matters

In practice, data rarely starts as a clean SDMX dataset.  
Most of the time you have an Excel sheet, a CSV file, or a database table.  
The challenge is: **how do we turn that table into a valid SDMX model?**

This is the *deductive approach*: starting from a dataset and mapping it to concepts, codelists, a DSD, and finally a Dataflow.

---

## Step 1 – Look at the table

Example table:

| Country | Year | Sex | Value |
|---------|------|-----|-------|
| TR      | 2025 | F   | 9,000,000 |
| TR      | 2025 | M   | 8,800,000 |

At first glance it looks simple, but we need to formalize it.

---

## Step 2 – Identify concepts

- `Country` → REF_AREA  
- `Year` → TIME_PERIOD  
- `Sex` → SEX  
- `Value` → OBS_VALUE  

Now we know which pieces are **dimensions** and which one is the **measure**.

---

## Step 3 – Check against global concepts

- `REF_AREA` → already a cross-domain concept  
- `TIME_PERIOD` → cross-domain, format must match the frequency  
- `SEX` → not global, but domain-specific (demography)  
- `OBS_VALUE` → the standard measure concept  

Tip: Always **start with global concepts**; only define local ones if nothing exists.

---

## Step 4 – Assign code lists

- `REF_AREA` → ISO 3166 (TR, FR, etc.)  
- `TIME_PERIOD` → YYYY, YYYY-Qn, YYYY-MM depending on frequency  
- `SEX` → CL_SEX (F, M, T) – we need to define this locally  
- `OBS_VALUE` → no codelist (it’s a numeric value)

---

## Step 5 – Build the DSD

From the mapping:

- **Dimensions:** REF_AREA, TIME_PERIOD, SEX  
- **Measure:** OBS_VALUE  
- **Attributes:** UNIT_MEASURE (e.g. Persons)  

Now we can formally describe the structure.

---

## Step 6 – Define the Dataflow

Finally, wrap the DSD in a Dataflow, e.g.:

- **ID:** DF_POP_SIMPLE  
- **Description:** Resident population by country, sex, and year  
- **Coverage:** 2015–present  
- **Update:** Annual  

---

## Example: Full mapping

| Table Column | Concept ID   | Type       | Linked Codelist |
|--------------|--------------|------------|-----------------|
| Country      | REF_AREA     | Dimension  | CL_AREA (ISO)   |
| Year         | TIME_PERIOD  | Dimension  | Time formats    |
| Sex          | SEX          | Dimension  | CL_SEX          |
| Value        | OBS_VALUE    | Measure    | –               |
| –            | UNIT_MEASURE | Attribute  | CL_UNIT         |

---

## 🔑 Practical tips

- **Don’t over-model.** Not every column in your source table must become a dimension. Keep only what matters for analysis.  
- **Start small.** Test the mapping with a few rows first.  
- **Legacy codes?** Always provide a mapping to global codes.  
- **Think about reusability.** If another dataset uses the same “Sex” breakdown, reuse the same CL_SEX.  
- **Document assumptions.** Future users will ask “why did you model it like this?”  

---

## TL;DR

- Start with your raw table.  
- Map each column to an SDMX concept (global first, local if needed).  
- Attach codelists.  
- Assemble the DSD.  
- Publish as a Dataflow.  

This way, any dataset — even a messy Excel sheet — can be transformed into an SDMX-compliant model.
