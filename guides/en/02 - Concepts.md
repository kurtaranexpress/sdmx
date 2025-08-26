# 02 – Concept Scheme

## From numbers to concepts

When we say:  
**“The population of Türkiye in 2025 is 82 million”**,  

we can identify the following **concepts**:  
- Country (Türkiye)  
- Year (2025)  
- Indicator (Population)  
- Value (82,000,000)  
- Unit (Persons)  

Every observation is just a combination of such concepts.  
This activity of defining the details is called **modelling**.

---

## The problem: everyone invents their own labels

Imagine three countries publish population data:  
- Türkiye uses “Türkiye”  
- Spain uses “TR”  
- France uses “TUR”  

Which one is correct? If everyone defines their own labels, **data cannot be compared or integrated**.  

---

## The solution: registries

To solve this, SDMX uses **registries**.  
A registry is like a **dictionary of official concepts and codes**, so that everyone uses the same words.

There are levels of registries:  
1. **Global registry** → contains concepts valid across all domains (cross-domain concepts).  
2. **Domain registries** → for subject areas (e.g. demography, national accounts).  
3. **Local registries** → institution-specific concepts.

**Rule of thumb:** Always check the global registry first, then go to domain or local level if needed.

---

## Cross-domain concepts (CDC)

These are the “shared vocabulary” of statistics — reusable concepts across all datasets:  
- `REF_AREA` → country or region (uses ISO codes, e.g. TR, FR)  
- `TIME_PERIOD` → time of observation (YYYY, YYYY-Qn, YYYY-MM)  
- `FREQ` → frequency (A/Q/M)  
- `UNIT_MEASURE` → unit of measure (persons, EUR, index)  
- `OBS_VALUE` → the actual statistical value  

---

## Extending with local concepts

If the global registry doesn’t cover your need, you extend with domain or local concepts.  
Example:  
**“The female population of İstanbul in 2025 is 9 million.”**  
Here, `SEX` is required → this is a **domain-specific** concept.  

---

## Example Concept Scheme

| Concept ID    | Name             | Description                                           | Level          |
|---------------|------------------|-------------------------------------------------------|----------------|
| `REF_AREA`    | Reference area   | Country/region (TR, FR, İstanbul)                     | Global (CDC)   |
| `TIME_PERIOD` | Time period      | Year, quarter, month of observation                   | Global (CDC)   |
| `FREQ`        | Frequency        | Periodicity (A/Q/M)                                   | Global (CDC)   |
| `UNIT_MEASURE`| Unit of measure  | Unit (persons, index, EUR)                            | Global (CDC)   |
| `OBS_VALUE`   | Observation      | The numeric value                                     | Global (CDC)   |
| `INDICATOR`   | Indicator        | What is measured (Population, CPI, GDP)               | Domain/local   |
| `SEX`         | Sex              | Female, Male, Total                                   | Domain/local   |

---

## Key message

- Concepts are the **language of your data**.  
- Registries ensure everyone speaks the **same language**.  
- Always reuse global concepts first, extend only when necessary.  
