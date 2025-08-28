# 05 – Dataflow (Published Dataset)

## From DSD to Dataflow  

The **DSD** defines the **data structure** – it tells us how concepts, dimensions, and attributes fit together.  
But the DSD alone is just a *definition*.  

A **Dataflow** is a **presentation of actual data** built on top of a DSD.  
It says: *“Here is the dataset you can query, based on this structure.”*  

In short:  
- **DSD = structure** (blueprint of the dataset)  
- **Dataflow = presentation** (a published dataset using that structure)  

---

## Why Dataflows matter  

- A single DSD can give rise to **many different Dataflows** (e.g. “Annual Population” vs “Monthly Population”).  
- Dataflows make the scope explicit: users know which dataset is being offered.  
- They let you manage publication lifecycle without altering the underlying DSD.  

---

## The role of Cubes and Mapping  

To move from **DSD (definition)** to **Dataflow (publication)** we need an extra step:  

- **Cube**  
  In practice, a cube is the **physical dataset in the database**, organised by the DSD’s dimensions (like a multi-dimensional fact table).  
  *(Note: “cube” is not a formal SDMX standard term, but a common way of storing statistical data.)*  

- **Mapping**  
  Mapping connects the **database layer (cubes, tables, fields)** to the **DSD concepts and codelists**.  
  Without mapping, the system doesn’t know how raw database fields correspond to DSD concepts.  
  *(Note: “mapping” is an implementation layer concept, not part of the SDMX XML standard itself.)*  

👉 A Dataflow exists only when there is both:  
- A **DSD** (definition), and  
- A **Mapping to a cube** (link to actual stored data).  

---

## Minimal elements of a Dataflow  

Every Dataflow must contain:  
- **ID** (short and stable, e.g. `DF_POP`)  
- **Name** (multi-lingual, e.g. `Population – Monthly`)  
- **Description** (what the dataset is about)  
- **Reference to a DSD**  

In addition, organisations often provide **extra metadata** as annotations, such as:  
- Coverage period (e.g. `2015–present`)  
- Geographic scope (e.g. `countries + selected cities`)  
- Update frequency (e.g. `Monthly, T+30`)  
- Contact or license information  

---

## Example  

Our population DSD (`FREQ`, `REF_AREA`, `TIME_PERIOD`, `INDICATOR`, `SEX` → `OBS_VALUE`) can be connected to a **population cube** in the database.  
A mapping aligns database fields (`country_code`, `year`, `sex`) with DSD concepts (`REF_AREA`, `TIME_PERIOD`, `SEX`).  

Once mapped, it can be published as:  

**Dataflow:** `DF_POP_MONTHLY`  
- **DSD:** `DSD_POP`  
- **Description:** Monthly population data  
- **Scope (annotation):** `FREQ = M`, `INDICATOR = POP`, `2015–today`  
- **Contact (annotation):** `population-team@example.org`  

---

## How does it look for the user?  

GET {baseUrl}/sdmx-json/data/DF_POP_MONTHLY/M.TR.POP.F?startPeriod=2024


- `DF_POP_MONTHLY` = Dataflow ID  
- Underlying structure = `DSD_POP`  
- The mapping ensures that “TR” and “POP” are correctly linked to database fields  

---

## Lifecycle management  

- Don’t break the DSD when something changes → open a **new Dataflow** if needed.  
- Mark old flows as `deprecated` and clearly link to the new ones.  
- Archive old notes and scopes so users can still track history.  

---

## Simple analogy  

- **DSD = table schema** (the plan)  
- **Cube = physical data table** (the storage)  
- **Mapping = how schema fields link to database fields**  
- **Dataflow = the published dataset** (what users see and query)  

---

## In short  

- **DSD defines the structure, Dataflow is the published view of that structure.**  
- **Cubes** hold the actual data; **mapping** links cubes to DSD concepts.  
- A Dataflow always has ID, name, description, and a DSD reference.  
- Extra details (coverage, frequency, contact) are usually provided via **annotations**.  
- A single DSD can support many Dataflows, each with its own scope and lifecycle.  

[Next Chapter - Validation](https://github.com/kurtaranexpress/sdmx/blob/main/guides/en/06%20-%20Validation.md)
