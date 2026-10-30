# Bug Reports — Cross-Project Index

This directory is a navigation layer. Every finding belongs to its **own SUT**, and the detailed reports remain alongside the case study or original test evidence.

| Project | Finding | Report |
|---|---|---|
| IoT Network Node | Reconnect storm / retry backoff | [BUG-001](../case-studies/iot-environmental-node/bug-reports.md#bug-001--reconnect-storm-after-network-loss) |
| IoT Network Node | Duplicate publish after offline flush | [BUG-002](../case-studies/iot-environmental-node/bug-reports.md#bug-002--duplicate-publishing-during-offline-buffer-flush) |
| IoT Network Node | Capacity 8 / DROP_OLDEST violation | [BUG-003](../case-studies/iot-environmental-node/bug-reports.md#bug-003--buffer-capacity-8-and-drop_oldest-not-enforced) |
| IoT Network Node | Progressive free heap loss | [BUG-004](../case-studies/iot-environmental-node/bug-reports.md#bug-004--progressive-free-heap-decline-under-telemetry-stress) |
| Smart Gate | LIMIT_OPEN, OPEN timeout, simultaneous limits | [Case study](../case-studies/smart-gate.md) / [full report](https://docs.google.com/document/d/1IrJTdb2rrrvoSeZq159T8Tr7AOMy53QUqzHHVdlLJjk/edit) |
| Interrupt & Debounce | Short noise accepted as valid press | [Case study](../case-studies/interrupt-debounce.md) / [full report](https://docs.google.com/document/d/1MCIdlbveIsD0F-fhKlCAuPbpfpC5ets7KCEth7hxwQ8/edit) |
| Watchdog / Sleep | Unsafe relay restore and recovery behaviors | [Case study](../case-studies/watchdog-recovery.md) / [full report](https://docs.google.com/document/d/15COrL-vUTrdvnlFhEyEcGxBkvmDZotUFSGCyLE40-kg/edit) |
| UART/Pytest | PWM boundary, RESET, JSON, PING | [Case study](../case-studies/python-automation.md) / [full report](https://docs.google.com/document/d/1nAbP0ulq0aC19MI5TuiUNGAtnZK4YVzIr5v7H86u_xE/edit) |

For each issue, assess severity against product impact. Simulation and finite observations do not establish physical-hardware outcomes.

[Portfolio home](../README.md)
