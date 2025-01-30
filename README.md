**# Mini Proof of Work Blockchain in Go**

## Overview
This project is a simple implementation of a Proof of Work (PoW) blockchain using Go for my core development Learning. It demonstrates how blocks are linked, hashed, and mined using a lightweight PoW algorithm that is designed to be much less resource-intensive than traditional PoW.

## Features
- Implements a basic blockchain structure
- Uses a simple cryptographic hash function for efficiency
- Includes a Proof of Work consensus mechanism with minimal computational overhead
- Adjustable difficulty level to control mining time
- Ability to run and test multiple nodes locally

## Getting Started

### Prerequisites
Ensure you have Go installed. If not, install it from the [official site](https://golang.org/doc/install).

### Installation
```sh
# Clone the repository
git clone https://github.com/Saiweb3dev/Mini_PoW_Blockchain.git
cd Mini_PoW_Blockchain

# Initialize Go module
go mod init Mini_PoW_Blockchain
```

### Running the Blockchain
```sh
go run main.go
```

### Expected Output
The output will show blocks being mined and added to the chain, including their hashes and nonce values.

## Folder Structure
```
mini-pow-blockchain/
│── cmd/                # Entry points for running different services
│   ├── node/           # Runs a full blockchain node
│   │   ├── main.go
│   ├── miner/          # Dedicated miner service
│   │   ├── main.go
│── internal/           # Core blockchain logic
│   ├── blockchain/     # Blockchain structure, validation, PoW
│   │   ├── blockchain.go
│   │   ├── pow.go
│   ├── network/        # P2P network communication
│   │   ├── network.go
│   ├── transaction/    # Transaction handling
│   │   ├── transaction.go
│── pkg/                # Shared utilities (logging, cryptography)
│   ├── utils/          # Common utility functions
│   │   ├── hash.go
│── api/                # REST API for interacting with the blockchain
│   ├── server.go
│── config/             # Configuration files
│   ├── config.json
│── tests/              # Unit tests for blockchain logic
│── go.mod              # Go module dependencies
│── README.md           # Documentation
```

## Components Explanation

### **1. Node (`cmd/node/main.go`)**
- Listens for new blocks from miners and adds them to the blockchain.
- Maintains a local copy of the blockchain and syncs with other nodes.
- Provides a REST API (`api/server.go`) for interaction.

### **2. Miner (`cmd/miner/main.go`)**
- Continuously mines new blocks.
- Solves the PoW puzzle and broadcasts the block to nodes.
- Uses a lightweight hash function to keep computation minimal.

### **3. Blockchain Logic (`internal/blockchain/`)**
- **`blockchain.go`**: Defines the block structure and blockchain operations (adding blocks, verifying chain).
- **`pow.go`**: Implements the lightweight PoW mechanism (e.g., using BLAKE2b instead of SHA-256).

### **4. Network (`internal/network/`)**
- Implements a simple P2P network where nodes can communicate.
- Uses WebSockets or HTTP to exchange blocks and transactions.

### **5. Transactions (`internal/transaction/`)**
- Defines a transaction structure (sender, receiver, amount).
- Implements a simple transaction pool for unconfirmed transactions.

### **6. API (`api/server.go`)**
- Provides endpoints for users to interact with the blockchain.
- Example:
  ```sh
  curl http://localhost:8080/blocks
  ```

### **7. Utility Functions (`pkg/utils/hash.go`)**
- Handles hashing functions.
- Example:
  ```go
  package utils

  import "golang.org/x/crypto/blake2b"

  func Hash(data string) []byte {
      hash := blake2b.Sum256([]byte(data))
      return hash[:]
  }
  ```

## How It Works
1. **Blockchain Structure**
   - Each block contains:
     - Timestamp
     - Data (transactions or messages)
     - Previous block's hash
     - Current block's hash
     - Nonce (used for mining)

2. **Proof of Work (PoW)**
   - A simple hashing algorithm is used to simulate PoW.
   - Instead of SHA-256, a lightweight hash function (e.g., XOR-based or a reduced-bit SHA variant) is used for efficiency.
   - The difficulty target is dynamically adjusted to keep block mining time reasonable.

3. **Mining Process**
   - A new block is created with a reference to the previous block.
   - A nonce is incremented until a hash meeting the difficulty condition is found.
   - The block is then added to the chain.

## Roadmap
1. Implement basic blockchain structure ✅
2. Add lightweight Proof of Work algorithm ✅
3. Validate the blockchain ✅
4. Implement transaction handling (Planned)
5. Multi-node network simulation (Planned)
6. Explore alternative consensus mechanisms (Planned)

## Contributing
Feel free to fork the repo and submit pull requests!

## License
This project is licensed under the MIT License - see the LICENSE file for details.
