# STM32-Based HAFC Control Code

This repository provides the embedded implementation of the Hierarchical Attitude–Force Control (HAFC) method on an STM32 platform. The method is developed for a self-levelling four-tracked chassis operating on asymmetric discrete terrain in hilly orchards, with the aim of coordinating chassis attitude levelling and track–ground contact preservation.

**Related paper:**

**Attitude–Force Control for Preserving Track–Ground Contact of a Self-Levelling Tracked Chassis for Hilly Orchard Operations**

## 1. Method Overview

Conventional attitude-feedback-based levelling methods can effectively regulate chassis roll and pitch angles, but continuous contact between all four tracks and the ground cannot always be guaranteed under non-coplanar support conditions.

To address this limitation, track-level ground reaction force (GRF) feedback is introduced into the kinematic attitude levelling (KAL) framework to establish the proposed HAFC method.

Local support abnormalities are identified using GRF residuals together with chassis attitude information, and the tracks requiring corrective action are determined through a predefined force–attitude–terrain mapping. When the event-triggering conditions are satisfied, the corresponding tracks are taken over by the force control layer, while the remaining tracks continue to follow the attitude-levelling commands. In this way, chassis attitude regulation and local track–ground contact preservation are coordinated.

## 2. Hardware Platform

The control algorithm is implemented on an STM32 microcontroller for real-time control of a four-tracked chassis equipped with active suspension.

The main inputs include:

- chassis roll and pitch angles;
- displacement measurements from the spring–damper assemblies;
- servo electric-cylinder encoder signals.

The main outputs are the control commands for the four servo-driven electric cylinders.

## 3. Main Functions

The code provided in this repository mainly includes the following functions:

- kinematic attitude levelling;
- GRF residual calculation;
- dead-zone-based state classification;
- persistence-time confirmation;
- force–attitude–terrain identification;
- selection of tracks requiring corrective actuation;
- track-level force control;
- switching between the attitude and force control layers;
- generation of servo actuator commands.

## 4. Code Structure

```text
HAFC-STM32/
├── README.md
│   ├── Inc/
│   │   └── HAFC-related header files
│   │
│   └── Src/
│       └── HAFC-related source files
```

The actual file structure may vary depending on the organisation of the STM32 project.

## 5. Control Framework

HAFC consists of an attitude control layer and a force control layer.

### 5.1 Attitude Control Layer

The attitude control layer employs the KAL method. Levelling commands for the four suspension channels are generated according to the chassis roll and pitch deviations to continuously regulate the overall chassis attitude.

### 5.2 Force Control Layer

Track-level GRF residuals are used as feedback variables in the force control layer and are combined with chassis attitude states to identify local support abnormalities.

Once a predefined terrain disturbance is identified, force control is selectively applied to the corresponding track to reduce local under-loading and preserve track–ground contact.

### 5.3 Control-Layer Switching

The attitude and force control layers are switched independently for each track according to the corresponding switching state.

Tracks identified as requiring contact correction are regulated by the force control layer, while the remaining tracks continue to follow the attitude-levelling commands.

## 6. Usage Notes

This repository mainly provides the core STM32 implementation of the HAFC method described in the corresponding paper.

Some hardware-specific low-level components may not be included in the public version, including:

- MCU peripheral initialisation;
- low-level RS485 / Modbus communication drivers;
- low-level IMU drivers;
- communication interfaces for specific servo electric-cylinder models;
- hardware configuration files specific to the experimental platform.

Therefore, this repository is primarily intended to demonstrate and reproduce the core control logic of HAFC rather than to provide a complete plug-and-play hardware project.

## 7. Code Version

The code in this repository may continue to be updated during the manuscript review process and subsequent research.

After publication of the paper, a stable Release corresponding to the final published version will be provided to enable version tracking of the control code used in the study.

## 8. Citation

If this code is helpful for your research, please cite the corresponding article after publication.
