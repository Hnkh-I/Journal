# TECHNICAL SPECIFICATION: PROJECT "BISOTUN NETWORK"

## 1. SYSTEM ARCHITECTURE OVERVIEW
The system is a "Fat Client" architecture with a "Thin Relay" network. It is designed to be fully functional in a `Local-First` capacity (Offline), syncing to a `Distributed Hash Table (DHT)` only when connectivity permits.

**The Stack:**
* **Base:** Fork of Telegram Android Client (Java/C++ via JNI).
* **Mesh Layer:** Meshtastic / Berty Protocol (BLE & WiFi Direct).
* **Ledger Layer:** RxDB (JavaScript/WASM running in a WebView sandbox).
* **The Catalyst:** TensorFlow Lite (On-device risk scoring).

## 2. THE CLIENT (THE TROJAN)
We will fork an open-source Telegram client (e.g., Nekogram or Forkgram) to utilize their existing anti-censorship routing and UI.

### 2.1 The UI Injection
* **Tab Addition:** Add a new primary tab labeled "Radar" or "Mesh."
* **The WebView Container:** This tab loads a local `index.html` (Vue.js PWA) stored in the app's assets. This ensures the crypto/ledger logic is sandboxed and easily updatable.
* **Bridge:** A Javascript Interface (`WebViewJavascriptBridge`) connects the Vue.js app to the Native Telegram Core (for accessing Contacts and Notification services).

### 2.2 The Mesh Networking Service (Background)
A background Android Service that runs independently of the Telegram servers.
* **Transport:**
    * **Bluetooth LE:** For peer discovery within 10-30 meters.
    * **Wi-Fi Direct:** For high-bandwidth ledger sync within 100 meters.
    * **mDNS / Local Network:** For discovery on the same LAN (Office/Bazaar WiFi).
* **Protocol:** Use **Berty Protocol** (IPFS-based) logic.
    * Device A advertises a `topic` (hash of the community ID).
    * Device B scans for `topic`.
    * Handshake established via Ephemeral Keys.

## 3. THE LEDGER (MUTUAL CREDIT PROTOCOL)
The economy operates on a **Signed Directed Graph** (DAG), not a linear Blockchain.

### 3.1 Data Structure (Holochain-Lite)
* **Agent Chain:** Each user has their own local append-only log.
* **Transaction Schema:**
    ```json
    {
      "id": "UUID",
      "timestamp": 1704067200,
      "counterparty_id": "Pub_Key_B",
      "amount": 5000,
      "type": "CREDIT",
      "previous_hash": "0xABC...",
      "signature": "Curve25519_Sig"
    }
    ```
* **Countersigning:** A transaction is valid ONLY if signed by both Sender and Receiver.

### 3.2 The Handshake (The "Mediator")
To initiate a trade without a server:
1.  **Visual (QR):** Sender generates a QR code containing the `Transaction Payload` + `Session Key`.
2.  **Scan:** Receiver scans QR. App verifies signature.
3.  **Counter-Sign:** Receiver signs the payload.
4.  **Transport:**
    * *If Mesh Active:* Signed payload is sent back via BLE.
    * *If Air-Gapped:* Receiver generates a **Response QR** code. Sender scans it to finalize.

## 4. THE CATALYST (ON-DEVICE AI)
The "Catalyst" is a background worker that acts as the Governance and Risk engine.

* **Input:** The User's local transaction history + Peer Reputation Graph.
* **Function:** `Entropy_Reduction()`
* **Logic:**
    * *Credit Limit Calculation:* "User B has high velocity but low default rate. Recommend limit: 50M Tomans."
    * *Loop Detection:* "User A owes you 100. You owe User C 100. User C owes User A 100. Initiate 3-way atomic swap?"
* **Implementation:** TensorFlow Lite model trained on synthetic transaction data, running locally.

## 5. NETWORK SYNCHRONIZATION (GOSSIP)
How the ledger spreads without a central server.

* **Gossip Protocol:** When Phone A connects to Phone B (Mesh or Internet), they exchange "Bloom Filters" of their known transaction headers.
* **Immune Response:** If Phone A sees a conflicting transaction from Phone B (Double Spend), the Catalyst flags the peer as "Dishonest" locally and gossips this Reputation Score to trusted neighbors.

## 6. ROADMAP TO MVP

**Phase 1: The "Handshake" (Weeks 1-4)**
* Standalone PWA (Vue.js).
* RxDB Local Storage.
* QR Code generation/scanning.
* *Deliverable:* Two phones can track a debt offline.

**Phase 2: The "Skin" (Weeks 5-8)**
* Fork Telegram Android.
* Inject the PWA into the "Radar" tab.
* *Deliverable:* A working Telegram client that has a hidden ledger.

**Phase 3: The "Mesh" (Weeks 9-12)**
* Integrate BLE/WiFi Direct libraries.
* Enable background syncing of ledgers.
* *Deliverable:* Walking into a Bazaar updates your ledger automatically.

**Phase 4: The "Catalyst" (Weeks 13+)**
* Deploy the Loop Detection algorithms.
* Enable automated credit clearing.
