<!--portfolio
title: Spring Water-Level Logger
dek: A low-cost, offline water-level logger for Himalayan spring monitoring that increases readings from 4 per month to at least 4 per day.
status: Completed
date: 2026-10-17
topics: Water Resources, Environmental Monitoring, Embedded Systems
type: Project
feature: false
image: 
-->

# Spring Water-Level Logger

A low-cost, battery-powered water-level logger for remote Himalayan spring chambers. It is designed for Key Resource Persons, hydrologists, and water-resource managers who currently measure spring behaviour manually during limited field visits. The MVP aims to install one working device at an agreed spring site within 30 days, increasing recording frequency from 4 readings per month to at least 4 readings per day a 30-fold increase.

## Problem and customer evidence

Himalayan springs supply fresh water to roughly one in seven people in India. Spring discharge, usually measured in litres per minute, is a key indicator of spring health, but climate change and human interventions are reducing discharge, making some springs seasonal and drying others completely.

Today, field personnel measure spring behaviour manually using a stopwatch, a one-litre container, and a measuring scale. The process is slow, operator-dependent, and only produces coarse, low-frequency data during field visits. Weather, access constraints, and staffing gaps create missing data, limiting the reliability of spring-health assessments and recharge planning.

The primary user is the Key Resource Person (KRP) of the Water User Community. They need to retrieve reliable records with minimal training, without disrupting normal community water collection. Hydrologists need time-stamped measurements with clear units, a stable reference point, and visible data-quality flags. Installers need a documented procedure to install, check, calibrate, and service the device.

## Requirements

| ID | Requirement | Pass/fail limit | Status |
|---|---|---|---|
| R-01 | Record water level automatically at a configurable interval | At least 4 scheduled readings per day; all 28 readings retained during a 7-day controlled run | ❎ |
| R-02 | Measure water level relative to a documented, fixed reference point | Proposed: absolute error of 5 mm or less across the agreed range; repeatability reported separately |✔️ |
| R-03 | Operate without mains power | Proposed: at least 90 days between battery-service visits | ✔️ |
| R-04 | Store data locally | At least 3 calendar months at the maximum supported logging rate; at least 372 measurement records at 4 readings/day | ✔️|
| R-05 | Enable offline, contactless archive retrieval | A supported phone downloads a complete CSV without mobile data, site internet, or opening the enclosure; proposed transfer time under 2 minutes | ✔️  |
| R-06 | Preserve records through interruptions | A failed download does not delete source data; a power interruption does not corrupt committed records; logging resumes after restart | ✔️ |
| R-07 | Preserve normal community water access | Users can collect water without obstruction, device handling, or unsafe exposed parts; placement must not contaminate water or alter measurement conditions | ✔️ |
| R-08 | Support practical transport and installation | Total installed mass under 3 kg; one person installs it with basic tools in under 30 minutes, proposed | ✔️ |
| R-09 | Withstand the site environment | Complete assembly tested against site temperature, humidity, splash/rain, condensation, and possible immersion; proposed IP67 or better | ✔️ |
| R-10 | Maintain usable time and calibration records | Timestamps include UTC offset; proposed clock drift of 1 minute or less per month; time, reference, and calibration changes are tracked | ✔️ |
| R-11 | Expose status and handle invalid readings clearly | Device identity, last sample, power status, and storage status are locally visible; sensor failures produce flagged records, never zero substitutions | ✔️ |
| R-12 | Control configuration and archive retention | Routine downloads cannot change settings or delete records; configuration changes are logged; records are not silently discarded within the retention window | ✔️ |
| R-13 | Meet the installed-unit cost ceiling | Itemised cost of 10,000 INR or less per installed unit under the approved cost boundary | ✔️ |

## Key decisions and trade-offs

**Water level rather than discharge.** The MVP records water level in millimetres relative to a fixed reference point, rather than directly estimating discharge in litres per minute. This reduces complexity and avoids making unsupported hydrological claims; discharge conversion requires site-specific measurements and will be performed during post-data analysis. A hydrologist and product owner must confirm whether water-level logging is sufficient for the MVP or whether automatic discharge estimation is essential.

**Four daily readings rather than continuous rapid sampling.** The proposed default schedule is at least four readings per day, approximately six hours apart. This provides substantially more data than the current four monthly readings while keeping power consumption and storage requirements manageable. However, it will not capture the rapid recovery process used in the existing manual discharge test. The hydrologist and field team must decide whether a separate rapid-sampling recovery mode is needed.

**Offline local retrieval rather than cloud connectivity.** The MVP uses local, contactless retrieval from a phone rather than automatic cellular upload, cloud dashboards, or remote alerts. This avoids recurring connectivity and data-service costs and suits remote sites with unreliable mobile coverage. The trade-off is that data reaches a server only after a field worker manually shares the downloaded archive. Automatic mobile-network upload is planned for the next phase.

**90-day battery-service target.** The device must operate without mains power, with solar power treated as optional. The proposed 90-day service interval balances maintenance effort against battery capacity, winter conditions, and the risk of snow blocking solar panels. The engineering lead and field team must confirm the required interval and whether solar is practical at the selected site.

**10,000 INR installed-unit cost ceiling.** The target limits cost to encourage practical deployment, but its boundary is not yet agreed. The project sponsor must decide whether it includes taxes, transport, travel, prototype development, and recurring maintenance, or only installed-unit production cost. If the inclusive definition is adopted, the design may need to remove features or use lower-cost components.

## Tests and measured results

No final measured results are available yet. The following tests are planned before the prototype is considered accepted:

- **7-day logging test:** verify that all 28 scheduled readings are retained with unique record IDs and valid timestamps.
- **Accuracy test:** take ten readings at each of five levels across the agreed range, compare them with an independent reference of known finer accuracy, and report bias, maximum absolute error, and repeatability separately.
- **Storage and recovery test:** load representative records, restart the device, and recover the data without loss or corruption.
- **Power test:** measure energy consumption across sensing, idle operation, storage, and downloads; demonstrate the agreed service interval before labelling runtime as verified rather than projected.
- **Retrieval usability test:** ask three representative users to download the archive offline within 5 minutes of approaching the device, after brief instruction and without help.
- **Interruption tests:** simulate download failure, power loss, connection failure, and restart; verify that previously committed records remain intact.
- **Environmental test:** test the complete assembly, including cable entries, against the recorded site conditions.


## Cost and bill of materials

The target installed-unit cost is 10,000 INR or less. The final bill of materials must include:

- Water-level sensor
- Microcontroller or data logger
- Battery and power-management components
- Optional solar charger and panel
- Enclosure, cable entries, and environmental protection
- Local storage
- Mounting hardware
- Assembly labour and installation materials

The cost boundary remains an open decision. It must be confirmed before purchasing whether the 10,000 INR ceiling covers taxes, transport, travel, prototype development, and recurring maintenance, or only installed-unit production cost.

## Schedule and risks

| Milestone | Target period | Exit criterion |
|---|---|---|
| Site and user research | Days 1–5 | Agreed water-level MVP, operating range, service interval, cost boundary, and test plan |
| Concept selection | Days 6–10 | Feasible sensing, power, and data-access concept selected; key components available; mounting and local-access approach agreed |
| Prototype build | Days 11–17 | Logging, archive retrieval, and fault handling work in bench testing |
| Controlled testing | Days 18–24 | 7-day logging test, usability checks, and interruption tests completed with a hydrologist |
| Field installation | Days 25–30 | Installation check, reference comparison, successful field download, and handover completed |
| Supervised pilot | After deployment | Runtime, record completeness, environmental performance, and maintenance findings documented |

### Top risks

| Risk | Mitigation | Owner |
|---|---|---|
| Temperature, condensation, turbulence, fouling, or mounting movement affects readings | Define operating conditions, log temperature where possible, test across the expected range, and specify cleaning and reference-check procedures | Engineering lead and hydrologist |
| Power is exhausted before the next visit, especially in cold weather or when snow blocks solar panels | Measure consumption, size for worst-case winter conditions, agree a service interval, and provide a power-status check | Engineering lead and field team |
| Cost or procurement delays prevent delivery within 30 days | Review the costed concept before purchasing and explicitly revise scope or schedule when needed | Product owner and project sponsor |

## Compliance and safety

The device must not obstruct community water collection, contaminate the spring water, or expose users to unsafe electrical or mechanical parts. It must be mounted securely to reduce risks from animals, accidental contact, and tampering.

The enclosure, cable entries, and complete assembly must withstand the recorded site environment, including temperature, humidity, rain or splash exposure, condensation, and possible immersion. The proposed environmental target is IP67 or better,

The device must preserve normal community water access and must not alter the measurement conditions at the spring chamber. Data privacy, access controls, and configuration-change logging must be addressed before deployment.

## Stakeholders and communication

| Stakeholder | Role | Key concern |
|---|---|---|
| Key Resource Person, Water User Community | Primary user | Simple retrieval, minimal training, and no disruption to water collection |
| Hydrologist / researcher | Technical reviewer | Measurement accuracy, reference stability, data quality, and valid interpretation |
| Water-resource manager | Data consumer | Comparable records from identified sites for review and planning |
| Installer / maintainer | Field operator | Practical installation, calibration, servicing, and troubleshooting |
| Product owner | Decision owner | Scope, priorities, cost, and delivery |
| Engineering lead | Technical decision owner | Sensing, power, enclosure, data storage, and retrieval design |
| Project sponsor | Approver | Budget, site approval, acceptance results, and deployment |
| Community representative | Site stakeholder | Access, safety, water quality, and local suitability |

Key disagreements to resolve before design freeze include whether water-level logging is sufficient, whether four daily readings are adequate.

## Failures and lessons

| Failures | Measure | Reason | Workaround |
|-|-|-|-|
| Battery capacity issue |Proposed Battery life 90 days <br> Achieved Battery life 72 days  |The 2,200 mAh battery currently supports logging for only 2 days at a 10-minute interval | *Long Term* : Replace the high-power ESP32 with an nRF52-series low-power microcontroller <br> *Short term* : Increasing the battery capacity |

No other build or field failures have been recorded yet. The major challenge was enabling wireless data transfer for the field person without rapidly draining the battery. If a high-energy wireless system such as Wi-Fi remained active all day, the device would run out of battery within 2–3 hours.

Introducing a Wi-Fi trigger activated through a BLE prompt addressed this issue. BLE keeps the device in a low-power state while waiting for the field worker, and Wi-Fi is enabled only when data collection is required. This approach supports data retrieval while preserving battery life.

## Build and reproduce

The final build and reproduction instructions. They are expected to cover:

1. Confirm the approved spring site, chamber geometry, reference point, operating range, and mounting location.
2. Assemble the sensor, controller, power system, enclosure, storage, and mounting hardware according to the final bill of materials.
3. Install the device without obstructing community access or altering measurement conditions.
4. Define and document the fixed water-level reference point.
5. Set the device clock, including UTC offset, and record the initial calibration and configuration version.
6. Configure the logging interval and verify that scheduled readings are being recorded.
7. Connect a supported phone to the device’s local network, open the device address, review status, and download the CSV archive.
8. Verify that the exported records match the stored archive and that downloading does not delete source data.
9. Perform routine maintenance, including battery checks, clock synchronisation, reference checks, cleaning, and calibration verification.
