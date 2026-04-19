# SLAM Rescue Robot Chassis

**Student:** G Hariharan (25BME0093)  
**Course:** Basic Multidisciplinary Project (2025–2026)  
**Guide:** Mr. Ramesh P. S

This repository contains the CAD and finite element analysis (FEA) of a 4‑wheel mobile robot chassis intended as a low‑cost platform for SLAM‑equipped search‑and‑rescue experiments.

## CAD Overview

- Modelled in Autodesk Fusion 360.
- Closed-shell chassis with:
  - Lower deck for BO motors, batteries and power electronics.
  - Upper deck for ESP32, small breadboard and sensors.
  - Side cut-outs for wheel shafts and front cut-outs for three ultrasonic sensors.
- Material assumed: ABS plastic (3D‑printed prototype / generic ABS sheet).

![Chassis](images/chassis_iso.png)

## FEA Setup

All simulations used Fusion 360 Static Stress analysis:

- Material: ABS plastic  
  - \(E = 2240\) MPa, \(\nu = 0.38\), yield strength ≈ 20 MPa.  
- Mesh: second‑order tetrahedral solids (~46k nodes, ~23k elements).  
- Supports: four motor‑mount regions fixed (Ux = Uy = Uz = 0).  
- Two load cases:
  1. **Uniform top load:** total 10 N distributed on the upper deck (self‑weight + payload).  
  2. **Corner load:** 30 N applied at a front corner, acting diagonally downward.

## FEA Results (summary)

| Load case         | Max von Mises (MPa) | Max displacement (mm) | Min safety factor* |
|-------------------|--------------------:|----------------------:|--------------------:|
| Top load (10 N)   | 0.121               | 0.013                 | 165.7               |
| Corner load (30 N)| 0.369               | 0.009                 | 54.2                |

\*Safety factor based on 20 MPa ABS yield strength.

Interpretation:

- Both load cases keep stress far below ABS yield; the design is highly conservative.
- Corner loading governs the design (highest local stress near the impacted corner and motor mounts).
- Deflections (< 0.02 mm) are negligible for sensor alignment and ground clearance.

## Files

- `cad/`: Fusion/STEP models of the chassis.  
- `fea_reports/`: Raw Fusion 360 FEA reports (top load and corner load).  
- `docs/SLAM_Rescue_Robot_Chassis_Report.*`: Project report with methodology, assumptions, and discussion.  
- `images/`: Chassis renders and FEA contour plots.

## Future Work

- FEA‑guided lightweighting / topology optimisation of low‑stress regions.
- Dynamic and fatigue analysis for repeated impacts.
- Experimental validation with a printed prototype.
