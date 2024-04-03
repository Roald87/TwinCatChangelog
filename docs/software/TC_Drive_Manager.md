# TE5950 TC3 Drive Manager 2

## Version 1.1.76.0

-   AX8000 Axis module firmware 1.02 build 0012, interface revision -0102
-   AX8000 Axis module firmware 1.03 build 0006, interface revision -0103
-   NEW: AX8000/AMP8000 Axis module firmware 1.04 build 0010, interface revision -0104
-   AX8000/AMP8000 Axis module firmware 1.05 build 0012, interface revision -0105
-   AX8000/AMP8000 Axis module firmware 1.06 build 0002, interface revision -0106
-   AX8yxx boot loader version 1.35
-   AX8525 / AX8540 / AX8620 / AX8640 Power supply module firmware 1.05 build 0006, interface revision -0105
-   AX8810 Capacitor module firmware 1.00 build 0022, interface revision -0100
-   AX86xx/AX8810 boot loader version 2.31 build 0000
-   AX883x Coupling module Firmware 2.01 Build 0001, interface revision -0201
-   NEW: AX8600 DC power supply module firmware 1.01 build 0005, interface revision -0101
-   AMP8600/AMP8800 Distributed power supply module / Decentralized distribution module firmware 2.01 build 0006, interface revision -0201
-   AX5000 Servo Drive firmware 2.13 build 0010, interface revision -0213
-   AX5000 Servo Drive firmware 2.14 build 0006, interface revision -0214
-   AX570x Optional encoder card firmware 2.00 build 0009
-   AX572x Optional digital encoder card firmware 3.00 build 0020
-   AX5021 Brake module firmware 1.02 build 0001

## Version 1.1.58.0

Supported devices: AX5000, AX8000, AMI8000, AMP8000, EL72xx, ELM72xx, EL74xx, EL7037, EL7047

## Features

-   AX5000/AX8000: Check and adjust feedback connections when importing settings from different channels
    -Adjustments and optimizations of the parameter description, user interface and usability

## Bug fixes

-   Scan ELM72xx channel B
-   AX80000/AMP8000: Display and configure velocity and acceleration in NC units when modulo is enabled
-   Import an axis from Motion Designer project

# TC drive manager

## Version 2.14.30.0

-   New: TC drive manager, version 2.10.36.0.
-   New: AX5000 servo drive, firmware 2.14 build 0004, interface revision -0214.
-   New: AX5000 servo drive, firmware 2.13 build 0010, interface revision -0213.
-   AX5000 servo drive, firmware 2.06 build 34, interface revision -0203.
-   AX5000 servo drive, firmware 1.06 build 30, interface revision -0011.
-   AX570x optional encoder card, firmware 2.00 build 0009.
-   AX572x optional encoder card, firmware 3.00 build 0019.
-   AX5021 brake module, firmware 1.02 build 0001, interface revision -0002.

## Version 2.10.36

Supported devices: AX5000, EL72xx, EP72xx, EJ72xx.

Changes from version 2.10.32.0 to Version 2.10.36.0.

### Features

-   AX5000: Velocity observer is activated when a feedback other than a resolver is selected. From firmware revision> = 2.10.

# AX5000 servo drive

## Firmware 2.14 build 0004, interface revision -0214

Supported Servo Drive: AX5xxx-xxxx-02xx HW2 (Serial number >= 100 000).

Changes from firmware 2.14 build 0002 to firmware 2.14 build 0004.

### Features

-   Support of HIPERFACE DSL encoders EEx.
-   Support of encoders with HIPERFACE to HIPERFACE DSL converter.
-   Extended diagnosis for position sensors with prime number processing.

### Optimizations

-   Initialization of HIPERFACE encoders.
-   Initialization of EnDat 2.1 RCN5180 / ECE225 encoders.

This firmware already includes the firmware for the encoder option cards. If an encoder card is connected to the drive during the update process, this card is updated automatically.

## Firmware 2.13 build 0010, interface revision -0213

Supported Servo Drive: AX5xxx-xxxx-02xx HW2 (Serial number >= 100 000).

Changes from firmware 2.13 build 0009 to firmware 2.13 build 0010.

### Optimizations

-   Initialization of HIPERFACE encoder.

This firmware already includes the firmware for the encoder option cards. If an encoder card is connected to the drive during the update process, this card is updated automatically.

## Firmware 2.06 build 0034, interface revision -0203

Supported Servo Drive: AX5xxx-xxxx-00xx HW2 (serial number >= 100 000).

Changes from firmware 2.06 build 32 to firmware 2.06 build 34.

### Optimizations

-   MES-position encode and communication offset.

## Firmware 1.06 build 0030, interface revision -0011

Supported Servo Drive: AX5xxx-xxxx-00xx HW1 (serial number < 100 000).

Changes from firmware 1.06 build 18 to firmware 1.06 build 30.

### Optimizations

-   Turn-on behavior when connecting with the AX5801 safety card.

# AX570x optional encoder card

## Firmware 2.00 build 0009

Changes from firmware 2.00 build 0008 to firmware 2.00 build 0009.

### Optimizations

-   Error response.

# AX572x optional encoder card

## Firmware 3.00 build 0019

Changes from firmware 3 build 0014 to firmware 3 build 0019.

### Features

-   Operation of battery-supported encoders with EnDat 2.2 (supported from firmware version 2.13).

### Optimizations

-   Position evaluation for EnDat 2.2 and BiSS C.

# AX5021 brake module

## Firmware 1.02 build 0001, interface revision -0002

No changes.

# AX8000

## Firmware 1.05

### Bug fixes

-   Recording a Bode plot sometimes caused the motor to uncontrollably move with a constant velocity to one end.

## Firmware 1.04

### Features

-   New object 0x32E0:08 (Raw slave line data).
-   Measure internal encoder delay time. The result is shown in object 0x32E2:03.
