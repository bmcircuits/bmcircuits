---
title: USB HID DFU Bootloader
category: Firmware
date: 2023-04-01
tech: C · STM32 · USB DFU
specs:
  - label: Target
    value: STM32F4 series
  - label: Interface
    value: USB Full-Speed
  - label: Flash footprint
    value: < 8KB
  - label: Security
    value: ECDSA-P256
  - label: Host tool
    value: dfu-util compatible
  - label: Year
    value: "2023"
---

A compact, secure field-update bootloader that presents as a standard USB DFU device — no proprietary tools or drivers required.

## Motivation

Most STM32 products using ST's internal DFU bootloader require BOOT0 pin manipulation to enter update mode — awkward in a sealed product. This bootloader lives in the first 8KB of user flash and enters update mode via a software flag, a button combination, or automatically on firmware validation failure.

## Security model

Firmware images are signed offline with an ECDSA-P256 private key. The bootloader verifies the signature against a public key stored in a protected flash sector before writing. An invalid signature is rejected without modifying application flash, preventing partial or corrupted updates.

## Dual-bank strategy

The STM32F4 flash is divided into two equal application banks. The bootloader always writes to the inactive bank, then atomically swaps via a bank pointer stored in the last flash page. On next reset, the new firmware is verified before the pointer is committed — if verification fails, the pointer is not updated and the previous version remains active.

## Host compatibility

The bootloader is compatible with `dfu-util` and custom host applications. A reference Python script for signing firmware images and triggering updates is provided as part of the deliverable.
