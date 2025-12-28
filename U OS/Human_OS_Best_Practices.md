# Human OS Best Practices

## 1. Task Chunking (Transfer-Encoding)
**Problem:** Sending large payloads (e.g., "Write Thesis") triggers a Buffer Overflow in the Pre-Frontal Cortex (RAM), causing `408 Timeout`.
**Solution:** Use `Transfer-Encoding: chunked`. Break the payload into atomic streams.
* **Rule:** The first chunk must require < 2% CPU to execute (e.g., "Open Laptop").

## 2. The WebSocket Upgrade (Flow State)
**Concept:** Standard work is HTTP (high overhead). Flow is a WebSocket (persistent connection).
**The Handshake:** You cannot force Flow. You must present a valid `Sec-WebSocket-Key` (Ritual).
* **Valid Keys:** Noise-canceling headphones, specific tea, clearing the desk.
* **Keep-Alive:** Send a "Heartbeat" signal (small win/micro-action) every 5-10 minutes to prevent the connection from timing out.

## 3. Memory Management (Garbage Collection)
**Constraint:** The kernel has a hardcoded **Ultradian Rhythm** (90-minute cycle).
**Strategy: Async/Await (The Rust Model)**
Instead of fighting the "Dip" (90-110 min mark):
1.  **Release Lock:** Stop Logic Thread.
2.  **Context Switch:** Activate Motor Thread (Walk/Stretch).
3.  **No Input:** Do not consume content (phone) during GC.
* **See:** [[Human_OS_Snippets#Snippet 4: The NSDR Reset (Unsafe Block)]]

## 4. Security (Webhook Verification)
**Vulnerability:** Anxiety and intrusive thoughts spoof `CRITICAL_ALERT` webhooks.
**Defense:** Verify the **HMAC Signature**.
* Ask: "Is this alert based on immediate physical evidence?"
* If `False`: Return `403 Forbidden` and drop packet.
* 