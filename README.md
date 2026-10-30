# Embedded QA & IoT Firmware Testing Portfolio

**Risk-based validation · Firmware reliability · UART / GPIO / MQTT-style telemetry · Python / Pytest**

I am a QA engineer with a background in functional and test automation, building practical skills in **Embedded QA / firmware validation** through a series of ESP32 simulation exercises. This portfolio documents the problem, test strategy, execution evidence, findings, and quality decisions — not just the tools used.

> **Transparency:** These are **educational projects and Wokwi simulations**, not production hardware tests. Some firmware builds deliberately contain defects. Failures are part of the learning objective; I report only what was observed.

## Featured case study: ESP32 IoT Environmental Monitoring Node

**Question:** Can a telemetry node tolerate a network outage while preserving buffered data, avoiding duplicate publication, and staying stable over time?

[**Read the complete IoT QA Case Study →**](case-studies/iot-environmental-node/README.md)

| Test focus | Evidence | Finding |
|---|---|---|
| Network reconnect | Reported retry backoff dropped from 500 ms to 50 ms | Reconnect storm risk |
| Offline buffer | 5 messages queued while network was down | Queue function passed |
| Buffer limit | Capacity 8; observed 9/8 and 12/8, dropped=0 | Overflow policy failed |
| Telemetry integrity | 5 unique IDs produced 10 publish events | Duplicate publish |
| Memory stability | Heap declined 40,004 B over 500 messages | Progressive degradation |
| Recovery | NET UP restored CONNECTED | Connection recovered; delivery not correct |

**QA release recommendation:** **NO-GO** for this training firmware against its R1–R8 requirements. The connection recovered but telemetry/data-integrity and memory/retry reliability did not satisfy the specified behavior.

## Test strategy

- [**Master Test Plan**](master-test-plan.md) — system and test boundaries, quality risks, test levels, environment, entry/exit gates, regression strategy and evidence rules.
- [Quality risks and risk-based test matrix](case-studies/iot-environmental-node/quality-risks.md) · [Test Matrix](case-studies/iot-environmental-node/test-matrix.md)
- [Evidence index and sources](evidence/README.md)

## Case studies

| Project | QA focus | Evidence / outcome |
|---|---|---|
| [IoT Network Testing](case-studies/iot-environmental-node/README.md) | States, backoff, buffer, duplicates, memory | 4 significant simulated findings; NO-GO |
| [Smart Gate Controller](case-studies/smart-gate.md) | GPIO, state-machine, safe stop, limits | 24 cases: 20 PASS, 3 FAIL, 1 BLOCKED |
| [Interrupt & Debounce](case-studies/interrupt-debounce.md) | ISR, bounce, Logic Analyzer, noise | Short noise incorrectly accepted; reproduced 5/5 |
| [Watchdog / Sleep / NVS](case-studies/watchdog-recovery.md) | Fault injection, safe state, persistence | Unsafe relay restore after WDT; timing limitations documented |
| [UART / Python Automation](case-studies/python-automation.md) | PySerial, JSON, Pytest, BVA, negative tests | 19 tests: 15 PASS, 4 FAIL; five custom scenarios passed |

These are **separate systems under test**; their pass/fail results must not be pooled as one product.

## How I approach embedded QA

1. **Problem & requirements:** identify observable device behavior and explicit constraints.
2. **Quality risks:** prioritize unsafe outputs, data corruption, missed recovery and instability.
3. **Test design:** state transitions, boundary/negative tests, fault injection and stress.
4. **Execution:** Wokwi, UART serial commands, logic traces and Python automation.
5. **Evidence:** preserve exact command sequences, device responses, counters and limitations.
6. **Triage:** distinguish test-oracle, environment, communication, requirement and firmware issues.
7. **Decision:** trace failures back to product risks and recommend GO / NO-GO with rationale.

## Tools and techniques used

| Area | Experience represented here |
|---|---|
| Microcontroller simulation | ESP32, Wokwi, PlatformIO |
| Protocol / diagnostics | UART CLI, JSON responses, MQTT-style educational protocol |
| Signal validation | Logic Analyzer / RAW vs logical GPIO trace, debounce |
| Automation | Python, Pytest, PySerial, parametrization, fixtures |
| Resilience | Watchdog, Deep Sleep, interrupted-save scenarios, recovery |
| Test management | Requirement traceability, risk matrix, Test Plan, Bug Reports |

I²C/SPI analysis was studied during the course, but this repository does not claim unverified captured hardware traces.

## Source code and original evidence

- [Python automation repository](https://github.com/nyarlathotep1/embedded-qa-python-automation) — includes five custom test cases and a separate copy of the IoT case study.
- [Evidence index](evidence/README.md) — links to the full Google Docs reports and notes on their limitations.
- [Professional positioning / skills](career/README.md)

**No course firmware has been copied into this portfolio.** It focuses on my QA reasoning, documented observations and test artifacts. All external report links are provided as references; access permissions should be checked before sharing with interviewers.

---

*This repository is a work-in-progress learning portfolio. Next improvements: timestamped retry evidence, archived raw logs and VCD files, reproducible hardware experiments, and stronger test-fixture isolation.*
