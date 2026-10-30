# UART / Pytest — Embedded Firmware Test Automation

**SUT:** separate buggy ESP32 CLI training firmware controlled through PySerial RFC2217, not the IoT network node.

## Goal and approach
Automate boundaries and negative input, parse UART JSON, verify both acknowledgment and device state. Classify a test failure before treating it as a firmware defect.

## Recorded execution
**19 collected · 15 passed · 4 failed**, including **5/5 additional custom scenarios passed**.

| Observed failure | Expected | Actual |
|---|---|---|
| `SET PWM 100` | Accepted (0..100 inclusive) | ERROR |
| `RESET` after LED ON | PWM=0 safe state | PWM=255 |
| `GET TEMP` | Valid JSON | Truncated JSON (`{"status":"OK","temperature":24.5`) |
| `PING` | JSON OK | TimeoutError |

## Custom test technique
The five custom cases used two parameterized functions with values `-1, 101, 999, abc, 50.5`. Sequence: valid `SET PWM 50`, capture `STATUS`, invalid `SET PWM value`, check ERROR, then compare `STATUS.pwm` before/after.

This comparison avoids assuming the internal PWM representation equals the CLI percentage. An earlier test failed because it expected status PWM=50, whereas it reported 127 — a **test-oracle mistake**, not proven firmware failure.

## Framework notes
Finite read timeout and JSON parsing were implemented. PySerial `DeprecationWarning` did not indicate test failures. An earlier session yielded widespread communication timeouts until Wokwi was restarted; these were separated from product defects. The fixture attempts RESET at teardown; no verified RESET precondition runs before each case, and cleanup can error when device communication fails.

## Links
- [Automation repository and custom Python tests](https://github.com/nyarlathotep1/embedded-qa-python-automation)
- [Full QA report](https://docs.google.com/document/d/1nAbP0ulq0aC19MI5TuiUNGAtnZK4YVzIr5v7H86u_xE/edit)
- [Portfolio home](../README.md)

**No CI run or physical ESP32 execution is claimed.**
