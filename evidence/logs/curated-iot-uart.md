# Curated UART Evidence — IoT Network Training Firmware

All extracts below come from the user's Wokwi Serial Monitor captures on 30 Oct 2026. They are *as-observed* educational simulation output, not real MQTT packet capture. Source logs are not timestamped.

## Reconnect/backoff (R2)

```text
[NET] state=DISCONNECTED
[NET] state=BACKOFF
[NET] retry=1 backoff_ms=500
[NET] retry=2 backoff_ms=50
...
[NET] retry=132 backoff_ms=50
```
A longer session recorded reconnect_attempts=435 before network restoration. Reported backoff is not independently measured elapsed time.

## Offline buffer and recovery: 5 messages (R3/R5/R6)

```text
[BUFFER] queued id=1 count=1/8
[BUFFER] queued id=2 count=2/8
[BUFFER] queued id=3 count=3/8
[BUFFER] queued id=4 count=4/8
[BUFFER] queued id=5 count=5/8
[BUFFER] count=5 capacity=8 dropped=0
[BUFFER] flush_start count=5
[MQTT] publish id=1 temp=24.5
[MQTT] publish id=1 temp=24.5
...
[BUFFER] flush_end count=0
{"net":"CONNECTED","broker":true,"buffer":0,"capacity":8,"sent":10,"dropped":0,"duplicates":5,"reconnect_attempts":435,"heap":350204}
```
The ellipsis indicates omitted repeated publish rows: IDs 2–5 also appeared twice.

## Buffer boundary (R4)

```text
[BUFFER] queued id=8 count=8/8
[BUFFER] overflow policy=DROP_OLDEST dropped_total=0
[BUFFER] queued id=9 count=9/8
[BUFFER] count=9 capacity=8 dropped=0
[BUFFER] count=12 capacity=8 dropped=0
```
9 and 12 are distinct test workloads. The last two BUFFER counts were not from the same continuous run.

## Stress / free heap (R7)

```text
[STRESS] start count=100 heap=349884
[STRESS] end heap=341884
[STRESS] start count=100 heap=341884
[STRESS] end heap=333884
[STRESS] end heap=317880
[STRESS] start count=100 heap=317880
[STRESS] end heap=309880
{"net":"CONNECTED","broker":true,"buffer":0,"capacity":8,"sent":500,"dropped":0,"duplicates":0,"reconnect_attempts":0,"heap":309880}
```
A later idle STATUS remained at heap=309880. The 300-message intermediate heap value was not retained.

See the [full QA report](https://docs.google.com/document/d/126fvFYXzWC-jdOEz_RiQoUFtV60L0TmRSE6S5HuL3Rg/edit) and [four bug reports](../../case-studies/iot-environmental-node/bug-reports.md).
