# Star-Delta Starter (Siemens SIMATIC Manager - STL/AWL)

This project contains a simple and practical **Star-Delta motor starter** program written in **STL (AWL)** for **Siemens S7 (SIMATIC Manager / STEP 7 Classic)**.

## Features

- Start/Stop process latch
- Main contactor control
- Star-to-Delta automatic transition
- Star timer = **5 s**
- Transition (dead-time) timer = **300 ms**
- Feedback monitoring for Main/Star/Delta contactors
- Fault alarm latch and manual fault reset

---

## Program Sequence

1. Press **START** (with STOP healthy, overload healthy, no fault)  
   → `PROCESS` is set.
2. `MAIN_CONTACTOR` turns ON.
3. `STAR_CONTACTOR` turns ON for 5 seconds.
4. After star time ends, waits 300 ms transition delay.
5. `DELTA_CONTACTOR` turns ON.
6. If any commanded contactor feedback is missing for 5 seconds  
   → `FAULT_ALARM` is set and process stops.
7. Press `FAULT_ALARM_RESET` to clear alarm after troubleshooting.

---

## Tag List (BOOL)

### Inputs
- `START`
- `STOP`
- `OVERLOAD_RELAY`
- `MAIN_FEEDBACK`
- `STAR_FEEDBACK`
- `DELTA_FEEDBACK`
- `FAULT_ALARM_RESET`

### Outputs
- `MAIN_CONTACTOR`
- `STAR_CONTACTOR`
- `DELTA_CONTACTOR`

### Internal Bits
- `PROCESS`
- `FAULT_ALARM`

### Timers (S5 Timers)
- `T1` = Star duration (`S5T#5S`)
- `T2` = Star→Delta delay (`S5T#300MS`)
- `T3` = Main feedback timeout (`S5T#5S`)
- `T4` = Star feedback timeout (`S5T#5S`)
- `T5` = Delta feedback timeout (`S5T#5S`)

---

## Notes

- Keep **electrical/mechanical interlock** between Star and Delta contactors in hardware.
- Adjust timer values to match motor and site requirements.
- Test in simulation/offline before commissioning on real equipment.

---

## File

- `StarDelta_Final.awl` (STL/AWL logic)

---

## Disclaimer

This example is for learning/reference.  
Commissioning must be done by qualified personnel following local electrical safety standards.
