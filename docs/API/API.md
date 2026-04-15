---
title: API
---

## Message Structure

B - Bryce <br>
H - Hattie <br>
T - Tim <br>
F - Riley <br>
W - Rylee <br> 
E - Everyone <br>

# API – Message Compliance Verification

**Subsystem:** Motor Driver  
**Node ID:** `0x02` (Bryce)  
**Protocol:** Team 301  
**Endianness:** Big-endian  

---

## Messages received by this node

---

### `0x0001` – Set Motor Speed  
**Type:** Receive  

Command to set motor speed and direction. Sent from Riley (0x01) or any upstream node with destination 0x02. This node consumes the packet and applies the motor command.

| Byte(s) | Variable name | C data type | # bytes | Min | Max | Example |
|--------|--------------|------------|--------|-----|-----|--------|
| 4–5 | `message_type` | `uint16_t` | 2 | 0x0001 | 0x0001 | 0x0001 |
| 6 | `motor_id` | `uint8_t` | 1 | 1 | 5 | 1 |
| 7 | `speed_high` | `uint8_t` | 1 | 0 | 255 | 0 |
| 8 | `speed_low` | `uint8_t` | 1 | 0 | 255 | 150 |
| 9 | `direction` | `uint8_t` | 1 | 0 (FWD) | 1 (REV) | 0 |
| 10 | `control_flags` | `uint8_t` | 1 | 0 | 255 | 0 |
| 11–61 | `reserved` | `uint8_t[]` | 51 | 0 | 0 | 0x00… |

!!! note
    Speed is a 16-bit value split across two bytes (big-endian).  
    Reconstruct in code as:
    
    ```c
    speed = (speed_high << 8) | speed_low;
    ```

    Valid RPM range: **0–1000**

    **Note:** `control_flags` currently has no defined meaning.

---

### `0x0002` – Request Telemetry  
**Type:** Receive (Broadcast)

Broadcast from Riley (0x01) to all nodes (destination 0xFF). This node responds with motor RPM if bit 4 is set.

| Byte(s) | Variable name | C data type | # bytes | Min | Max | Example |
|--------|--------------|------------|--------|-----|-----|--------|
| 4–5 | `message_type` | `uint16_t` | 2 | 0x0002 | 0x0002 | 0x0002 |
| 6 | `telemetry_mask` | `uint8_t` | 1 | 0 | 255 | 0x1F |
| 7 | `timeout_sec` | `uint8_t` | 1 | 1 | 255 | 5 |
| 8–61 | `reserved` | `uint8_t[]` | 54 | 0 | 0 | 0x00… |

!!! note
    Telemetry mask bits:  
    - bit0 = Distance  
    - bit1 = Motion  
    - bit2 = Temperature  
    - bit3 = Hall sensor  
    - **bit4 = Motor RPM**

    This node only responds if **bit4 is set**.

---

## Messages sent by this node

---

### `0x0003` – Telemetry Packet  
**Type:** Send  

Sent upstream to Riley (0x01) in response to telemetry request.

| Byte(s) | Variable name | C data type | # bytes | Min | Max | Example |
|--------|--------------|------------|--------|-----|-----|--------|
| 4–5 | `message_type` | `uint16_t` | 2 | 0x0003 | 0x0003 | 0x0003 |
| 6–7 | `distance_mm` | `uint16_t` | 2 | 0 | 0 | 0 |
| 8 | `motion` | `uint8_t` | 1 | 0 | 1 | 1 |
| 9–10 | `temperature_tenths_c` | `int16_t` | 2 | 0 | 0 | 0 |
| 11–12 | `motor_rpm` | `uint16_t` | 2 | 0 | 1000 | 300 |
| 13 | `status_flags` | `uint8_t` | 1 | 0 | 7 | 0x01 |
| 14–61 | `reserved` | `uint8_t[]` | 48 | 0 | 0 | 0x00… |

!!! note
    `status_flags` bits:  
    - bit0 = motor running  
    - bit1 = error  
    - bit2 = low battery  

---

### `0x0004` – ACK  
**Type:** Send  

Sent after executing a Set Motor Speed command.

| Byte(s) | Variable name | C data type | # bytes | Min | Max | Example |
|--------|--------------|------------|--------|-----|-----|--------|
| 4–5 | `message_type` | `uint16_t` | 2 | 0x0004 | 0x0004 | 0x0004 |
| 6 | `acked_msg_type` | `uint8_t` | 1 | 0x01 | 0xFF | 0x01 |
| 7 | `status` | `uint8_t` | 1 | 0 | 1 | 0 |
| 8 | `error_code` | `uint8_t` | 1 | 0 | 0x08 | 0 |
| 9–61 | `text` | `char[]` | 53 | — | — | "OK\\0" |

---

### `0x0005` – Error / Event Log  
**Type:** Send  

Sent when a motor fault occurs.

| Byte(s) | Variable name | C data type | # bytes | Min | Max | Example |
|--------|--------------|------------|--------|-----|-----|--------|
| 4–5 | `message_type` | `uint16_t` | 2 | 0x0005 | 0x0005 | 0x0005 |
| 6 | `error_code` | `uint8_t` | 1 | 0x01 | 0x08 | 0x03 |
| 7 | `severity` | `uint8_t` | 1 | 0 | 3 | 2 |
| 8–61 | `message_text` | `char[]` | 54 | — | — | "Motor overcurrent\\0" |

!!! note
    Error codes:  
    - 0x01 = Motor not found  
    - 0x02 = Invalid parameter  
    - 0x03 = Overcurrent  
    - 0x04 = TTL expired  
    - 0x05 = Destination unreachable  
    - 0x06 = CRC failure  
    - 0x07 = Unsupported message type  
    - 0x08 = Resource busy  


