# 02 – Concept Scheme

## From numbers to concepts

When you model data, you need to decide **what details** describe your number.  
Example:  
- **82,000,000** → just a number.  
- **“Türkiye’s population in 2025 is 82 million”** → now it has meaning:
  - Country = Türkiye
  - Year = 2025
  - Indicator = population
  - Value = 82,000,000

Each of these details (country, year, indicator, value) is a **concept**.  
Creating and organising these concepts is what we call **modelling**.

---

## Why do we need registries?

Think of a **dictionary**: instead of everyone inventing their own words, we share a common set of definitions.  
A **registry** in SDMX works like that dictionary: it stores and publishes standard concepts, codelists, and structures.

There are different levels of registries:
1. **Global registry:** contains concepts shared internationally.  
2. **Domain registry:** for specific subject areas (labour, demography, prices).  
3. **Local/institutional registry:** concepts created for your office or project.

**Rule of thumb:**  
👉 Always check if the concept already exists in a global or domain registry **before** creating a local one.  
This way, other people can understand your data without translation.

---

## Cross-domain concepts (CDC)

Some concepts are so common that they are reused everywhere.  
SDMX defines them as **cross-domain concepts** (CDC) — the “shared vocabulary” of official statistics.

Examples:  
- `REF_AREA` → country/region (ISO codes)  
- `TIME_PERIOD` → time of observation (YYYY, YYYY-Qn, YYYY-MM)  
- `FREQ` → frequency (Annual, Quarterly, Monthly)  
- `UNIT_MEASURE` → unit of measure (e.g. persons, EUR)  
- `OBS_VALUE` → the actual data value  

If you use these, someone in another country can read your dataset immediately, even if they don’t speak your language.

---

## Adding local concepts

Sometimes you need extra details that are not covered by CDC.  
Example:  
- “The **female** population of İstanbul in 2025 is 9 million.”  
- Here we need a **SEX** concept, which is domain-specific (demography).  

So your Concept Scheme may combine:
- **Global concepts (CDC):** REF_AREA, TIME_PERIOD, FREQ, UNIT_MEASURE, OBS_VALUE  
- **Local concepts:** INDICATOR, SEX  

---

## Example Concept Scheme for Population

| Concept ID    | Name             | Description                                           | Level          |
|---------------|------------------|-------------------------------------------------------|----------------|
| `REF_AREA`    | Reference area   | Country or region (e.g. Türkiye, İstanbul, France)    | Global (CDC)   |
| `TIME_PERIOD` | Time period      | Year/quarter/month of the observation                 | Global (CDC)   |
| `FREQ`        | Frequency        | Periodicity of observation (Annual/Quarterly/Monthly) | Global (CDC)   |
| `UNIT_MEASURE`| Unit of measure  | Persons, households, index, etc.                      | Global (CDC)   |
| `OBS_VALUE`   | Observation      | The numeric value (e.g. 82,000,000)                   | Global (CDC)   |
| `INDICATOR`   | Indicator        | Subject measured (Population, GDP, CPI)               | Local/domain   |
| `SEX`         | Sex              | Female, Male, Total                                   | Local/domain   |

---

## Key message

- **Concepts = the language of your dataset.**  
- Use the **shared vocabulary first (CDC)**, then add local terms only if needed.  
- This ensures your data can be read, compared, and integrated internationally.
