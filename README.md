# 🏭 Smart Factory OEE Analytics

## 📝 Opis Projektu
**Smart Factory OEE Analytics** to projekt typu End-to-End realizujący proces Business Intelligence: od surowych danych po gotowy raport zarządczy. System symuluje działanie procesów produkcyjnych i umożliwia analizę kluczowego wskaźnika efektywności – **OEE (Overall Equipment Effectiveness)**.

**Struktura repozytorium:**
Repozytorium stanowi agregację kodów źródłowych dwóch modułów w celu prezentacji pełnego potoku danych (Data Pipeline):
1. **Moduł Python** – generator danych telemetrycznych i symulator pracy maszyn.
2. **Moduł SQL** – hurtownia danych oraz warstwa transformacji ETL.

Projekt demonstruje skalowalną architekturę analityczną: **Generator ➡ Baza SQL (Star Schema) ➡ Power BI**.

---

## 🛠️ Technologie

* **Python (PyODBC):** Skrypt odpowiadający za symulację pracy maszyn. Pobierane są cykle produkcyjne, generowane są losowe zdarzenia awaryjne oraz statusy kontroli jakości (braki/dobre sztuki).
* **SQL Server (T-SQL):** Magazyn danych zaprojektowany w oparciu o model gwiazdy (**Star Schema**). W celu sprawdzenia jakości generowanych danych telemetrycznych utworzono Procedurę Składowaną (`LoadTelemetry`), która przy nieprawidłowych wartościach loguje błąd do tabeli ErrorLog. Wykorzystano Widoki (`Views`) do agregacji danych i przygotowania warstwy semantycznej.
* **Power BI:** Warstwa wizualizacji danych. Zastosowano miary DAX, funkcję Drill-through oraz formatowanie warunkowe w celu diagnostyki przyczyn spadków wydajności.

---

### Panel Główny (Executive)
![Executive Dashboard](img/ExecutiveDashboard.png)
*Widok ogólny z możliwością filtrowania czasu i linii produkcyjnych.*

### Szczegóły Maszyny (Diagnostyka)
![Machine Details](img/DrillThrough.png)
*Widok szczegółowy wykorzystujący paski danych do analizy przyczyn awarii.*

---

## 📂 Struktura Plików

Projekt został podzielony na moduły funkcjonalne zgodnie z poniższym schematem:

```text
SmartFactory_OEE_Analytics/
│
├── img/                        # Zrzuty ekranu wykorzystywane w dokumentacji
│   ├── ExecutiveDashboard.png
│   └── DrillThrough.png
│
├── python/                     # Kod źródłowy generatora danych
│   ├── database/               # Moduł obsługi bazy danych
│   │   ├── db_connector.py     # Konfiguracja połączenia
│   │   └── db_insertion.py     # Logika zapisu rekordów
│   └── simulator/              # Główna logika symulacji
│       ├── data_generator.py   # Generowanie parametrów losowych
│       └── simulator.py        # Start symulacji
│
├── sql/                        # Skrypty T-SQL (Hurtownia Danych)
│   ├── 01_DDL_Create_Tables.sql          # Tworzenie struktury tabel
│   ├── 02_DML_Fill_Dim_Tables.sql        # Zasilanie wymiarów statycznych
│   ├── 03_DML_Fill_fct_ProductionPlan.sql
│   ├── usp_LoadTelemetry.sql             # Procedura składowana
│   ├── v_Daily_Availability.sql          # Widok liczący dostępność
│   ├── v_Daily_Performance.sql           # Widok liczący wydajność
│   ├── v_Daily_Quality.sql               # Widok liczący jakość
│   └── v_OEE_FactSheet.sql               # Widoki analityczne (Warstwa semantyczna)
│
├── SmartFactoryReport.pbix     # Gotowy plik raportu Power BI
└── README.md                   # Dokumentacja techniczna
```

ENG BELOW

# 🏭 Smart Factory OEE Analytics

## 📝 Project Description

Smart Factory OEE Analytics is an End-to-End project implementing a complete Business Intelligence process: from raw data to a ready-to-use executive report. The system simulates production processes and enables analysis of a key performance indicator – OEE (Overall Equipment Effectiveness).

---

Repository Structure:
The repository aggregates source code from two modules to present the full Data Pipeline:
**Python Module** – telemetry data generator and machine operation simulator.
**SQL Module** – data warehouse and ETL transformation layer.

The project demonstrates a scalable analytical architecture:
***Generator ➡ SQL Database (Star Schema) ➡ Power BI***

---

## 🛠️ Technologies

Python (PyODBC): Script responsible for simulating machine operations. Production cycles are retrieved, random failure events are generated, and quality control statuses (scrap/good parts) are assigned.

SQL Server (T-SQL): Data warehouse designed using a Star Schema model. To validate the quality of generated telemetry data, a Stored Procedure (LoadTelemetry) was created, which logs errors to the ErrorLog table when invalid values are detected. Views are used for data aggregation and preparation of the semantic layer.

Power BI: Data visualization layer. DAX measures, Drill-through functionality, and conditional formatting were applied to diagnose causes of performance drops.

### Main Panel (Executive)***
![Executive Dashboard](img/ExecutiveDashboard.png)
*Overview with time and production line filtering options.*

### Machine Details (Diagnostics)***
![Machine Details](img/DrillThrough.png)

*Detailed view using data bars to analyze failure causes.*

---

## 📂 File Structure

The project has been divided into functional modules according to the following structure:
```text
SmartFactory_OEE_Analytics/
│
├── img/                        # Screenshots used in documentation
│   ├── ExecutiveDashboard.png
│   └── DrillThrough.png
│
├── python/                     # Source code of the data generator
│   ├── database/               # Database handling module
│   │   ├── db_connector.py     # Connection configuration
│   │   └── db_insertion.py     # Record insertion logic
│   └── simulator/              # Main simulation logic
│       ├── data_generator.py   # Random parameter generation
│       └── simulator.py        # Simulation start
│
├── sql/                        # T-SQL scripts (Data Warehouse)
│   ├── 01_DDL_Create_Tables.sql          # Creating table structures
│   ├── 02_DML_Fill_Dim_Tables.sql        # Populating static dimensions
│   ├── 03_DML_Fill_fct_ProductionPlan.sql
│   ├── usp_LoadTelemetry.sql             # Stored procedure
│   ├── v_Daily_Availability.sql          # View calculating availability
│   ├── v_Daily_Performance.sql           # View calculating performance
│   ├── v_Daily_Quality.sql               # View calculating quality
│   └── v_OEE_FactSheet.sql               # Analytical views (Semantic layer)
│
├── SmartFactoryReport.pbix     # Final Power BI report file
└── README.md                   # Technical documentation
```

---

## 📬 Contact
Author: **Igor Sarnowski**
* LinkedIn: https://www.linkedin.com/in/igor-sarnowski-9921202a1/
* GitHub: https://github.com/1G4S
