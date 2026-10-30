# Smart Gate Controller — State Machine & Safety Testing

**SUT:** separate educational Wokwi controller. **Method:** black-box GPIO/limit-switch tests.

## Problem / risk
A controller that fails to honor physical limits or timeout may keep a relay energized and allow unexpected movement. Test focus: safe state transitions, relays and error conditions.

## Test design
24 scenarios covering CLOSED/OPENING/OPEN/CLOSING/STOPPED/ERROR, limit switches, interrupted commands and timeout behavior. Observe status, relay and LED states rather than trusting command acknowledgment.

## Results
**24 cases: 20 PASS, 3 FAIL, 1 BLOCKED.** The OPEN state could not be reached normally in a later dependent scenario, hence BLOCKED rather than FAIL.

| Finding | Expected | Observed |
|---|---|---|
| LIMIT_OPEN failure | OPENING→OPEN, OPEN relay OFF | Remained OPENING, relay ON; reproduced 3/3 |
| OPENING timeout | ERROR, relays OFF after threshold | Stayed OPENING after >30 s, relay ON; reproduced 3/3 |
| Both limits active | Controlled ERROR | Warning without ERROR transition; reproduced 3/3 |

## Evidence, decision, limitations
[Full Smart Gate Test Sheet & Bug Reports](https://docs.google.com/document/d/1IrJTdb2rrrvoSeZq159T8Tr7AOMy53QUqzHHVdlLJjk/edit).

**QA conclusion:** NO-GO against safety-related requirements in this simulated build. No motor-force or electrical measurement on physical hardware; status/relay logic only. This is a **different device** from the IoT environmental node.

**Skills demonstrated:** black-box state-machine design, BVA/negative safety tests, explicit blocked classification, reproducibility.

[Portfolio home](../README.md)
