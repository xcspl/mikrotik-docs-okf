---
type: Reference
title: "Grounding"
description: "Grounding requirements for MikroTik RouterOS devices emphasize proper installation of shielded cables, lightning arresters, and reliable grounding infrastructure using 2.5-4 mm² Cu wire with corrosion-resistant"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, hardware]
resource: https://manual.mikrotik.com/docs/hardware/grounding.md
sources:
  - resource: https://manual.mikrotik.com/docs/hardware/grounding.md
---

# Grounding

## Introduction

Shielded cable installation infrastructure (towers and masts), as well as antennas and the router itself, must be properly grounded. Lightning arresters must be installed on all external antenna cables (near the antennas or on the antennas themselves) to prevent equipment damage and human injury. Note that lightning arresters will not be effective if they are not properly grounded.

Use 2.5-4 mm² Cu (AWG 11–13) wire with corrosion-resistant connectors for grounding. Ensure that the grounding infrastructure you use is fully functional (not merely decorative, as seen in some installations):

1. For shielded connectors, please use shielded cables as they provide better immunity.
2. The grounding wire should be connected to the RouterBOARD grounding wire attachment point if such is provided. This wire should then be connected to the base of the tower, ensuring the connection meets grounding standards. The antenna's grounding wire should be connected near the RouterBOARD outdoor case and can be joined with the same grounding wire used for the RouterBOARD.

## Shielded RJ45 Port vs Unshielded RJ45 Port

### Device with Shielded Ports

![shielded.png](https://manual.mikrotik.com/docs/hardware/img/grounding-01.webp)
![](https://manual.mikrotik.com/docs/hardware/img/grounding-diagram.png)

### Device with Unshielded Ports

![unshielded.png](https://manual.mikrotik.com/docs/hardware/img/grounding-02.webp)

### PoE injector with shielded connectors

![poeinjector.png](https://manual.mikrotik.com/docs/hardware/img/grounding-03.webp)

## RouterBOARD grounding wire attachment points

![](https://manual.mikrotik.com/docs/hardware/img/grounding-04.webp)

![screw1.png](https://manual.mikrotik.com/docs/hardware/img/grounding-05.webp)

![screw2.png](https://manual.mikrotik.com/docs/hardware/img/grounding-06.webp)

:::info
You should not use Power Sourcing Equipment (PSE) with the positive terminal connected to Protective Earth (PE) if it power a MikroTik device. It may cause a short circuit, harm you and your device.

:::
