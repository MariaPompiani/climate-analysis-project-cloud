# Project: Cloud-Based Weather Analysis System with Azure

**Team**
* Student Name 1 — ID — Email
* Student Name 2 — ID — Email (if applicable)

---

## General Description

This project is a data analysis system for weather monitoring. The objective is to collect, store, process, and visualize meteorological data from major Brazilian capitals using Microsoft Azure services. The system is automatically deployed via GitHub Actions and can be run locally using Docker.

**Problem Analysed:** Analysis of temperature and humidity trends across different regions in Brazil.
**System Objective:** "A data analysis dashboard for climate data with daily updates."

## Dataset

* **Data Source:** [OpenWeatherMap - Current Weather Data API](https://openweathermap.org/current)
* **Expected Data Volume:** Small. Daily collection of ~5 JSON records (one for each capital city).
* **Dataset Licensing:** Free for non-commercial use (OpenWeatherMap "Free" Plan).

## Data Model (Schema)

The system will capture a complex JSON from the API but will process it into the following simplified format, which will be stored in the `processed-data` container:

| Column | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `city` | String | Name of the queried city | "São Paulo" |
| `collection_timestamp_utc` | Datetime | Timestamp of data collection (UTC) | "2025-10-24T12:00:00Z" |
| `temperature_c` | Float | Temperature in Celsius | 22.5 |
| `humidity_perc` | Integer | Relative air humidity | 80 |
| `weather_condition` | String | Brief weather description | "Clouds" |
| `collection_id` | String | Unique identifier (e.g., GUID) | "a1b2c3d4-..." |

## Solution Architecture

(Paste the Mermaid code from Step 1.3 here)

```mermaid
graph TD;
    subgraph "Local Environment (Development)"
        Dev[<i class='fa fa-user'></i> Developer] -- Codes & Tests --> Docker(Docker Desktop)
        Docker -- Contains --> FuncLocal(Local Azure Functions)
    end

    subgraph "CI/CD (Automation)"
        Dev -- Git Push --> GitHub(GitHub Repo)
        GitHub -- Triggers --> Actions(GitHub Actions)
    end
    
    subgraph "Azure Cloud (Production)"
        Actions -- Deploys Code --> FuncApp(Azure Function App)
        Actions -- Deploys Infra --> IaC(Bicep/ARM Template)
        IaC -- Provisions --> FuncApp
        IaC -- Provisions --> Storage
        IaC -- Provisions --> PowerBI(Power BI Workspace)

        FuncApp -- Contains --> F1(Func: Collector - Timer)
        FuncApp -- Contains --> F2(Func: Processor - Blob)
        
        F1 -- Calls --> API(OpenWeatherMap API)
        API -- Responds (JSON) --> F1
        F1 -- Saves (Raw JSON) --> Storage(Blob Storage: /raw-data)
        
        Storage -- Triggers (New Blob) --> F2
        F2 -- Reads (Raw JSON) --> Storage
        F2 -- Saves (Clean CSV/JSON) --> Storage(Blob Storage: /processed-data)
        
        PowerBI -- Imports --> Storage
        PowerBI -- Displays --> Dashboard(Online Dashboard)
    end

    Dashboard -- Viewed by --> EndUser[<i class='fa fa-chart-bar'></i> End User]
