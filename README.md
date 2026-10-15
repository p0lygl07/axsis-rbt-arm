# P01yg107 Labs: 6-Axis Arm Build Guide

**Base Build Photos and detail will be updated**

**Hyper PETG-CF · MG996R / MG90S · ESP32-S3 + VERA**

Six joints, bottom to top: base yaw → shoulder pitch → elbow → wrist pitch → wrist rotate → gripper. Every joint utilizes the same mechanical architecture — a servo drives a link through its round horn seat, while the far end operates as a free pivot.

### Core Assembly Directives

* **Center before you torque:** Send each servo to 90° before tightening its horn, otherwise you immediately lose half the joint's sweep range.
* **Fit-check first:** Test the fit coupon with a real servo before final-torquing structural joints. Tune clearances as needed for your printer's tolerances.
* **Power & control isolation:** Run servos on a separate 5V 5A+ rail with a common ground. Never pull servo power through the ESP32.

---

## Phase 0: Heat-Set Inserts (PREP)

Seat brass M3 inserts in every pilot hole first. These provide metal threads that can handle repeated torque without stripping out the Hyper PETG-CF walls.

| Hardware Required | Tools |
| --- | --- |
| M3 brass heat-set inserts | Soldering iron (set to ~230°C) |
|  | 900M-T-2C bevel tip |

1. Set the iron to ~230°C and fit the 900M-T-2C bevel tip.
2. Stand the printed part on a flat, heat-safe surface with the pilot hole facing up.
3. Rest an M3 brass insert on the hole, knurled end down.
4. Touch the iron to the insert and press straight down — let the plastic melt and accept it (~3–5 seconds).
5. Stop when the insert is flush with the surface; pull the iron straight up and leave the part to set and cool.
6. Keep every insert perfectly square — a tilted insert will cross-thread and strip when you drive the screw later.

> ⚠ **Target Parts:** `base_mount` (shroud + 4 corners), `shoulder_bracket` upright, both `mg996_bracket` feet (4 each), `gripper_base` (4 corners + 2 finger pivots), `wrist_housing` flange. **Never heat a servo.**

---

## Phase 1: Base Rotation (J1 · YAW)

Build the turntable. The base servo stands shaft-up and spins the entire arm assembly riding on a 608 bearing.

| Hardware Required | Printed Parts |
| --- | --- |
| 1× MG996R Servo & Round Horn | `base_mount` |
| 1× 608ZZ Bearing | `bearing_cap` |
| 4× M4, 2× M3, 4× M2.6 screws | `base_rotor` |

1. Bolt the `base_mount` (plate down) to your bench or a heavy base plate using the 4× M4 corners.
2. Center the base MG996R at 90° (using a servo tester or a quick PWM pulse) before it goes in.
3. Drop the servo into the shroud shaft-UP; feed the lead out through the gap first.
4. Press the 608ZZ bearing into the `bearing_cap`'s top pocket until it seats perfectly flat.
5. Lower the `bearing_cap` over the servo so the inner slots capture the flange tabs; bolt the cap to the shroud (2× M3).
6. Fit a round horn onto the centered servo spline.
7. Set the `base_rotor` down so its spigot passes through the 608 bearing and the underside horn-seat lands flush on the horn.
8. Screw the horn to the rotor (4× M2.6). Spin it by hand — it should be smooth with zero lateral rock.

> ⚠ **Tolerance Check:** If the rotor wobbles, the 608 bearing isn't fully seated in the cap, or the cap isn't pulled down tight against the shroud.

---

## Phase 2: Shoulder (J2 · PITCH)

Stand the shoulder servo on the rotor. This joint bears heavy torque as it swings the entire arm structure up and down.

| Hardware Required | Printed Parts |
| --- | --- |
| 1× MG996R Servo & Round Horn | `shoulder_bracket` |
| 6× M3 screws |  |

1. Orient the `shoulder_bracket` foot-down on the rotor top; line up the 2 holes (±18) with the rotor inserts.
2. Bolt the foot to the rotor using 2× M3 screws.
3. Center a second MG996R at 90°.
4. Seat the servo into the upright wall with the shaft horizontal and the horn facing OUT along the arm axis; bolt it in place (4× M3).
5. Fit a round horn onto the splines.

> ⚠ **Alignment Critical:** You must center the servo at exactly 90° before mounting the bicep in the next step, otherwise the arm will mechanically bottom out and fail to reach its full vertical envelope.

---

## Phase 3: Bicep onto Shoulder (LINK)

Hang the upper-arm link onto the shoulder horn.

| Hardware Required | Printed Parts |
| --- | --- |
| 4× M2.6 screws | `bicep` |
| 1× Horn center screw | `joint_cover` |

1. Identify the `bicep`'s horn-seat end (look for the round counterbore) versus the plain-hole pivot end.
2. With the shoulder servo centered, press the horn-seat end onto the shoulder horn.
3. Check that the open channel faces inboard so the elbow and wrist assemblies can nest alongside it later.
4. Screw the horn to the bicep using 4× M2.6 screws, followed by the horn's main center screw.
5. Cap the exposed shoulder pivot with a `joint_cover`.

> ⚠ **Kinematic Pattern:** The link is driven at the horn-seat end and remains free at the pivot end. This exact mechanical pattern repeats at every joint below.

---

## Phase 4: Elbow (J4 · ELBOW)

The elbow servo acts as the hinge between the bicep and forearm — the two printed arm sections never touch directly.

| Hardware Required | Printed Parts |
| --- | --- |
| 1× MG996R Servo & Round Horn | `mg996_bracket` |
| 4× M3, 4× M2.6 screws | `forearm` |
| 1× Horn center screw | `joint_cover` |

1. Bolt an `mg996_bracket` foot FLAT to the bicep's distal (plain-hole) end using 4× M3 screws.
2. Center the elbow MG996R at 90°; seat it in the bracket upright and bolt it down.
3. Fit a round horn; press the `forearm`'s horn-seat end onto it.
4. Match the forearm channel direction to the bicep so the entire arm stays planar.
5. Secure with 4× M2.6 screws and the center screw, then snap on a `joint_cover`.

> ⚠ **Load Path:** The bicep and forearm are joined exclusively through the servo. The bracket carries the structural load, while the horn carries the rotational motion.

---

## Phase 5: Wrist Pitch (J5 · WRIST)

Add the wrist-pitch joint at the forearm tip; the clevis acts as the yoke it tilts.

| Hardware Required | Printed Parts |
| --- | --- |
| 1× MG996R Servo | 2nd `mg996_bracket` |
| 4× M3 screws | `wrist_clevis` |
| 2× M3 pivot pins |  |

1. Bolt the second `mg996_bracket` to the forearm's distal end (4× M3).
2. Center and seat the wrist-pitch MG996R; bolt it down securely.
3. Seat the `wrist_clevis` with its back plate resting on the joint, ears pointing outward, and pivot holes up.
4. Pin the clevis through both ears using M3 hardware onto the servo output.
5. Dry-fit and swing the clevis manually through its physical range BEFORE applying final torque.

> ⚠ **V1 Note:** This is the tightest tolerance area. Dry-fit the clevis and servo first. The exact horn clocking must be set and verified on the bench, not assumed from the CAD model.

---

## Phase 6: Wrist Rotation (J6 · ROTATE)

A compact MG90S spins the gripper mount around the arm's primary axis.

| Hardware Required | Printed Parts |
| --- | --- |
| 1× MG90S Servo | `wrist_housing` |
| 2× M2 screws | `wrist_cover` |
|  | `joint_cover` |

1. Center the rotate MG90S servo.
2. Drop it into the `wrist_housing` from the top (cavity facing up); feed the lead through the side slot, then bolt the flange (2× M2).
3. Fit the assembled housing onto the wrist-pitch output from the previous phase.
4. Set the `wrist_cover` on top — recess facing down, horn hole facing up — ensuring the output shaft passes through cleanly.
5. Add a `joint_cover` if the horn remains exposed.

> ⚠ **Interface Point:** The MG90S output protruding through the cover becomes the direct mounting face for the gripper assembly in the final mechanical phase.

---

## Phase 7: Gripper (GRIPPER)

Finish the end-effector. A single servo drives both fingers simultaneously through a linkage system.

| Hardware Required | Printed Parts |
| --- | --- |
| 1× MG90S Servo | `gripper_base` |
| 4× M3 screws | 2× `gripper_finger` |
| 2× M3 pivots, 2× drive pins |  |

1. Bolt the `gripper_base` to the wrist-rotate output using the 4× M3 corners, with the servo pocket facing outward.
2. Center and seat the gripper MG90S, securing it with 2× M2 screws.
3. Pin both `gripper_fingers` onto the base pivots (M3, ±20); mirror the pair so the tips meet flush in the center.
4. Link each finger's drive-pin to the servo horn.
5. Set the fingers perfectly symmetric at the wide-open position before locking down the linkage screws.

> ⚠ **Calibration:** One servo drives both fingers. Achieving perfect symmetry at the 'open' position is what guarantees they will close evenly on the center axis.

---

## Phase 8: Electronics & Power (ELECTRONICS)

Wire the brain and the muscle: the ESP32-S3 handles local PWM offloading via I2C, while the VERA Arm Driver runs the heavy kinematics on your PC.

| Hardware Required |
| --- |
| ESP32-S3 (with u.FL external antenna) |
| PCA9685 16-Channel PWM Controller |
| Dedicated 5V 5A+ Power Supply |

1. Mount the ESP32-S3 and the PCA9685 inside the base bay. Route the u.FL antenna cable to a clear exterior spot on the base to avoid signal attenuation from the motors.
2. Wire the PCA9685 to the S3 via I2C (`SDA` / `SCL` + `3V3` + `GND`).
3. Run the 6 servo signal leads down the arm and plug them into the PCA9685 channels.
4. Power the servo rail directly from your 5V 5A+ PSU.
5. Tie all grounds together — the PSU ground, PCA9685 ground, and ESP32-S3 ground must share a common reference line.
6. Flash the S3 with the WiFi command-listener firmware.
7. Boot the VERA Arm Driver on your PC (handling Inverse Kinematics, joint limits, and e-stop routines) to push coordinates to the S3 over the network.

> ⚠ **System Architecture Rule:** Never run servo power through the ESP32's onboard regulator. The LLM proposes, the driver validates — strictly no raw PWM is generated directly from the model.
