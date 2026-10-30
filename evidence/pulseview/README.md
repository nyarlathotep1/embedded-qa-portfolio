# PulseView / I²C Screenshot Evidence

Upload exactly these four PNGs from `pulseview/` inside `embedded_qa_evidence_package.zip`:

| File | Purpose |
| --- | --- |
| `i2c_decoded_transaction.png` | Decoded write/read transaction, including final read NACK. The final master NACK is normal in this context. |
| `i2c_normal_final_ack_annotated.png` | Annotated normal ACK/NACK timing for protocol discussion. |
| `i2c_fault_nack_annotated.png` | Annotated fault-injection trace; compare with expected device response before claiming a defect. |
| `i2c_normal_raw.png` | Supporting unmodified screenshot from the I²C waveform capture. |

**Status:** Screenshots have not yet been uploaded to this GitHub folder. This README establishes the intended location.

These images are from an **educational Wokwi/PulseView I²C practice**, not actual oscilloscope measurements or proof that the separate IoT MQTT node failed.

See [I²C case study](../../case-studies/i2c-pulseview.md) and [Evidence Index](../README.md).
