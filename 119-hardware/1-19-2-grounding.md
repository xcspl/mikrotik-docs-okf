---
type: Reference
title: "Grounding"
description: "Shielded cable installation infrastructure (towers and masts), as well as antennas and the router itself, must be properly grounded. Lightning arresters must be installed on all external antenna cables (near the antennas."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# Grounding

Introduction Shielded RJ45 Port vs Unshielded RJ45 Port PoE injector with shielded connectors: RouterBOARD grounding wire attachment points:

## Introduction

Shielded cable installation infrastructure (towers and masts), as well as antennas and the router itself, must be properly grounded. Lightning arresters must be installed on all external antenna cables (near the antennas or on the antennas themselves) to prevent equipment damage and human injury. Note that lightning arresters will not be effective if they are not properly grounded.

Use 2.5-4 mm² Cu (AWG 12–14) wire with corrosion-resistant connectors for grounding. Ensure that the grounding infrastructure you use is fully functional (not merely decorative, as seen in some installations).

1. For shielded connectors, please use shielded cables as they provide better immunity.
2. The grounding wire should be connected to the RouterBOARD grounding wire attachment point if such is provided. This wire should then be connected to the base of the tower, ensuring the connection meets grounding standards. The antenna's grounding wire should be connected near the RouterBOARD outdoor case and can be joined with the same grounding wire used for the RouterBOARD.
## Shielded RJ45 Port vs Unshielded RJ45 Port

Device with Shielded Ports:

Device with Unshielded Ports:

### with shielded connectors:PoE injector

## RouterBOARD grounding wire attachment points:

You should not use Power Sourcing Equipment (PSE) with the positive terminal connected to Protective Earth (PE) if it powers a MikroTik device. It may cause a short circuit, harm you and your device.
