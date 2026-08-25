# DigitalTwin.ai --- Predictive Digital Twin for Vehicle Assembly Lines

## Overview

**DigitalTwin.ai** is a predictive digital-twin concept for vehicle
assembly lines designed to detect bottlenecks and process drift early,
predict defect risk, and enable targeted intervention before problems
spread across the line.

The solution addresses three core challenges:

-   Bottlenecks are discovered too late, causing upstream queues and
    downstream starvation.
-   Early-stage process defects can spread across multiple vehicles
    before final inspection detects them.
-   Approximately **35% of stations may be unmonitored**, including
    manual stations and legacy machines where sensor retrofitting is
    difficult.

## Problem Statement

A vehicle assembly line consists of interdependent stations such as
welding, painting, engine fitment, door fitment, and final inspection. A
small slowdown at one station can create queues upstream while starving
downstream stations.

Similarly, a drifting process parameter---such as torque---may not be
detected until final inspection. By then, many vehicles may have passed
through the affected station, creating costly rework or broad
quarantine.

The core gap is:

**Reactive monitoring → Late detection → Lost throughput + broad
quarantine**

## Solution

DigitalTwin.ai creates a unified view of vehicle identity, station
activity, process parameters, queues, and quality outcomes.

The digital twin combines:

-   **VIN / barcode data** --- vehicle identity and timestamps
-   **PLC / machine data** --- machine states and cycle events
-   **Process sensors** --- torque, temperature, pressure
-   **Quality records** --- inspection results and outcomes
-   **Station events** --- entry, exit, and waiting times
-   **Edge vision signals** --- station-level pose/activity information
    where available

The system focuses on predicting process problems rather than simply
alerting after they occur.

## Digital Twin Engine

The twin models:

-   Station sequences
-   Cycle and wait times
-   Queue dynamics
-   Key process parameters
-   VIN-level history across stations

The approach deliberately avoids requiring full 3D physics simulation or
detailed machine-level modeling.

## Prediction Layers

### 1. Drift Detection --- MVP

The MVP monitors process parameters for gradual drift.

**Example:**

`50 → 49.5 → 49 Nm`

The system can identify a developing torque-limit breach approximately
**2 hours early** in the example presented.

### 2. Change-Point Detection

A change-point check confirms whether an observed shift represents a
meaningful process change before generating an alert, helping reduce
false alarms.

### 3. Per-VIN Defect Risk Prediction

The system follows an individual vehicle across stations rather than
analyzing stations in isolation.

**Example:**

`VIN 4471 → Station 8 → Station 15 → Station 22`

Cross-station signals can also be combined. For example, low torque at
one station combined with thick sealant at another can increase the
predicted risk of a downstream rattle defect.

## Blind-Station Observability

DigitalTwin.ai is designed to remain useful even when a station has no
direct sensor data.

Missing signals can be estimated using:

-   VIN timestamps
-   PLC states
-   Queue position

These values are explicitly treated as **estimates with confidence
ranges**, rather than direct measurements.

Predictions start conservatively and become sharper as labeled outcomes
accumulate.

## Bottleneck Detection & Prescriptive Control

The solution extends from visibility to predictive intervention:

1.  **Detect** station activity and buffer dynamics.
2.  **Identify** variance bottlenecks and pacing-pressure risk.
3.  **Forecast** a potential stall and recovery window.
4.  **Escalate** based on severity.
5.  **Verify** high-risk vehicles through targeted end-of-line checks.

The concept uses signals such as:

-   Buffer swings to identify the true constraint
-   **\>85% takt load** as a pacing-pressure risk indicator
-   VIN/gate timestamps
-   Smart-tool telemetry
-   Edge-vision station activity

Global line stops are filtered using pause timers to avoid incorrectly
interpreting planned stoppages as bottlenecks.

## Example Alert

Instead of producing multiple disconnected alerts, the system
prioritizes actionable alerts such as:

> **Vehicle 4471 --- High defect risk. Inspect before final assembly.**

Or:

> **Station 8 --- Torque breach predicted at 3:05 PM. Recalibrate during
> the 1:00 PM break.**

## Expected Operational Impact

The concept targets:

-   Earlier bottleneck detection
-   Reduced unplanned downtime
-   More targeted quarantine
-   Fewer false alarms
-   Earlier defect intervention
-   Better visibility into previously unmonitored stations

The presentation highlights a potential reduction from **200 suspect
VINs to 12 quarantined VINs** when the system can isolate affected
vehicles with supporting evidence.

The referenced downtime exposure is **\$2.3M per hour**, highlighting
the potential value of preventing or shortening major line disruptions.

## MVP Scope

The proposed MVP focuses on:

**Drift Detection → Change-Point Confirmation → Early Process
Prediction**

The complete solution extends this into:

**Per-VIN Defect Prediction → Cross-Station Risk → Predictive Bottleneck
Detection → Prescriptive Control**

## Why DigitalTwin.ai?

### No Retrofit

Uses existing operational signals and is designed to work without
requiring PLC retrofits.

### Fewer False Alarms

Change-point confirmation and contextual signals help distinguish
meaningful process shifts from normal variation.

### Predictive Control

Moves beyond reactive alerts by forecasting bottlenecks and defect risks
early enough to support intervention.

## Team

**Team CORTEX --- IIT Kanpur**

-   Muskan Kumari --- Team Leader
-   Kartik Raj
-   Shivanee Shrivas

**Competition:** Accenture Innovation Challenge 2026

**Problem Statement:** DigitalTwin.ai / Vehicle Assembly Line

## Solution Walkthrough

A 3-minute solution walkthrough, **DARKLINE**, is included with the
project submission.

The presentation provides a Google Drive link to the walkthrough video.

## Source

This README is based on the **Cortex --- IIT Kanpur** presentation
submitted for the Accenture Innovation Challenge 2026.
