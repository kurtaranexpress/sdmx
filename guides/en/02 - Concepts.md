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

Imagine three organisations publish population data:  
- **Türkiye (TURKSTAT)** writes “Türkiye”  
- **OECD** writes “TR”  
- **Eurostat** writes “TUR”  

Which one is correct?  
If everyone uses their own labels, **data cannot be compared or combined**.  

---

## The solution: registries  

To solve this, SDMX uses **registries**.  
A registry is like a **dictionary of official concepts and codes**, so that everyone uses the same words.  

There are three levels of registries:  
1. **Global registries** → for concepts valid across all statistics.  
2. **International registries** → for organisations such as **Eurostat SDMX Registry** or **OECD SDMX Registry**.  
3. **National or regional registries** → for institution-specific or country-specific needs.  

**Rule of thumb:** Always reuse from the global level first, then go to international or national only if needed.  

---

## Cross-domain concepts (CDC)  

These are the shared vocabulary used in many datasets:  
- `REF_AREA` → country or region (ISO codes like TR, FR)  
- `TIME_PERIOD` → time of observation (year, quarter, month)  
- `FREQ` → frequency (A, Q, M)  
- `UNIT_MEASURE` → unit of measure (persons, EUR, index)  
- `OBS_VALUE` → the actual number  

---

## Extending with local concepts  

If global concepts don’t cover your case, you add international, national, or regional ones.  

Example:  
**“The female population of İstanbul in 2025 is 9 million.”**  
Here, `SEX` is needed → this is an **extended concept**.  

---

## Example Concept Scheme  

| Concept ID    | Name            | Description                                | Level                  |
|---------------|-----------------|--------------------------------------------|------------------------|
| `REF_AREA`    | Reference area  | Country/region (TR, FR, İstanbul)          | Global (CDC)           |
| `TIME_PERIOD` | Time period     | Year, quarter, month of observation        | Global (CDC)           |
| `FREQ`        | Frequency       | Periodicity (A/Q/M)                        | Global (CDC)           |
| `UNIT_MEASURE`| Unit of measure | Unit (persons, index, EUR)                 | Global (CDC)           |
| `OBS_VALUE`   | Observation     | The numeric value                          | Global (CDC)           |
| `INDICATOR`   | Indicator       | What is measured (Population, GDP, CPI)    | International/National |
| `SEX`         | Sex             | Female, Male, Total                        | International/National |

---

## Key message  

- Concepts are the **language of data**.  
- Registries make sure everyone uses the **same words**.  
- Always reuse global concepts first, then international, and only extend nationally or locally when necessary.  

[Next Chapter - Codelists](https://github.com/kurtaranexpress/sdmx/blob/main/guides/en/03%20-%20Codelists.md)
