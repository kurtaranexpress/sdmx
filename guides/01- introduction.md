# 01 – Introduction: Why Metadata Matters?

## A number without meaning

Take the number:

**82,000,000**

On its own, this number is meaningless. What does it represent? For which year? For which country?

---

## Turning data into information

When we say:

**“The population of Türkiye in 2025 is 82 million.”**

Now the value has *metadata*:
- **Indicator:** Population
- **Reference area (REF_AREA):** Türkiye
- **Time period (TIME_PERIOD):** 2025
- **Value (OBS_VALUE):** 82,000,000
- **Unit:** Persons

---

## Adding more detail

Consider another statement:

**“The female population of İstanbul in 2025 is 9 million.”**

New dimension needed:
- **Indicator:** Population
- **Reference area (REF_AREA):** İstanbul
- **Time period (TIME_PERIOD):** 2025
- **Sex (SEX):** Female
- **Value (OBS_VALUE):** 9,000,000
- **Unit:** Persons

---

## Lesson learned

- Same value can be described with **different levels of detail**.  
- The statistical office decides *what dimensions* are needed.  
- **Modellers** come in **after** this decision, to design concepts, codelists, and structures.

➡️ Next step: define a **Concept Scheme** to capture the meaning of these dimensions.
