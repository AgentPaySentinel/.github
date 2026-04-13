

# 🌞 SolarFi — Pay-As-You-Go Solar Powered by Stellar

**SolarFi** is a blockchain-powered Pay-As-You-Go (PAYG) solar system that directly connects **micropayments to physical electricity access**.

Unlike traditional fintech apps that only move money, SolarFi controls **real-world hardware**. When a user’s credit runs out, the system automatically cuts power via a relay. When they pay, electricity is restored — instantly.

---

## 🚀 What Makes SolarFi Different

* ⚡ **Money → Electricity Bridge**
  Payments on the blockchain directly control power supply.

* 🔗 **Blockchain + IoT Integration**
  Combines **ESP32 hardware**, **MQTT messaging**, and **Soroban smart contracts**.

* 💸 **Ultra-Low Cost Micropayments**
  Powered by Stellar with near-zero fees.

* 🌍 **Real-World Impact**
  Inspired by PAYG leaders like M-KOPA, but removes reliance on costly SMS infrastructure.

---

## 🏗️ System Architecture

SolarFi consists of **four tightly integrated layers**:

### 1. 🔌 IoT Hardware Layer

* **ESP32** microcontroller
* **PZEM-004T** energy meter
* **Relay module**

**Responsibilities:**

* Measure energy consumption every 10 seconds
* Control electricity ON/OFF
* Publish data via MQTT

---

### 2. 🌐 Communication Layer (MQTT)

* Lightweight messaging protocol
* Enables real-time communication between devices and backend

**Flow:**

```
ESP32 → MQTT Broker → Backend Bridge
```

---

### 3. ⚙️ Backend Bridge (Node.js / Python Hybrid)

Acts as the **translator between blockchain and hardware**:

* Subscribes to MQTT topics
* Listens to blockchain events
* Sends relay commands to ESP32

**Core Responsibilities:**

* Sync energy usage with user credit
* Trigger power cutoff when balance = 0
* Update system state in real-time

---

### 4. 🧠 Smart Contract Layer (Soroban)

Built on Stellar using Soroban.

**Responsibilities:**

* Store user balances
* Deduct credit based on usage
* Enforce tariff pricing
* Emit events for backend

---

### 5. 📱 Frontend Layer (React App)

User interface for:

* Checking balance
* Making payments
* Viewing energy usage
* Managing account

---

## 🔁 End-to-End Flow

1. User sends payment via Stellar
2. Soroban contract updates balance
3. Event is emitted
4. Backend bridge detects event
5. MQTT message sent to ESP32
6. Relay turns ON power
7. Energy consumption tracked in real-time
8. Balance decreases until zero
9. Relay turns OFF power automatically

---

## 💡 Real-World Validation

* PAYG solar is already proven:

  * M-KOPA serves **700,000+ homes**
  * Handles **30M+ micropayments/year**
* Typical user spends:

  * ~$0.50/day on energy
* Stellar fees:

  * ~$0.00001 → **massive cost reduction**

---

## 🧰 Tech Stack

### Frontend

* React.js
* Tailwind CSS
* Stellar Wallet Integration

### Backend

* Node.js (API + bridge logic)
* MQTT (Mosquitto broker)

### Blockchain

* Stellar Network
* Soroban Smart Contracts (Rust)

### Hardware

* ESP32
* PZEM-004T Energy Meter
* Relay Module

---

## 📁 Project Structure

```
solarfi/
│
├── frontend/           # React app
│
├── backend/
│   ├── api/            # Express APIs
│   ├── bridge/         # MQTT ↔ Stellar listener
│
├── contracts/
│   └── solarfi/        # Soroban smart contract (Rust)
│
├── firmware/
│   └── esp32/          # ESP32 code
│
├── docs/               # Architecture & specs
│
└── README.md
```

---

## 🔧 Hardware Setup

### Required Components

* ESP32 (~$5)
* PZEM-004T (~$6)
* Relay module
* Power supply

### Why You Must Start Early

Shipping (AliExpress, etc.) takes **2–3 weeks**, and:

* Firmware cannot be tested without hardware
* Relay control is core to system validation

---

## ⚙️ Smart Contract Design (Soroban)

### Core Functions

* `deposit(user, amount)`
* `consume(user, units)`
* `get_balance(user)`
* `cutoff(user)`

### Key Logic

* Deduct credit per watt-hour consumed
* Emit event when:

  * Balance updated
  * Balance hits zero

---

## 🔌 MQTT Topics

```
solarfi/device/{deviceId}/usage
solarfi/device/{deviceId}/relay
solarfi/device/{deviceId}/status
```

---

## 🧪 Development Roadmap

### Phase 1: Setup

* [ ] Create monorepo
* [ ] Setup React frontend
* [ ] Setup Node.js backend
* [ ] Deploy MQTT broker

### Phase 2: Blockchain

* [ ] Write Soroban contract
* [ ] Deploy to testnet
* [ ] Integrate wallet payments

### Phase 3: Backend Bridge

* [ ] Listen to Stellar events
* [ ] Connect MQTT broker
* [ ] Implement relay triggers

### Phase 4: Firmware

* [ ] Read PZEM-004T data
* [ ] Publish MQTT messages
* [ ] Control relay

### Phase 5: Integration

* [ ] End-to-end testing
* [ ] Simulate low balance cutoff
* [ ] Optimize latency

---

## ⚠️ Key Challenges

* Real-time synchronization between blockchain & hardware
* Network reliability in rural environments
* Secure device authentication
* Handling offline scenarios

---

## 🔐 Security Considerations

* Signed MQTT messages
* Secure wallet transactions
* Device ID verification
* Rate limiting on backend

---

## 🌍 Future Improvements

* Mobile app (React Native)
* Offline-first payments (USSD fallback)
* AI usage prediction
* Multi-device household support


