# 04 – Data Structure Definition (DSD)

## What is a DSD?

A **Data Structure Definition (DSD)** is the **blueprint of your dataset**.  
It tells us:
- Which **concepts** are used as **dimensions**  
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

## When is a concept a dimension or an attribute?

- Use a **dimension** when the value *changes the identity of the observation*.  
  - Example: `SEX` → Male vs Female are **different series**.  
- Use an **attribute** when the value is *extra information*, not part of the identity.  
  - Example: `UNIT_MEASURE` → “Persons” or “EUR” are just describing the value.  

👉 Rule of thumb:  
If removing it would make two observations look the same but mean different things → it must be a **dimension**.  
If it only explains the number further → it’s an **attribute**.

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

## Example series key

Observation: “Female population of İstanbul in 2025 = 9 million persons”  

Series key (dimensions only):  
`FREQ=M • REF_AREA=IST • TIME_PERIOD=2025-01 • INDICATOR=POP • SEX=F`

Measure:  
`OBS_VALUE = 9,000,000`

Attribute:  
`UNIT_MEASURE = PERS`

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

## 💡 Tiny practical exercise

Try to describe this sentence in DSD terms:

**“The GDP of France in 2024 (annual, current prices) is 3,200 billion EUR.”**

- Dimensions: `REF_AREA=FR`, `TIME_PERIOD=2024`, `FREQ=A`, `INDICATOR=GDP`  
- Measure: `OBS_VALUE=3,200,000,000,000`  
- Attributes: `UNIT_MEASURE=EUR`, `PRICE_TYPE=CURRENT`

---

## TL;DR

- DSD is the **formal definition** of how data is structured.  
- **Dimensions** = define the identity of observations.  
- **Measure** = the actual value.  
- **Attributes** = extra information about the value.  
- Deciding if a concept is dimension or attribute is the most important modelling step.  

---  
[Next Chapter: Dataflow](https://github.com/kurtaranexpress/sdmx/blob/main/guides/en/05%20-%20Dataflow.md)
