# Human OS API Specification v1.3

## System Architecture
* **Kernel Space:** Biological firmware (Autonomic Nervous System). *Read-Only.*
* **User Space:** Conscious awareness. *Read/Write.*

---

## 1. Protocols
The OS supports three modes of operation based on context.

| Protocol | Protocol Name | Use Case | Latency | Cost |
| :--- | :--- | :--- | :--- | :--- |
| **HTTP/1.1** | Standard REST | Discrete Tasks | High | High (Context Switching) |
| **WS://** | WebSockets | Flow State / Deep Work | ~0ms | Low (Persistent) |
| **Webhook** | Event-Driven | Habits / Reflexes | Instant | Zero (Passive) |

---

## 2. Internal Endpoints (`localhost`)

### State Monitoring
#### `GET /system/state`
Returns current telemetry.
* **Returns:** `{ "glucose": int, "dopamine": float, "alertness": "string" }`
* **Rate Limit:** None. Frequent polling recommended (Mindfulness).

#### `GET /process/active`
Returns background processes consuming RAM (Working Memory).
* **Optimization:** If `count > 3`, trigger [[Human_OS_Snippets#Snippet 3: RAM Dump (Journaling)|RAM Dump]].

### Execution Engine
#### `POST /task/queue`
Submits an intent to the behavioral engine.
* **Header:** `Transfer-Encoding: chunked` (Mandatory for complex tasks).
* **Payload:** Must be atomic actions.
* **Returns:** `200 OK` (Dopamine ACK).
* **Error:** `408 Timeout` (Procrastination) if payload is too large.

#### `GET /flow/session`
Request to upgrade connection to WebSocket (Flow State).
* **Header:** `Upgrade: websocket`
* **Header:** `Sec-WebSocket-Key: [Ritual_Key]`
* **See:** [[Human_OS_Best_Practices#2. The WebSocket Upgrade (Flow State)]]

---

## 3. External Endpoints (I/O)

#### `STREAM /input/sensory`
Raw data feed (Eyes/Ears).
* **Filter:** Reticular Activating System (RAS). Configurable via Intent.

#### `POST /output/communication`
* **Params:** `protocol` (verbal/non-verbal), `encryption` (jargon/plain).

---

## 4. Error Codes

| Code | Status | Cause | Fix |
| :--- | :--- | :--- | :--- |
| **400** | Bad Request | Brain Fog / Unclear Intent | Simplify Input |
| **408** | Timeout | Task Complexity > Energy | Apply [[Human_OS_Best_Practices#1. Task Chunking (Transfer-Encoding)]] |
| **429** | Too Many Requests | Overwhelm | Activate Single-Thread Mode |
| **503** | Service Unavailable | Burnout | Hard Sleep Reset |
