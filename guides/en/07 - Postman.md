# 07 – Querying and Testing with Postman

## Why Postman?

Postman is a simple but powerful tool for testing APIs.  
Since SDMX services are RESTful endpoints, Postman can be used to:

- Build and send queries without writing code  
- Inspect responses in JSON, XML, or CSV  
- Validate parameters and keys before embedding queries in production  
- Share examples with colleagues or data providers  

---

## Basic SDMX request in Postman

1. Open Postman  
2. Create a new `GET` request  
3. Paste the endpoint, for example:
https://example.org/sdmx-json/data/DF_POP_MONTHLY/M.TR.POP.F?startPeriod=2024

4. Click **Send**  
5. Check the JSON response in the lower panel

---

## Using query parameters

Common SDMX query parameters include:

- `startPeriod` → first period to include  
- `endPeriod` → last period to include  
- `dimensionAtObservation` → controls whether dimensions appear at series or observation level  
- `detail` → controls how much metadata is included (e.g. `full`, `dataonly`)  

Example:

GET https://example.org/sdmx-json/data/DF_POP_MONTHLY/M.TR.POP?startPeriod=2020&endPeriod=2024&detail=full

---

## Checking validation with Postman

- Try sending a request with a wrong code (e.g., `SEX=X`) → server should return an error.  
- Check that `startPeriod` matches your frequency (`YYYY` for annual, `YYYY-MM` for monthly).  
- Inspect the response headers for content type (`application/vnd.sdmx.data+json`).  

---

## Sharing collections

Postman allows you to save and share requests as **Collections**.  
- Create a collection `SDMX Examples`  
- Add requests for population, CPI, GDP, etc.  
- Share the collection JSON file with your team so they can import and run the same queries.  

---

## 🔑 Practical tips

- Always test new Dataflows in Postman before announcing them to users.  
- Save “golden examples” (queries that always work) to verify future changes.  
- Use environment variables in Postman (`{{baseUrl}}`, `{{apiKey}}`) so you can switch servers easily.  
- Check response times — large queries may need filtering or smaller scopes.  

---

## TL;DR

- Postman is perfect for **exploring and testing SDMX APIs**.  
- Start simple, then add parameters to refine queries.  
- Share collections with your team for consistent testing.  
- Use Postman as your **first validation step** before embedding queries in applications.

[Next Chapter - Modelling From Table](https://github.com/kurtaranexpress/sdmx/blob/main/guides/en/08-%20Modelling-from-table.md)

