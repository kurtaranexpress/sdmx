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
