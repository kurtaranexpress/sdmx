# 04 – Data Structure Definition (DSD)

## What is a DSD?

A **Data Structure Definition (DSD)** is the **blueprint of your dataset**.  
It tells us:
- Which **concepts** are used as dimensions  
- Which concept is the **measure** (the actual value)  
- Which concepts are **attributes** (extra information)  
- Which **codelists** each dimension/attribute uses

In short:  
**Concepts = language → Codelists = vocabulary → DSD = grammar**

---

## Dimensions, Measure, Attributes

- **Dimensions**  
  Identify *where, when, what* the observation refers to.  
  Together they form the **series key**.  
  Example: `REF_AREA`, `TIME_PERIOD`, `FREQ`, `INDICATOR`, `SEX`.

- **Measure**  
  The actual data value.  
  Usually called `OBS_VALUE` in SDMX.  
  Example: `9,000,000` (female population of İstanbul in 2025).

- **Attributes**  
  Provide additional info about the observation or series.  
  Example: `UNIT_MEASURE` = “Persons”.

---

## Example DSD: Population

### Dimensions
| Position | Concept ID  | Linked Codelist | Example values                |
|----------|-------------|-----------------|--------------------------------|
| 1        | FREQ        | CL_FREQ         | A, Q, M                        |
| 2        | REF_AREA    | CL_AREA         | TR, FR, IST (if local codes)   |
| 3        | TIME_PERIOD | (time format)   | 2025, 2025-Q1, 2025-01         |
| 4        | INDICATOR   | CL_IND          | POP                            |
| 5        | SEX         | CL_SEX          | F, M, T                        |

### Measure
| Concept ID | Description                    |
|------------|--------------------------------|
| OBS_VALUE  | The numeric value (e.g. 82,000,000) |

### Attributes
| Concept ID    | Linked Codelist | Example values |
|---------------|-----------------|----------------|
| UNIT_MEASURE  | CL_UNIT         | PERS, MILP     |

---

## How DSDs enable validation

Because each dimension/attribute is linked to a codelist:
- Only valid codes can be used in keys.  
- Systems can check consistency (e.g. `M` frequency requires `YYYY-MM` format).  
- Attributes like `UNIT_MEASURE` ensure clarity across datasets.

---

## Example series key

Observation: “Female population of İstanbul in 2025 = 9 million persons”  

Series key (dimensions only):  
`FREQ=M • REF_AREA=IST • TIME_PERIOD=2025-01 • INDICATOR=POP • SEX=F`

Measure:  
`OBS_VALUE = 9,000,000`

Attribute:  
`UNIT_MEASURE = PERS`

---

## Notes on best practice

- **Order of dimensions matters** → defined in the DSD, used in keys.  
- **DimensionAtObservation** parameter controls how dimensions are exposed in data queries (flat vs nested).  
- **Keep DSDs stable** → changing dimension order or codelist links breaks comparability.  
- **Document your DSD** → publish a short note in plain language.

---

## 🔎 Simple analogy: DSD as an Excel sheet

Think of your dataset as an Excel table:

| Country | Year | Sex | Indicator | Value | Unit |
|---------|------|-----|-----------|-------|------|
| Türkiye | 2025 | F   | POP       | 9,000,000 | Persons |

- **Dimensions = columns that describe the observation** (Country, Year, Sex, Indicator)  
- **Measure = the main value column** (Value)  
- **Attributes = extra notes** (Unit)  

The DSD is just the **formal definition of this table**.

---

## 💡 FAQ for beginners

**Q: Why do we separate “measure” from “dimensions”?**  
A: Because the measure is the number you want to analyse. The dimensions are the “labels” that explain it.  

**Q: Can I have more than one measure?**  
A: Usually not in SDMX. Better to use one measure (`OBS_VALUE`) and if you need different variables (e.g. population & GDP), model them as indicators.  

**Q: What if I forget an attribute like Unit?**  
A: Then users may misinterpret your value (e.g. “9” → 9 persons? 9 thousand? 9 million?). Always keep units explicit.

---

## 🧩 Tiny practical exercise

Try to describe this sentence in DSD terms:

**“The GDP of France in 2024 (annual, current prices) is 3,200 billion EUR.”**

- Dimensions: `REF_AREA=FR`, `TIME_PERIOD=2024`, `FREQ=A`, `INDICATOR=GDP`  
- Measure: `OBS_VALUE=3,200,000,000,000`  
- Attributes: `UNIT_MEASURE=EUR`, `PRICE_TYPE=CURRENT`

---

## TL;DR

- DSD is the **formal definition** of how data is structured.  
- It combines concepts and their codelists into **dimensions, measure, attributes**.  
- It enforces validation, enables queries, and ensures your dataset is understood globally.
---
[Next Chapter: Dataflow](https://github.com/kurtaranexpress/sdmx/blob/main/guides/en/05%20-%20Dataflow.md)
