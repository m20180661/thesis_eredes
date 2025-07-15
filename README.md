# thesis_eredes

This repository contains all code and supporting resources used in the master's thesis:

**"Optimizing Energy Analytics: A Dimensional Modelling Approach for Enhanced Decision-Making"**  
Master’s in Information Management – Business Intelligence Specialization  
**NOVA Information Management School (NOVA IMS)**  
By **Vitor André Jóia Aires**, July 2025

---

## 🧭 Project Overview

This thesis proposes a dimensional data warehouse architecture for analyzing open energy datasets provided by **E-REDES**, the Portuguese electricity distribution operator. Using the **Medallion architecture** (Bronze → Silver → Gold) in **Microsoft Fabric**, the solution enables analytical insights on consumption patterns, electric mobility infrastructure, renewable energy deployment, and service reliability across Portugal.

The architecture follows the **Kimball methodology**, supporting incremental builds, reusable conformed dimensions, and Power BI reporting.

---

## 📁 Repository Structure

/notebooks/
│ bronze_layer.ipynb # Raw data ingestion from E-REDES APIs and CSV exports
│ silver_layer.ipynb # Data cleaning, normalization, and surrogate key generation
│ gold_layer.ipynb # Fact and dimension table creation in Fabric Warehouse

/pbix/
│ report_final.pbix # Final Power BI dashboard (optional)

/figures/
│ architecture_diagram.png # Architecture diagram used in the thesis


---

## 🧱 Modeled Tables

### 📊 Fact Tables
| Table                          | Description |
|-------------------------------|-------------|
| `fact_energyconsumption_hourly`    | Hourly consumption per grid zone (zipcode level) |
| `fact_energyconsumption_municipality` | Daily/monthly aggregated consumption by municipality |
| `fact_energyconsumption_zipcode`     | Daily aggregated consumption by postal code |
| `fact_electricmobility`              | Infrastructure metrics for EV chargers per municipality |
| `fact_serviceinterruptions`         | SAIDI, SAIFI and reliability metrics per year and municipality |
| `fact_energyproduction`             | Daily renewable energy injected into the grid |
| `fact_evimpact`                     | Estimated EV impact on grid load (composite indicators) |
| `fact_loadbalance`                  | Net consumption vs. production per area |
| `fact_serviceorders`                | Monthly breakdown of service orders and grid interventions |
| `fact_gridoperations`              | Operational metrics related to switching, outages, etc. |
| `fact_renewableadoption`           | Adoption of renewable production units per tech/type |
| `fact_renewablegoals`              | Long-term policy targets by region and technology |

### 🧭 Dimension Tables
| Table            | Description |
|------------------|-------------|
| `dim_date`           | Calendar reference with full hierarchy (day/month/year/quarter) |
| `dim_municipality`   | Geographic reference by municipality, with area and location data |
| `dim_parish`         | Sub-municipality level (freguesia) for fine-grained analysis |
| `dim_zipcode`        | Zipcode-based reference for high-resolution consumption mapping |
| `dim_servicetype`    | Classification of electricity services (e.g., HT, MT, LT) |
| `dim_technology`     | Renewable energy technologies (e.g., wind, solar) |
| `dim_policy`         | Energy policy framework, targets, and implementation metadata |

> All surrogate keys (SKs) are generated using SHA-256 hashing on standardized name combinations, ensuring uniqueness and enabling conformed joins across fact and dimension tables.

---

## ⚙️ Platform and Tools

- **Microsoft Fabric**
  - OneLake (Delta Lake Storage)
  - Spark Notebooks (ETL with PySpark)
  - SQL-based Warehouse (Star Schema)
- **Power BI**
  - Dashboards connected directly to the Fabric Warehouse
- **E-REDES Open Data Portal**
  - Source of all open datasets (via API or CSV exports)
- **Python / PySpark**
  - Used for all transformation logic and table construction

---

## 📘 License

This repository is licensed under the **MIT License**. See the [LICENSE](./LICENSE) file for more details.

---

## 📩 Author Contact

**Vitor André Jóia Aires**  
Email: [m20180661@novaims.unl.pt]  
Affiliation: NOVA Information Management School  
GitHub: [https://github.com/m20180661/thesis_eredes](https://github.com/m20180661/thesis_eredes)
