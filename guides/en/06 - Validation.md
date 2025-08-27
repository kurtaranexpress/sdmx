# 06 – Validation

## Why do we need validation?

Once we define a Data Structure Definition (DSD) and start preparing data, there is always a risk of inconsistencies or mistakes. Validation ensures that:

- Every value is consistent with its defined concept and code list  
- Mandatory dimensions are always present  
- Time series and frequency information follow the expected format  
- Values match the correct data type (e.g., integer, decimal, string)  

Without validation, data can be published with hidden errors, reducing trust and usability.

---

## Typical validation checks

1. **Code list consistency**  
   Every dimension value must exist in the referenced code list.  
   - Example: If `SEX` dimension only has `M` (Male) and `F` (Female), any value like `X` is invalid.

2. **Mandatory dimensions**  
   All required dimensions must be included in the key.  
   - Example: If `TIME_PERIOD` is missing, the observation cannot be processed.

3. **Value type checks**  
   Observations must match the declared data type in the DSD.  
   - Example: Population must be an integer, not a text like `"ten million"`.

4. **Frequency alignment**  
   The reported period must match the declared frequency.  
   - Example: A monthly dataset (`M`) cannot have an annual observation (`2025` instead of `2025-01`).

---

## Example: Invalid vs. valid record

### Invalid
| REF_AREA | SEX | TIME_PERIOD | VALUE   |
|----------|-----|-------------|---------|
| TR       | X   | 2025        | 82M     |

Problems:  
- `X` is not in the code list for SEX.  
- `2025` is not in the correct monthly format (`YYYY-MM`).  
- `82M` is not a valid integer.  

---

### Valid
| REF_AREA | SEX | TIME_PERIOD | VALUE   |
|----------|-----|-------------|---------|
| TR       | M   | 2025-01     | 82000000 |

---

## How validation is performed

Validation can be done at different levels:

- **Local validation tools**: Spreadsheet checks, scripts, or database constraints  
- **SDMX Validation services**: Tools like the SDMX Validator or .Stat Suite’s validation modules  
- **Registry-based validation**: Ensures submitted data matches the DSD and associated metadata in the registry  

---

## Practical tips

- Always start validation with **small datasets** before publishing large volumes.  
- Use **official SDMX validators** for interoperability.  
- Automate validation in the workflow (e.g., CI/CD pipeline or ETL process).  
- Keep track of **error reports** and share them with data providers for correction.  

---

✅ Validation is not just about finding mistakes – it’s about guaranteeing that your data can be trusted, reused, and integrated across institutions.

[Next Chapter - Postman](https://github.com/kurtaranexpress/sdmx/blob/main/guides/en/07%20-%20Postman.md)

