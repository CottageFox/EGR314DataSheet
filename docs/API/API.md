---
title: API - Motor Subsystem (Bryce)
---

# API – Motor Driver Node (Bryce)

**Owner:** Bryce  
**Node ID:** `B` (ASCII `0x42`)  
**Subsystem:** Motor Driver  
**Language:** MicroPython (ESP32)  
**Protocol:** Team daisy-chain UART, 9600 baud, 64-byte fixed frames

---

## Packet Frame Structure

All messages use a **64-byte fixed-length frame** on the UART daisy chain. The message payload (bytes 4–61) carries an ASCII string command. Unused payload bytes are padded with `0x00`.

| Byte(s) | Field | Type | Value |
|---------|-------|------|-------|
| 0–1 | `prefix` | `char[2]` | `AZ` (always) |
| 2 | `src_id` | `uint8_t` | Sender's ASCII ID (e.g. `B` = `0x42`) |
| 3 | `dst_id` | `uint8_t` | Destination ASCII ID (e.g. `B`, `X`) |
| 4–61 | `message` | `char[58]` | ASCII command string, null-padded |
| 62–63 | `suffix` | `char[2]` | `BY` (always) |

**Example frame (hex):** `41 5A 57 42 46 57 44 00 ... 42 59`  
→ From `W` (Rylee), To `B` (Bryce), Message = `"FWD"`

---

## Team Member Identifiers

| ASCII Char | Hex | Name |
|-----------|-----|------|
| `W` | `0x57` | Rylee |
| `B` | `0x42` | Bryce *(this node)* |
| `F` | `0x46` | Riley |
| `T` | `0x54` | Tim |
| `H` | `0x48` | Hattie |
| `X` | `0x58` | Everyone (Broadcast) |

---

## Messages Received (Direct — `dst = B`)

Messages addressed directly to Bryce (`dst = 'B'`). Upon receiving any valid direct message, this node **automatically sends an `ACK`** back to the sender, then executes the command.

---

### `FWD` — Drive Motor Forward

**From:** Any known team member  
**To:** `B` (Bryce)

Sets the motor driver to run in the **forward** direction.

| Byte(s) | Variable Name | C Type | Min | Max | Example |
|---------|--------------|--------|-----|-----|---------|
| 4 | `cmd[0]` | `char` | `F` (0x46) | `F` (0x46) | `F` |
| 5 | `cmd[1]` | `char` | `W` (0x57) | `W` (0x57) | `W` |
| 6 | `cmd[2]` | `char` | `D` (0x44) | `D` (0x44) | `D` |
| 7–61 | `padding` | `uint8_t` | 0x00 | 0x00 | 0x00 |

> **Action:** Sets `dir_pin = 1`, enables driver (`dis = 0`), asserts `pwm_pin = 1`, turns LED on.  
> **Response:** Sends `ACK` to sender.

---

### `REV` — Drive Motor Reverse

**From:** Any known team member  
**To:** `B` (Bryce)

Sets the motor driver to run in the **reverse** direction.

| Byte(s) | Variable Name | C Type | Min | Max | Example |
|---------|--------------|--------|-----|-----|---------|
| 4 | `cmd[0]` | `char` | `R` (0x52) | `R` (0x52) | `R` |
| 5 | `cmd[1]` | `char` | `E` (0x45) | `E` (0x45) | `E` |
| 6 | `cmd[2]` | `char` | `V` (0x56) | `V` (0x56) | `V` |
| 7–61 | `padding` | `uint8_t` | 0x00 | 0x00 | 0x00 |

> **Action:** Sets `dir_pin = 0`, enables driver (`dis = 0`), asserts `pwm_pin = 1`, turns LED on.  
> **Response:** Sends `ACK` to sender.

---

### `STOP` — Stop Motor

**From:** Any known team member  
**To:** `B` (Bryce)

Halts the motor and disables the driver output.

| Byte(s) | Variable Name | C Type | Min | Max | Example |
|---------|--------------|--------|-----|-----|---------|
| 4 | `cmd[0]` | `char` | `S` (0x53) | `S` (0x53) | `S` |
| 5 | `cmd[1]` | `char` | `T` (0x54) | `T` (0x54) | `T` |
| 6 | `cmd[2]` | `char` | `O` (0x4F) | `O` (0x4F) | `O` |
| 7 | `cmd[3]` | `char` | `P` (0x50) | `P` (0x50) | `P` |
| 8–61 | `padding` | `uint8_t` | 0x00 | 0x00 | 0x00 |

> **Action:** Deasserts `pwm_pin = 0`, disables driver (`dis = 1`), turns LED off.  
> **Response:** Sends `ACK` to sender.

---

## Messages Received (Broadcast — `dst = X`)

Broadcast messages are addressed to `X` (Everyone). This node **acts on them** and then **forwards the packet** down the daisy chain.

---

### `FWD` — Broadcast Forward

**From:** Any known team member  
**To:** `X` (Everyone)

| Byte(s) | Variable Name | C Type | Min | Max | Example |
|---------|--------------|--------|-----|-----|---------|
| 4–6 | `cmd` | `char[3]` | — | — | `FWD` |
| 7–61 | `padding` | `uint8_t` | 0x00 | 0x00 | 0x00 |

> **Action:** Same as direct `FWD`. Then forwards the original packet unchanged.

---

### `REV` — Broadcast Reverse

**From:** Any known team member  
**To:** `X` (Everyone)

| Byte(s) | Variable Name | C Type | Min | Max | Example |
|---------|--------------|--------|-----|-----|---------|
| 4–6 | `cmd` | `char[3]` | — | — | `REV` |
| 7–61 | `padding` | `uint8_t` | 0x00 | 0x00 | 0x00 |

> **Action:** Same as direct `REV`. Then forwards the original packet unchanged.

---

### `STOP` — Broadcast Stop

**From:** Any known team member  
**To:** `X` (Everyone)

| Byte(s) | Variable Name | C Type | Min | Max | Example |
|---------|--------------|--------|-----|-----|---------|
| 4–7 | `cmd` | `char[4]` | — | — | `STOP` |
| 8–61 | `padding` | `uint8_t` | 0x00 | 0x00 | 0x00 |

> **Action:** Same as direct `STOP`. Then forwards the original packet unchanged.

---

## Messages Sent

---

### `ACK` — Acknowledgement

**From:** `B` (Bryce)  
**To:** Original sender of the command

Sent automatically whenever a valid, correctly-addressed command is received.

| Byte(s) | Variable Name | C Type | Min | Max | Example |
|---------|--------------|--------|-----|-----|---------|
| 4 | `cmd[0]` | `char` | `A` (0x41) | `A` (0x41) | `A` |
| 5 | `cmd[1]` | `char` | `C` (0x43) | `C` (0x43) | `C` |
| 6 | `cmd[2]` | `char` | `K` (0x4B) | `K` (0x4B) | `K` |
| 7–61 | `padding` | `uint8_t` | 0x00 | 0x00 | 0x00 |

> **Trigger:** Sent in response to any valid direct message (`FWD`, `REV`, `STOP`, or any unrecognized command).  
> **Note:** ACK is sent even for unknown commands — the node acknowledges receipt, but motor state remains unchanged in that case.

---

## Error Handling

| Error Condition | Detection Method | Action Taken |
|----------------|-----------------|--------------|
| Malformed packet | `prefix != "AZ"` or `suffix != "BY"` | Discard silently, print error |
| Unknown sender | `src` not in `KNOWN_IDS` | Discard silently, print error |
| Own message looped back | `src == MY_ID ('B')` | Discard (loop prevention) |
| Buffer overflow | `len(buffer) > 128 bytes` | Clear entire buffer, print error |
| Unknown command (direct) | Payload not `FWD`/`REV`/`STOP` | ACK sent, motor state unchanged |
| Out-of-frame bytes | Bytes before valid `AZ` prefix | Re-sync: strip bytes until `AZ` found |

---

## Message Forwarding Rules

| `dst` value | Action |
|------------|--------|
| `B` (this node) | Process command + send ACK |
| `X` (broadcast) | Execute command + forward packet |
| Any other known ID | Forward packet unchanged (no ACK, no action) |

---

## Hardware Summary

| Signal | Pin | Function |
|--------|-----|----------|
| UART TX | GPIO 43 | Daisy-chain transmit |
| UART RX | GPIO 44 | Daisy-chain receive |
| `dir_pin` | GPIO 18 | Motor direction (1=FWD, 0=REV) |
| `pwm_pin` | GPIO 16 | Motor enable/PWM |
| `dis` | GPIO 15 | Driver disable (active low enable) |
| `cs` | GPIO 14 | SPI chip select |
| `led` | GPIO 6 | Status LED (on = motor running) |
| Debug button | GPIO 5 | Cycles STOP→FWD→REV locally |
| Failsafe (BOOT) | GPIO 0 | Hold 1.5s to emergency stop |

---

## Failsafe Behavior

- **Startup check:** If the BOOT button (GPIO 0) is held at power-on, the node enters safe mode immediately (motor stopped, program exits).
- **Runtime check:** If BOOT is held for **>1500 ms** during operation, the motor is stopped and the program exits.
- **Debug button (GPIO 5):** Locally cycles motor state `STOP → FWD → REV → STOP` without requiring a UART message. Debounced at 50 ms.
