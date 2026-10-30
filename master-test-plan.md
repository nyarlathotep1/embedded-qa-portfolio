# Master Test Plan — Embedded / IoT Training Portfolio

**Version:** 1.0 · **Scope:** simulated course exercises and risk-based evidence · **Decision authority:** QA release recommendation (not production certification).

## 1. Product / system overview
This is a **portfolio-level plan** for separate educational firmware projects: [IoT Environmental Node](case-studies/iot-environmental-node/README.md), [Smart Gate Controller](case-studies/smart-gate.md), [ESP32 Debounce](case-studies/interrupt-debounce.md), [WDT/Recovery](case-studies/watchdog-recovery.md), and [UART/Pytest](case-studies/python-automation.md). These are **not one integrated product**. Their results are never combined into a single product pass rate.

## 2. Goal and test strategy
Validate observable firmware behavior against stated requirements, identify high-impact failures in safety, recovery, protocol/data integrity, and document the basis for accepting or rejecting a simulated build.

**Traceability chain:** requirement → risk → technique/case → observed evidence → finding → QA decision.

## 3. Scope / exclusions
**In scope:** Wokwi ESP32 behavioral tests, GPIO/state logic, interrupt/noise, serial CLI, fault injection, watchdog/sleep, persistence observations, network reconnect/buffering/duplicates, heap trend, Python/Pytest automation.

**Out of scope:** physical board electrical tolerances, real RF/Wi-Fi and broker acknowledgments, production hardware qualification, EMC, RF security, power measurements, extended thermal/battery endurance. I²C/PulseView practices count only where separately evidenced; no unverified traces are uploaded as test results.

## 4. Quality risks and strategy
| Risk | Impact | Priority | Representative evidence |
|---|---|---|---|
| Unsafe output after reset | Safety / actuator unintended state | P1 | Smart Gate relay and watchdog safe-state checks |
| Lost or duplicated telemetry | Data integrity / wrong downstream action | P1 | IoT message IDs and flush |
| Failed or aggressive reconnect | Availability and excessive resource load | P1 | NET DOWN/UP; backoff |
| Bad command validation | Unsafe configuration / malformed protocol | P1 | UART PWM boundary and negative tests |
| Interrupt noise accepted | Unintended action | P1 | RAW vs LOGICAL and noise injection |
| Memory degradation | Progressive malfunction | P1 | Five STRESS 100 batches |
| Poor diagnostics | Slow triage / invalid conclusions | P2 | STATUS, serial logs, test output |

Risk is rated by potential impact and likelihood where evidence is available; precise field probabilities are *not* asserted.

## 5. Test levels & types
| Level/type | Use | Tool |
|---|---|---|
| Component/interface checks | GPIO, debounce RAW/logical, CLI syntax | Wokwi, Serial, Logic Analyzer |
| Integration | Sensor↔firmware response, buffer↔publish, persistence | Wokwi UART logs |
| System black-box | State transitions and user-facing status | Wokwi |
| Fault injection / recovery | Hang/WDT, powerloss, sleep, NET DOWN/UP | Training CLI |
| Non-functional reliability | Backoff, stress/heap, duplicates | UART logs, STATUS |
| Automation/regression | Parameterized boundaries and negative cases | Python / Pytest / PySerial |

Physical hardware is a **future validation level**, not an executed test level in this portfolio.

## 6. Test environment
Windows + VS Code/PlatformIO + Wokwi Simulator, ESP32/DHT22 training builds, UART Serial Monitor, Logic Analyzer/VCD in the debounce exercise, Python 3.14.7 / pytest 9.1.1 / PySerial 3.5 for the Webinar 6 course suite.

**Reproducibility rules:** one serial-port owner, correct firmware build, known preconditions, collect device logs, record raw commands, isolate environment/test failures before filing firmware bugs.

## 7. Entry criteria
- Requirements available with clear oracle and traceable ID.
- Simulated build compiles; target boots; UART CLI and STATUS work.
- Baseline state known and evidence collection available.
- Test steps, negative/boundary conditions, fault-injection recovery planned.
- Limitations and dependencies documented.

## 8. Exit criteria / acceptance
- All P1 scenarios executed or explicitly blocked with impact recorded.
- No unresolved release-blocking safety, persistence, protocol integrity or reliability defects.
- Recovery and safe-state conditions met.
- Actual behavior matches specified boundaries, no duplicate messages per protocol.
- No unexplained progressive heap loss.
- Evidence linked to requirements and conclusions, regression after fixes.
- Known risks documented and accepted by accountable stakeholders.

The IoT Node training firmware received **NO-GO** due to R2, R4, R6 and R7 failures. The Smart Gate and other buggy exercises have separate conclusions in their case studies.

## 9. Regression layers
**Smoke:** boot, STATUS, basic command/control and sensor response.  
**Critical:** safety/actuators, buffer/data integrity, fault recovery, reconnect.  
**Full:** functional + protocol + stress/memory + persistence + regression suites.  
**Automated:** deterministic CLI tests via Pytest, with robust preconditions/teardown to be improved before CI.

## 10. Evidence and reporting
- Expected/actual, test step, firmware/build ID where possible, UART logs, snapshots, traces, Pytest results.
- [IoT evidence](case-studies/iot-environmental-node/evidence.md) and [IoT defect reports](case-studies/iot-environmental-node/bug-reports.md).
- [Other case studies](README.md#case-studies).
- Do **not** classify every FAILED Pytest result as firmware defect: consider test logic → environment → communication → requirement → firmware.

## 11. Assumptions, dependencies, residual risks
Simulated transports and mocked brokers may hide real latency, packet loss, power spikes, hardware bounce, or physical timing. A future hardware plan should include real MQTT capture, Wi-Fi outage/roaming, power cycle/brownout, long soak and resource measurement. Exact retry time in IoT logs was not independently timestamped; actual physical safety of relays was not measured during reset.

## 12. Sign-off
This plan offers an evidence-based **training-build QA recommendation**, not an approval to deploy hardware. A product owner/engineering lead would own a production release decision.

[Back to portfolio](README.md)
