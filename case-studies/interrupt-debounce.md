# ESP32 Interrupt & Debounce — Noise vs Logical Events

**SUT:** standalone Wokwi interrupt/debounce demonstration; not the IoT node.

## Risk and test objective
One physical press should generate one accepted logical event. Contact bounce may cause several RAW transitions but should not duplicate actions. Short noise and noise during a critical operation must not trigger an action.

## Test execution / evidence
Normal press, visual RAW D0 vs LOGICAL D1 trace, long press (2–5 s), five rapid valid presses, short noise pulse, noise during critical operation, reproducibility check.

- Normal/bouncing/hold/rapid presses behaved as expected.
- Short noise pulse produced **RAW=2, LOGICAL=1, ACTION=1** despite no valid press.
- Reproduced short noise defect **5/5**.
- Noise during critical operation increased logical events/actions from 1 to 2 before operation finished.

**Recorded summary:** 7/7 mandatory scenarios executed; 4 PASS, 2 FAIL, plus reproducibility check. The two noise scenarios were reported as **one confirmed defect**, not two independent bugs.

## Conclusion
Debounce generally filtered valid physical contact bounce, but did not adequately reject injected noise. This risks unintended logical actions.

[Original report and VCD findings](https://docs.google.com/document/d/1MCIdlbveIsD0F-fhKlCAuPbpfpC5ets7KCEth7hxwQ8/edit) · [Portfolio home](../README.md)

**Limit:** Simulated digital event inputs; no physical-switch EMC/noise characterization.
