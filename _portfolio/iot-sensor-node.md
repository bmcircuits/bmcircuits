---
title: IoT Environmental Sensor Node
category: PCB Design
date: 2024-06-01
tech: STM32L4 · LoRa · 4-layer
specs:
  - label: MCU
    value: STM32L476RG
  - label: Layers
    value: 4-layer
  - label: Dimensions
    value: 50 × 40mm
  - label: Year
    value: "2024"
  - label: Radio
    value: LoRa SX1276
  - label: Standby current
    value: 8µA
---

A compact wireless environmental sensor node designed for long battery life in remote monitoring applications.

## Overview

The board features the BME688 environmental sensor array, capturing temperature, humidity, barometric pressure, and VOC index. Data is transmitted over LoRa radio (SX1276) to a gateway up to several kilometres away, enabling deployment without Wi-Fi or cellular infrastructure.

## Design highlights

Power was the central design challenge. The STM32L476 runs in Stop 2 mode between measurements, with the sensor and radio powered down via load switches. The LiPo charge circuit (MCP73831) and a 3.3V LDO with very low quiescent current round out the power tree.

A 1000mAh LiPo cell achieves over six months of battery life at a ten-minute reporting interval — validated against a current profile measured on the bench with a Nordic PPK2.

## Firmware

Bare-metal C on the STM32L4, no RTOS. Interrupt-driven I²C for the BME688, SPI for the SX1276 LoRaWAN stack. A custom low-power sequencer manages wake, measure, transmit, and sleep phases. OTA firmware update is supported via the LoRaWAN Class A protocol.
