---
title: API - Motor Subsystem (Bryce)
---

## Message Structure

B - Bryce <br>
H - Hattie <br>
T - Tim <br>
F - Riley <br>
W - Rylee <br> 
E - Everyone <br>

# API – Motor Driver (Node 0x02)

**Owner:** Bryce (B)  
**Subsystem:** Motor Driver  
**Node ID:** `0x02`  
**Protocol:** Team 301 (Big-endian)

---

## Messages Received

---

### `0x0001` — Set Motor Speed
**From:** Riley (F) or upstream  
**To:** Bryce (B)  
**Type:** <span class="tag recv">Receive</span>

Command to set motor speed and direction.

| Byte(s) | Field | Type | Bytes | Min | Max | Example |
|--------|------|------|------|-----|-----|--------|
| 4–5 | `message_type` | `uint16_t` | 2 | 0x0001 | 0x0001 | 0x0001 |
| 6 | `motor_id` | `uint8_t` | 1 | 1 | 5 | 1 |
| 7 | `speed_high` | `uint8_t` | 1 | 0 | 255 | 0 |
| 8 | `speed_low` | `uint8_t` | 1 | 0 | 255 | 150 |
| 9 | `direction` | `uint8_t` | 1 | 0 | 1 | 0 |
| 10 | `control_flags` | `uint8_t` | 1 | 0 | 255 | 0 |
| 11–61 | `reserved` | `uint8_t[]` | 51 | 0 | 0 | 0x00… |

> **Notes**
> - Speed = `(speed_high << 8) | speed_low`
> - Valid RPM: **0–1000**
> - `control_flags` undefined (team spec gap)

---

### `0x0002` — Request Telemetry
**From:** Riley (F)  
**To:** Everyone (E)  
**Type:** <span class="tag recv">Receive (Broadcast)</span>

Requests telemetry data from all nodes.

| Byte(s) | Field | Type | Bytes | Min | Max | Example |
|--------|------|------|------|-----|-----|--------|
| 4–5 | `message_type` | `uint16_t` | 2 | 0x0002 | 0x0002 | 0x0002 |
| 6 | `telemetry_mask` | `uint8_t` | 1 | 0 | 255 | 0x1F |
| 7 | `timeout_sec` | `uint8_t` | 1 | 1 | 255 | 5 |
| 8–61 | `reserved` | `uint8_t[]` | 54 | 0 | 0 | 0x00… |

> **Notes**
> - bit4 = Motor RPM  
> - Only responds if bit4 is set  

---

## Messages Sent

---

### `0x0003` — Telemetry Packet
**From:** Bryce (B)  
**To:** Riley (F)  
**Type:** <span class="tag send">Send</span>

Telemetry response containing motor status.

| Byte(s) | Field | Type | Bytes | Min | Max | Example |
|--------|------|------|------|-----|-----|--------|
| 4–5 | `message_type` | `uint16_t` | 2 | 0x0003 | 0x0003 |
| 6–7 | `distance_mm` | `uint16_t` | 2 | 0 | 0 |
| 8 | `motion` | `uint8_t` | 1 | 0 | 1 |
| 9–10 | `temperature_tenths_c` | `int16_t` | 2 | 0 | 0 |
| 11–12 | `motor_rpm` | `uint16_t` | 2 | 0 | 1000 | 300 |
| 13 | `status_flags` | `uint8_t` | 1 | 0 | 7 |
| 14–61 | `reserved` | `uint8_t[]` | 48 | 0 | 0 |

> **Notes**
> - bit0 = running  
> - bit1 = error  
> - bit2 = low battery  

---

### `0x0004` — ACK
**From:** Bryce (B)  
**To:** Original sender  
**Type:** <span class="tag send">Send</span>

Acknowledges successful command execution.

| Byte(s) | Field | Type | Bytes | Min | Max |
|--------|------|------|------|-----|-----|
| 4–5 | `message_type` | `uint16_t` | 2 | 0x0004 | 0x0004 |
| 6 | `acked_msg_type` | `uint8_t` | 1 | 0x01 | 0xFF |
| 7 | `status` | `uint8_t` | 1 | 0 | 1 |
| 8 | `error_code` | `uint8_t` | 1 | 0 | 0x08 |
| 9–61 | `text` | `char[]` | 53 | — | — |

---

### `0x0005` — Error / Event Log
**From:** Bryce (B)  
**To:** Riley (F)  
**Type:** <span class="tag send">Send</span>

Sent when a motor fault occurs.

| Byte(s) | Field | Type | Bytes | Min | Max | Example |
|--------|------|------|------|-----|-----|--------|
| 4–5 | `message_type` | `uint16_t` | 2 | 0x0005 | 0x0005 |
| 6 | `error_code` | `uint8_t` | 1 | 0x01 | 0x08 | 0x03 |
| 7 | `severity` | `uint8_t` | 1 | 0 | 3 | 2 |
| 8–61 | `message_text` | `char[]` | 54 | — | — |

> **Error Codes**
> 0x01 Motor not found  
> 0x02 Invalid parameter  
> 0x03 Overcurrent  
> 0x04 TTL expired  
> 0x05 Destination unreachable  
> 0x06 CRC failure  
> 0x07 Unsupported message  
> 0x08 Resource busy  
