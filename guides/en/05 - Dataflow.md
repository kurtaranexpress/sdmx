# 05 – Dataflow (Published Dataset)

## What is a Dataflow?

A DSD gives us the **plan** or the **schema**, but it’s not enough on its own.  
To tell users *“this is the dataset you can actually query”*, we define a **Dataflow**.

A Dataflow specifies:
- Which DSD it is based on  
- What the dataset is meant for  
- Which time periods and areas it covers  
- How often it is updated  
- Description, contact, and license information  

In short:
- **DSD → how the data is structured**  
- **Dataflow → which data is published**

---

## Why do we need Dataflows?

- You can publish **multiple products from the same DSD** (e.g. “Annual Population” vs “Monthly Population”).  
- It makes the scope explicit (e.g. “data available from 2015 onwards, city level included”).  
- It lets you manage the **publication lifecycle** without breaking the DSD (close an old flow, open a new one).  

---

## Minimal elements of a Dataflow

- **ID:** `DF_POP` (short and stable)  
- **Name:** `Population – Monthly`  
- **Description:** `Resident population, monthly`  
- **DSD reference:** `DSD_POP`  
- **Coverage:** `2015–present`, `countries + selected cities`  
- **Update frequency:** `Monthly, T+30`  
- **Contact:** `population-team@example.org`  
- **License:** `CC-BY 4.0`  

---

## Example

Our population DSD (FREQ, REF_AREA, TIME_PERIOD, INDICATOR, SEX → OBS_VALUE) can be published as:

**Dataflow:** `DF_POP_MONTHLY`  
- **DSD:** `DSD_POP`  
- **Description:** Monthly population data  
- **Scope:** `FREQ = M`, `INDICATOR = POP`  
- **Time:** `2015–today`  
- **Contact:** `population-team@example.org`  

---

## How does it look for the user?
GET {baseUrl}/sdmx-json/data/DF_POP_MONTHLY/M.TR.POP.F?startPeriod=2024


- `DF_POP_MONTHLY` = Dataflow ID  
- Underlying structure = `DSD_POP`  
- Key order = the sequence of dimensions in the DSD  

---

## Lifecycle management

- Don’t break the DSD when something changes → open a **new Dataflow** if needed.  
- Mark old flows as `deprecated` and clearly link to the new ones.  
- Archive old notes and scopes so users can still track history.  

---

## Documentation checklist

- [ ] Plain-language summary (what’s included / not included)  
- [ ] Dimension order and codelist references (link or small table)  
- [ ] Time coverage and update frequency  
- [ ] Known issues (breaks, rebases, etc.)  
- [ ] Contact & license  
- [ ] Copy-paste example request  

---

## Simple analogy

- **DSD = table schema**  
- **Dataflow = published view/product based on that schema**  

You can create multiple dataflows from a single schema for different purposes.

---

## 🔑 Practical tips

- Don’t hardcode years or scopes into IDs (`DF_POP_2025` is bad) → keep IDs stable, put details in description.  
- If users struggle to filter, **split into smaller flows** that are easier to understand.  
- Don’t create duplicate DSDs for the same concept → use one DSD, multiple Dataflows.  
- Always provide an **example query** on the Dataflow page — this alone reduces many support emails.  

---

## In short

- **DSD = structure**, **Dataflow = publication**.  
- A single DSD can support multiple Dataflows.  
- Explain the scope clearly, manage lifecycle openly, and give users example queries.  


[Next Chapter - Validation](https://github.com/kurtaranexpress/sdmx/blob/main/guides/en/06%20-%20Validation.md)

