# Evidence Index & Provenance

This page collects **traceable evidence** across separate educational systems. Reports below contain execution steps, expected/actual behavior and logs. When a full raw file is unavailable in this repository, it is **not** claimed to be attached.

| Artifact | Device / topic | Evidence |
|---|---|---|
| [IoT Network QA Report](https://docs.google.com/document/d/126fvFYXzWC-jdOEz_RiQoUFtV60L0TmRSE6S5HuL3Rg/edit) | Network state, buffering, telemetry duplicates, heap | 4 findings; 500-message stress; state logs |
| [Smart Gate Hardware Test Sheet](https://docs.google.com/document/d/1IrJTdb2rrrvoSeZq159T8Tr7AOMy53QUqzHHVdlLJjk/edit) | State transitions / limits / timeout | 24 executed/blocked cases and linked defects |
| [Interrupt & Debounce Report](https://docs.google.com/document/d/1MCIdlbveIsD0F-fhKlCAuPbpfpC5ets7KCEth7hxwQ8/edit) | RAW / logical GPIO, noise | 5/5 noise failure reproduction and VCD observations |
| [Watchdog / Sleep / NVS Report](https://docs.google.com/document/d/15COrL-vUTrdvnlFhEyEcGxBkvmDZotUFSGCyLE40-kg/edit) | Fault injection, sleep, relay, sensor | WDT/reset logs, source-reviewed caveats |
| [Python / Pytest Test Report](https://docs.google.com/document/d/1nAbP0ulq0aC19MI5TuiUNGAtnZK4YVzIr5v7H86u_xE/edit) | UART CLI and automated regression | 19 tests; 5 additional cases |
| [Executable custom Pytest cases](https://github.com/nyarlathotep1/embedded-qa-python-automation/blob/main/tests/test_firmware_cli.py) | UART CLI negative/state | 5 custom tests in Python |

## Evidence boundaries

- Wokwi output is not physical electrical measurement, real MQTT packet capture or production validation.
- IoT retry rate was **not** measured from reliable timestamps; only reported `backoff_ms` and attempt counters were observed.
- IoT memory 300-message free heap data was not retained; no number is invented.
- The debounce VCD evidence is described in its original report; original VCD is not currently uploaded here.
- Source-review observations in Watchdog/Sleep work are distinguished from black-box behavior.
- Google Docs sharing/access permissions may need to be adjusted manually before external review.

## Evidence to add later

- Raw serial logs with timestamps, test-case IDs, device build/ELF hashes.
- Captured VCD/PulseView traces and annotated screenshots with exact observations.
- Pytest JUnit/HTML reports for a reproducible regression suite.
- Physical ESP32 test evidence separate from simulated runs.

[Portfolio home](../README.md)

## New curated evidence package

A verified evidence ZIP was assembled from the supplied course attachments (3 annotated/decoded PulseView views, 3 Wokwi system screenshots, supporting raw PulseView and nine UART text clips). It remains an **attachment in the ChatGPT conversation**, not a GitHub-hosted binary asset. Upload the ZIP contents into the appropriate GitHub folders before labeling its PNGs as repository evidence. See [I²C protocol-analysis notes](../case-studies/i2c-pulseview.md) and the already hosted [curated UART excerpts](logs/curated-iot-uart.md).
