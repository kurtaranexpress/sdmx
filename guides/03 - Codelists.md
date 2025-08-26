# 03 – Code Lists (making metadata readable & computable)

## Why code lists?

We made our number meaningful with metadata (country, year, indicator…).  
But **how do we make that metadata understandable by everyone and usable by machines**?

Think of colours: saying *“mavi”* or *“kırmızı”* depends on language.  
A **code** like `BLU` or `RED` is language-neutral.  
**Code lists** are dictionaries that map short, stable **codes** to human-friendly labels (in many languages).

**Benefits**
- **Clarity:** one concept value → one unambiguous code (no “Türkiye/Turkey/TR” chaos)  
- **Compute-friendly:** faster queries, joins, filters (codes as keys)  
- **Validation:** invalid values can be rejected automatically  
- **Multilingual:** same code, labels in many languages  
- **Interoperability:** others can merge/use your data without translation  

As with concepts, follow **global → domain → local**.

---

## Global first: reuse standard lists

Whenever possible, reuse **cross-domain / international** lists:

| Concept        | Typical global codelist            | Example codes                           |
|----------------|------------------------------------|-----------------------------------------|
| `FREQ`         | `CL_FREQ`                          | `A` (Annual), `Q` (Quarterly), `M` (Monthly) |
| `REF_AREA`     | ISO 3166 (countries/areas)         | `TR` (Türkiye), `FR` (France)           |
| `TIME_PERIOD`* | SDMX time formats (not a codelist) | `2025`, `2025-Q1`, `2025-01`            |
| `UNIT_MEASURE` | global or domain unit lists        | `PERS` (Persons), `EUR`, `INDEX`        |

\* Time uses **formats**, not enumerated codes; still standardized.

Reusing global lists means an analyst in Spain or France immediately understands your dataset keys.

---

## Then extend locally (only if needed)

If your domain requires extra detail, create **domain/local** codelists:

- `SEX` → `F` (Female), `M` (Male), `T` (Total)  
- `INDICATOR` → `POP` (Population), `CPI`, `GDP`…  

Keep them **short, stable, documented**, and versioned.

---

## Example: population dataset – minimal set

### Global / shared lists

**`CL_FREQ`**
| Code | English label | Description            |
|------|----------------|------------------------|
| A    | Annual         | Yearly observations    |
| Q    | Quarterly      | Quarter observations   |
| M    | Monthly        | Month observations     |

**`REF_AREA`** (excerpt from ISO 3166)
| Code | English label |
|------|---------------|
| TR   | Türkiye       |
| FR   | France        |

**`UNIT_MEASURE`**
| Code | English label  | Notes                  |
|------|----------------|------------------------|
| PERS | Persons        | Count of persons       |
| MILP | Million persons| Persons / 1,000,000    |

---

### Local / domain lists

**`CL_SEX`**
| Code | English label |
|------|---------------|
| F    | Female        |
| M    | Male          |
| T    | Total         |

**`CL_IND`**
| Code | English label         | Notes                   |
|------|-----------------------|--------------------------|
| POP  | Population (headline) | Resident population      |

## How code lists connect to the model

- **Concepts** define meaning (e.g., `REF_AREA`, `SEX`).  
- **Code lists** enumerate valid values for those concepts.  
- In the DSD you explicitly link a dimension or attribute to a codelist:
  - `REF_AREA → CL_AREA`  
  - `FREQ → CL_FREQ`  
  - `SEX → CL_SEX`  
  - `INDICATOR → CL_IND`

This ensures:
- Only **valid keys** are possible.  
- Queries and filters are precise.  
- Data can be validated automatically.

---

## Governance & versioning

Good practice rules:  
- **Stable codes:** once published, never change codes; update labels instead.  
- **Short IDs:** avoid spaces, stick to `[A–Z0–9_]`.  
- **Versioning:** maintain versions like `CL_IND (v1.0)`, note changes.  
- **Mappings:** if you migrate from legacy codes, publish a mapping table.  
- **Deprecation:** mark codes as deprecated but keep them until users migrate.

---

## Validating incoming data

Simple rules to check data against codelists:  
- Every observation key must use codes from the linked codelist.  
- Time formats must match frequency (e.g. `M` → `YYYY-MM`).  
- Units must be consistent within a series (or explicitly given as attributes).  

Start small:  
- First validate `REF_AREA`, `FREQ`, `TIME_PERIOD`.  
- Then extend to `SEX`, `INDICATOR`, `UNIT_MEASURE`.

---

## TL;DR

- **Concepts = what something means.**  
- **Code lists = which values are valid.**  
- Always reuse global codelists first, extend locally only if needed.  
- Version and document codelists so others can trust and reuse your data.


---

## CSV examples (ready to use)

`data/example_codelist.csv`

```csv
codelist_id,code,name,description,lang
CL_FREQ,A,Annual,Yearly observations,en
CL_FREQ,Q,Quarterly,Quarterly observations,en
CL_FREQ,M,Monthly,Monthly observations,en
CL_AREA,TR,Türkiye,ISO 3166 code,tr
CL_AREA,FR,France,ISO 3166 code,en
CL_UNIT,PERS,Persons,Count of persons,en
CL_UNIT,MILP,Million persons,Persons / 1,000,000,en
CL_SEX,F,Female,,en
CL_SEX,M,Male,,en
CL_SEX,T,Total,,en
CL_IND,POP,Population (headline),Resident population,en



---


