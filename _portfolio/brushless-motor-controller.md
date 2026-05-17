---
title: Brushless Motor Controller
category: Embedded Systems
date: 2024-02-01
tech: STM32G4 · CAN FD · FOC
specs:
  - label: MCU
    value: STM32G474
  - label: Bus voltage
    value: 12–48V DC
  - label: Peak current
    value: 20A
  - label: Comms
    value: CAN FD
  - label: Control
    value: FOC / SVPWM
  - label: Year
    value: "2024"
---

A high-performance FOC-based BLDC motor controller designed for robotics and industrial automation applications.

## Overview

Field Oriented Control (FOC) with Space Vector PWM modulation delivers smooth, efficient torque control across the full speed range. Dual inline shunt resistors on phases A and B provide accurate current measurement without the inductance issues of a single DC-link shunt.

## Hardware design

The power stage uses six MOSFET half-bridges driven by a gate driver IC with integrated deadtime control and shoot-through protection. An isolated CAN FD transceiver handles communication with the host controller at up to 5 Mbit/s data phase.

Thermal design was carefully managed: the FETs are placed directly over a 2oz copper pour tied to exposed pads on the bottom layer, which mounts flat against an aluminium heatsink bracket.

## Firmware

FreeRTOS with three core tasks: the FOC inner loop runs at 20kHz from a timer interrupt (outside the RTOS scheduler), a velocity control loop runs at 1kHz, and a CAN communication task handles command parsing and telemetry at lower priority.

A custom CAN protocol supports torque, velocity, and position command modes with configurable ramp rates and configurable limit values stored in flash.
