```markdown
# Technical Report — Final Project
**Course:** Cloud Computing
**Semester/YEAR:** (Your Semester/Year)
**Team:** (Your Names)

---

## 1. Introduction

**Problem:** Analyzing climate trends in large urban centers is a challenge that requires continuous data collection and processing. Many analyses are performed manually or with legacy systems that are difficult to maintain.

**Motivation:** To use the cloud computing paradigm to create a scalable, automated (via CI/CD), and low-cost (serverless) system for climate monitoring.

**Objectives:**
1.  Develop a serverless data pipeline in Microsoft Azure.
2.  Implement data collection from an external API (OpenWeatherMap).
3.  Store raw and processed data in Azure Blob Storage.
4.  Process and transform data using Azure Functions.
5.  Automate deployment using GitHub Actions.
6.  Visualize processed data in a Power BI dashboard.

**Applied Context:** The system can be used by data analysts, weather enthusiasts, or even for urban planning to understand temperature and humidity patterns in different capital cities.

## 2. Dataset

**Source:** The primary data source is the "Current Weather Data" API provided by OpenWeatherMap. This API delivers real-time meteorological data in JSON format.

**Description:** For this project, we will make API calls for 5 pre-defined cities (e.g., São Paulo, Rio de Janeiro, Brasília, Salvador, Manaus). The collection will be scheduled to run daily.

**Schema (Processed):** The raw JSON will be transformed into a tabular schema (as described in `README.md`) containing `city`, `collection_timestamp_utc`, `temperature_c`, `humidity_perc`, and `weather_condition`.

**Required Transformations:**
* Extraction of key fields from the JSON (e.g., `main.temp`, `main.humidity`, `weather[0].description`).
* Conversion of temperature from Kelvin (API default) to Celsius.
* Conversion of the Unix timestamp to ISO 8601 format.
* Creation of a unique ID for each processed record.

## 3. Solution Architecture
*(To be completed later)*

... (rest of the report sections) ...
