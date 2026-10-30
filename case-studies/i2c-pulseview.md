# I²C Protocol Analysis — PulseView / Wokwi

**Scope:** a separate ESP32 I²C course practice, **not** the featured IoT MQTT node. Evidence consists of Wokwi-generated SDA/SCL waveform screenshots opened in PulseView and a decoded transaction.

## What was tested

- Configure decoder: SCL channel = `SCL`, SDA channel = `SDA`.
- Interpret START / repeated START / STOP, addressing, direction (R/W) and ACK/NACK.
- Compare raw waveform and I²C protocol-decode overlays.
- Examine fault-injection cases involving peripheral availability, without assuming the meaning of any single NACK.

## Verified decoded transaction from the provided screenshot

```text
START
Address write: 0xD0  ACK
Data write:    0x41  ACK
REPEATED START
Address read:  0xD1  ACK
Data read:     0xEF  ACK
Data read:     0x5C  NACK
STOP
```

The display was configured in **shifted** address mode, so `0xD0` and `0xD1` are the address bytes including the R/W bit; their 7-bit slave address is **0x68**.

**Critical interpretation:** a **master NACK after the final read byte, followed by STOP**, is a **normal and expected I²C termination pattern**. It is **not by itself evidence of a faulty sensor or peripheral**. A NACK during address acknowledgment or a failed subsequent transaction must be analyzed in its context, with the expected device behavior and surrounding trace.

## Evidence already collected

- PulseView screenshots showing SDA/SCL and an I²C decoder overlay.
- Screenshots of decoded write/read messages and a terminal NACK.
- Raw waveforms at different scales; some screens show idle SCL/SDA and are not stand-alone defect evidence.
- Separate annotated ACK/NACK screenshots from course debugging.

The **original binary screenshots are present in the conversation attachments** but have **not yet been committed as PNG assets into this GitHub repository**. The original `wokwi.vcd` or PulseView `.sr` is not verified as available.

## Evidence judgment

| Evidence | Use | Limit |
|---|---|---|
| Decoded transaction | Best primary illustration of I²C decoding skill | Ending NACK is normal; no bug by itself |
| Raw waveform | Signal transition timing/context | Cannot infer byte fields without decoding |
| Annotated fault/NACK | Fault-injection illustration if paired with expected/actual | Must verify which NACK, exact trigger and timing |
| Decoder settings screenshot | Setup/procedure | Not proof of protocol correctness |
| Empty/idle screenshots | Supplementary context only | Not useful as a headline finding |

## What would strengthen this case

Upload the original `wokwi.vcd` / `.sr` if found, a decoded normal trace, a fault trace with step-by-step expected/actual, and the corresponding UART/status log. Test conclusions should remain scoped to simulation.

[Portfolio home](../README.md) · [Evidence index](../evidence/README.md)
