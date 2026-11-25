# GPS Tracker Fleet Violation and Idling Cost Engine

**An intelligent Python-based vehicle fleet monitoring and violation detection system using GPS telemetry data.**

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![Status](https://img.shields.io/badge/Project-Completed-success)
![Domain](https://img.shields.io/badge/Domain-IoT%20%7C%20Vehicle%20Telematics-orange)
![License](https://img.shields.io/badge/License-MIT-green)

---

## 1. Project Overview

The **GPS Tracker Fleet Violation and Idling Cost Engine** is a Python-based fleet monitoring system designed to process GPS telemetry data, detect vehicle violations, monitor driver behaviour, and calculate fuel costs associated with vehicle idling.

The system analyzes timestamped GPS records and identifies operational irregularities such as overspeeding, geofence violations, prolonged idling, night driving, and GPS signal loss.

It also calculates idling fuel consumption costs and generates daily driver performance reports, helping fleet operators improve vehicle utilization, monitor driver behaviour, and reduce unnecessary operational expenses.

The application follows a **command-file-driven architecture**, processing vehicle information, geographical zones, and GPS data from structured CSV files.

## 2. Problem Statement

Fleet operators face several challenges in monitoring vehicles efficiently:

- Difficulty tracking vehicle movement across predefined geographical boundaries.
- Overspeeding and unsafe driving behaviour.
- Fuel wastage caused by prolonged vehicle idling.
- Unauthorized or unusual vehicle activity during restricted hours.
- GPS connectivity interruptions and missing location updates.
- Lack of consolidated reports for evaluating driver performance.

This project addresses these challenges through automated GPS data processing, event detection, cost calculation, and daily reporting.

## 3. Key Features

### Vehicle and Fleet Management
- Register multiple vehicles with their respective driver details.
- Maintain vehicle-specific speed limits and idle fuel consumption rates.
- Associate vehicles with predefined geographical zones.

### GPS Data Processing
- Read and process timestamped GPS records from CSV files.
- Validate incoming GPS records.
- Handle invalid records, unknown vehicles, and out-of-order timestamps.

### Automated Violation Detection

The system detects five major event categories:

| Event | Description |
|---|---|
| GEOFENCE | Detects vehicles operating outside their assigned geographical boundaries. |
| OVERSPEED | Identifies vehicles exceeding their configured speed limits. |
| IDLING | Detects prolonged vehicle idling based on ignition and duration conditions. |
| NIGHT_DRIVE | Identifies vehicle movement during configured night hours. |
| GPS_LOST | Detects interruptions in GPS updates beyond the defined threshold. |

The system records event start and end timestamps and calculates event durations where applicable.

### Idling Cost Calculation
- Calculates fuel consumed during idling.
- Uses vehicle-specific idle fuel consumption rates.
- Estimates the associated fuel cost.
- Includes idling cost information in the generated reports.

### Driver Performance Scoring
- Generates daily driver performance scores.
- Evaluates vehicle activity using detected events.
- Produces consolidated fleet performance information.

### Automated Report Generation

The application generates three CSV reports:

| Report | Purpose |
|---|---|
| `event_log.csv` | Contains detected vehicle events and their details. |
| `daily_report.csv` | Provides daily vehicle statistics, idling costs, and driver scores. |
| `errors.csv` | Records invalid or rejected GPS records and processing errors. |

## 4. System Architecture

The project follows a modular architecture, separating GPS data processing, event detection, cost calculation, and report generation.

```text
                 INPUT DATA
                     |
          +----------+----------+
          |          |          |
       Vehicles    Zones     GPS Data
          |          |          |
          +----------+----------+
                     |
                     v
              DATA READER
                     |
                     v
             DATA VALIDATION
                     |
                     v
             EVENT DETECTION
                     |
       +-------------+-------------+
       |             |             |
    GEOFENCE      OVERSPEED      IDLING
       |             |             |
       +-------------+-------------+
                     |
          +----------+----------+
          |                     |
       NIGHT DRIVE           GPS LOST
          |                     |
          +----------+----------+
                     |
                     v
             COST CALCULATION
                     |
                     v
           DRIVER SCORE ENGINE
                     |
                     v
             REPORT GENERATION
                     |
          +----------+----------+
          |          |          |
       Event Log  Daily Report  Errors
          CSV        CSV         CSV
```

## 5. Technology Stack

| Technology | Usage |
|---|---|
| Python 3.10+ | Core programming language |
| CSV | Input data and report storage |
| Python Standard Library | Data processing, timestamps, calculations, and file handling |
| Unittest | Unit testing and validation |
| Git | Version control |
| GitHub | Source code hosting |

## 6. Project Structure

```text
E019-ECE-013/
│
├── data/
│   ├── vehicles.csv
│   ├── zones.csv
│   ├── gps_data.csv
│   ├── pings.csv
│   ├── commands.txt
│   └── README.md
│
├── src/
│   ├── __init__.py
│   ├── data_reader.py
│   ├── gps_validator.py
│   ├── event_detector.py
│   ├── geofence.py
│   ├── overspeed.py
│   ├── idling.py
│   ├── night_drive.py
│   ├── gps_lost.py
│   ├── cost_calculator.py
│   ├── driver_score.py
│   ├── report_generator.py
│   └── ...
│
├── tests/
│   ├── test_geofence.py
│   ├── test_overspeed.py
│   ├── test_idling.py
│   ├── test_gps_l