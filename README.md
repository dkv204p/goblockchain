# ⛓️ Go Blockchain & Wallet System

A minimal, educational implementation of a **decentralized Proof-of-Work blockchain** and a **web-based wallet system** built in **Go**.  
This project demonstrates blockchain fundamentals from scratch, including **block creation**, **transaction signing**, and a **simple peer-to-peer consensus mechanism**.

---

## 🚀 Features

- **Decentralized Node**:  
  The `blockchain_server` acts as a full node that can mine new blocks and synchronize with peers.

- **Proof-of-Work (PoW)**:  
  A mining algorithm secures the network by requiring computational effort to create new blocks.

- **Cryptographic Wallets**:  
  The `wallet` package handles secure generation of **ECDSA key pairs** and **Base58Check-style blockchain addresses**.

- **Transaction Management**:  
  Users can create and sign transactions, which are broadcast across the network.

- **RESTful API**:  
  Both blockchain and wallet servers expose APIs for communication.

- **Web UI**:  
  The `wallet_server` provides a basic interface to create wallets, view balances, and send transactions.

---

## 📂 Project Structure

```
├── block/              # Core blockchain logic (Block, Blockchain, mining, validation, consensus)
├── blockchain_server/  # Runs a blockchain node (mining, transactions, chain sync)
├── wallet/             # Cryptographic key pairs & transactions
├── wallet_server/      # Web server for wallet UI
├── utils/              # Helper functions (crypto, networking, responses)
└── wallet_server/templates/
                  └── index.html      # Wallet web UI

````

---

## ⚙️ Getting Started

### ✅ Prerequisites
- [Go](https://go.dev/dl/) (v1.20+ recommended)

### 🛠 Setup

Clone the repository and initialize dependencies:

```bash
git clone https://github.com/dkv204p/goblockchain.git
cd goblockchain
go mod init goblockchain
go mod tidy
````

---

## ▶️ Running the System

You need to run both the **blockchain server** and the **wallet server** in separate terminals.

### 1️⃣ Start the Blockchain Server

```bash
cd blockchain_server
go run . --port=5000
```

* Runs a blockchain node
* Begins mining automatically
* Searches for other nodes

### 2️⃣ Start the Wallet Server

```bash
cd wallet_server
go run . --port=8080 --gateway="http://127.0.0.1:5000"
```

* Starts the wallet’s web server
* Connects to the blockchain node

### 3️⃣ Access the Wallet UI

Open your browser:
👉 [http://127.0.0.1:8080](http://127.0.0.1:8080)

---

## 💰 How to Use the Wallet

1. **Get Funds (Mine a Block)**

   * New wallets start with `0` balance.
   * Trigger mining:
     [http://127.0.0.1:5000/mine](http://127.0.0.1:5000/mine)
   * A reward (`1.0`) is added to your balance.

2. **Send a Transaction**

   * Run another wallet server on a different port:

     ```bash
     go run . --port=8081 --gateway="http://127.0.0.1:5000"
     ```
   * Copy the new wallet’s address.
   * In the first wallet, paste it into the **Address** field → enter amount → click **Send**.

3. **Confirm the Transaction**

   * The transaction will be **pending**.
   * Mine another block (`/mine`) to confirm it.
   * The recipient’s balance updates.

---

## 📡 API Endpoints

### ⛓ Blockchain Server (default port: `5000`)

| Method | Endpoint                | Description                                                                     |
| ------ | ----------------------- | ------------------------------------------------------------------------------- |
| `GET`  | `/chain`                | Get the full blockchain (all blocks).                                           |
| `GET`  | `/mine`                 | Mine a new block and receive reward.                                            |
| `POST` | `/transactions/new`     | Submit a new transaction (JSON body with sender, recipient, amount, signature). |
| `GET`  | `/transactions/pending` | View pending transactions waiting to be mined.                                  |
| `POST` | `/nodes/register`       | Register a new node in the network.                                             |
| `GET`  | `/nodes/resolve`        | Resolve conflicts and achieve consensus.                                        |

### 👛 Wallet Server (default port: `8080`)

| Method | Endpoint              | Description                                               |
| ------ | --------------------- | --------------------------------------------------------- |
| `GET`  | `/wallet`             | Generate a new wallet (public/private keypair + address). |
| `GET`  | `/wallet/balance`     | Check wallet balance.                                     |
| `POST` | `/wallet/transaction` | Create & broadcast a signed transaction.                  |
| `GET`  | `/`                   | Access the wallet web UI (index.html).                    |

---
## 🔮 Future Improvements

* **Persistence**: Use a database (e.g., BoltDB, SQLite) for blockchain & transaction pool storage.
* **Advanced Consensus**: Replace longest-chain rule with **authenticated gossip protocol** or other consensus.
* **Transaction Fees**: Introduce miner rewards via fees.
* **Security Enhancements**: Harden against attacks (input parsing, overflows, etc.).

---

## 📜 License

This project is licensed under the **MIT License** – feel free to use and modify it for educational purposes.

---
💡 *Built with Go for learning blockchain fundamentals.*
