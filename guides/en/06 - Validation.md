# 06 – Validation

## From design to checks

We designed the **DSD** and decided how to **publish** via a Dataflow.  
Now we must check whether the data is **correctly formatted and consistent**.  
That is the role of **validation**.

---

## Why do we need validation?

Validation ensures that:
- Every value matches its **concept and code list**.
- **Mandatory dimensions** are always present.
- **Time formats** match the **frequency** (e.g., `M` → `YYYY-MM`).
- The **measure** has the correct **data type** (integer/decimal/text, etc.).

Without validation, hidden errors reduce trust and usability.

---

## Two layers of validation (keep it simple)

1) **Structural (schema-based) validation**  
   Uses the **DSD**, **codelists**, and (if provided) **constraints**.  
   - Keys use only **allowed codes**.  
   - Required dimensions (e.g., `REF_AREA`, `TIME_PERIOD`) are present.  
   - `TIME_PERIOD` format aligns with `FREQ`.  
   - `OBS_VALUE` matches its declared representation (integer/decimal).

2) **Business-rule validation**  
   Rules about **meaning**, not just format. Examples:  
   - `SEX=T` equals `M + F`.  
   - Rates are within plausible ranges.  
   - Series are internally consistent over time.

> For business rules you can write checks in a **standard, shareable language (VTL)**,  
> or implement them in **your local scripts** if that’s easier for your workflow.

---

## Invalid vs valid (minimal example)

**Invalid**
| REF_AREA | SEX | TIME_PERIOD | OBS_VALUE |
|----------|-----|-------------|-----------|
| TR       | X   | 2025        | 82M       |

Problems:
- `X` is not in the `CL_SEX` code list.
- `2025` is not a monthly format (`YYYY-MM`).
- `82M` is not a valid integer.

**Valid**
| REF_AREA | SEX | TIME_PERIOD | OBS_VALUE |
|----------|-----|-------------|-----------|
| TR       | M   | 2025-01     | 82000000  |

---

## How to perform validation (practical paths)

- **Use metadata-driven tools**  
  Run validation against the **DSD + codelists (+ constraints)** from your registry/platform.

- **Adopt VTL for shareable business rules**  
  Express cross-checks (e.g., totals, ranges) in a **standard** way that others can reuse.

- **Or script it locally**  
  Quick to implement; great for pipelines and CI/CD. Keep rule docs next to the code.

---

## A simple workflow

1. **Fetch structures** used by the Dataflow (DSD, codelists, constraints).  
2. Run **structural checks** (keys, formats, data types).  
3. Run **business-rule checks** (VTL or local scripts).  
4. Produce an **error report** (line, field, reason) and fix before publishing.

---

## Tiny example in VTL

Check that the total equals male + female:

```vtl
-- Define a hierarchical rule for the SEX dimension
define hierarchical ruleset sex_hr (valuedomain rule SEX) is
    T = M + F
end hierarchical ruleset;

-- Apply the rule to the dataset
-- Assume: Population(REF_AREA, TIME_PERIOD, SEX, obs_value)
Population_errors := check_datapoint(
    ds := Population,
    ruleset := sex_hr,
    on := SEX,
    measure := obs_value
);
If the rule fails, Population_errors will return the records that violate it.

---

## TL;DR

- **Structural validation** = “Is the data shaped correctly?” (DSD/codelists/formats)  
- **Business validation** = “Does it make sense?” (totals, ranges, consistency)  
- Use **VTL** when you need a **standard, portable rule set**; or use local scripts when you need **quick, pragmatic** checks.

[Next Chapter - Postman](https://github.com/kurtaranexpress/sdmx/blob/main/guides/en/07%20-%20Postman.md)
