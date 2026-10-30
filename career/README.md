# Professional Profile — QA / Embedded QA

**Role positioning:** QA Engineer progressing into **Embedded QA / Firmware Validation**.

## Transferable experience

- Manual and automated testing, negative/boundary and API-style validation.
- Structuring expected vs actual results, reproducible test design and defect triage.
- Python / Pytest / PySerial UART automation of a simulated ESP32 CLI.
- Embedded-oriented state-machine, GPIO, interrupt/debounce and recovery exercises.
- Network resilience, telemetry data integrity, buffer boundaries and heap stability in Wokwi.

## What this portfolio demonstrates

I can derive test scenarios from explicit device requirements, identify risk-based priorities, validate observable system behavior, capture evidence, separate environmental/test issues from firmware defects, and provide a QA release recommendation with documented limitations.

## What it does not claim

- Professional production firmware/hardware validation experience solely from these exercises.
- Certified hardware timing, EMC, power or RF tests.
- Real MQTT broker packet-level validation or production Wi-Fi reliability.
- Source-level debugging expertise for bugs that were only observed as black-box findings.

## Interview-ready example

**Risk:** duplicate telemetry after reconnection.  
**Design:** simulate broker outage, queue five telemetry IDs, restore network, count publish logs by ID.  
**Evidence:** five queued IDs but ten publish entries, `duplicates=5`.  
**Decision:** fail R6; product build NO-GO with additional buffer and heap findings.

[Detailed IoT Case Study](../case-studies/iot-environmental-node/README.md) · [Master Test Plan](../master-test-plan.md) · [Portfolio home](../README.md)

*This is a skill-focused public portfolio, not a personal résumé containing private contact information.*
