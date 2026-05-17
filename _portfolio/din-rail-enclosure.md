---
title: Sheet Metal Din-Rail Enclosure
category: CAD / Enclosure
date: 2023-09-01
tech: Sheet Metal · IP20 · Din-rail
specs:
  - label: Material
    value: 1.5mm steel
  - label: Rating
    value: IP20
  - label: Mounting
    value: 35mm Din-rail
  - label: Finish
    value: Powder coat RAL 7035
  - label: Tool
    value: Fusion 360
  - label: Year
    value: "2023"
---

A parametric Din-rail mount enclosure designed for press-brake manufacture, housing a custom industrial controller PCB.

## Design intent

The brief called for a low-cost enclosure manufacturable by a local sheet metal shop without any tooling investment. Press-brake bending from a single blank keeps part count and cost minimal. The design accommodates standard 35mm DIN rail using a snap-fit clip profile bent into the base — no separate clip hardware required.

## PCB retention

A clip-in rail system on the inner walls holds the PCB at the correct height without screws. Two retention clips stamped from the same blank snap into slots in the side walls. The PCB slides in from the front and locks positively — assembly time under 30 seconds.

## Thermal and EMI

Ventilation slots on the lid and rear wall provide natural convection airflow across the controller. An optional EMI mesh insert press-fits into a recess in the lid for applications requiring additional shielding.

The design was validated in Fusion 360 against the PCB outline model before any material was cut, catching two interference issues early that would otherwise have required a metal respin.
